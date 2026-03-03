# How to Correctly Add Apt Repositories

Due to the deprecation of `apt-key` it is advised to handle the keys and sources process manually when adding local apt repositories.
Previously, gpg keys were stored in `/etc/apt/keyrings`. New direction states that `/usr/share/keyrings` is more secure and is the best practice.

## Adding an `apt` Repository

When adding an apt repo, we must first install the associated gpg key then define the repo source.

### Installing the Key

To install the key, we rely on `curl` and `tee` like so:

```bash
curl -fsSL https://path.to.key.gpg | sudo tee /usr/share/keyrings/key.gpg
```

If the key is not in `gpg` format, utilize the `gpg` tool like so:

```bash
curl -fsSL https://path.to.nongpg.key | gpg --dearmor | sudo tee /usr/share/keyrings/key.gpg > /dev/null
```

\*note: the line `> /dev/null` ignores the `sudo tee` output

### Adding the `apt` Repository Source

To add the apt source, run something similar to the following:

```bash
echo "deb [signed-by=/usr/share/keyrings/key.gpg] https://path.to.deb example main" | sudo tee /etc/apt/sources.list.d/example.list
```

Update `apt` to sync sewly added repo:

```bash
sudo apt update
```
