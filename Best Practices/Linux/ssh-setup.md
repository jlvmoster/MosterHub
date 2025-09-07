## Setting up GitHub SSH Access with Existing SSH Keys

Create a new file called `id_rsa` (or whatever you want to call it) and copy your private key to the new file:

```bash
touch ~/.ssh/id_rsa
```

Change the permissions to be more restrictive:

```bash
sudo chmod 600 ~/.ssh/id_rsa
```

Start the ssh-agent in the background:

```bash
eval $(ssh-agent -s)
```

Register the newly created private key with the ssh-agent:

```bash
ssh-add ~/.ssh/id_rsa
```

## Setting up SSH Access on a Raspberry Pi

Use Raspberry Pi Imager and enable ssh access by default with the `authorized_keys` field populated with the desired `ssh-rsa` public key of your local machine.

### Only Use Public Key Authentication for SSH Access

Modify `/etc/ssh/sshd_config` and change the following:

```diff
- #PubkeyAuthentication yes
+ PubkeyAuthentication yes

- PasswordAuthentication yes
+ PasswordAuthentication no
```

### Set SSH Access for `root` User

Enable SSH root access (temporary) by modifying `/etc/ssh/sshd_config` with the following changes:

```diff
- #PermitRootLogin prohibit-password
+ PermitRootLogin prohibit-password
```

Make the `.ssh` directory and add desired public key to the `.ssh/authorized_keys` file:

```bash
sudo su
cd /root
mkdir .ssh
chmod 700 .ssh
echo "<my public rsa key>" >> .ssh/authorized_keys
chmod 600 .ssh/authorized_keys
```

Restart ssh service

```bash
sudo service ssh restart
```

### Rename Default `pi` User to Desired Username

Login as root and rename `pi` to `jalo`:

```bash
usermod -l jalo pi
```

Rename `pi` group as well:

```bash
groupmod -n jalo pi
```

Rename the home directory to `jalo`:

```bash
usermod -m -d /home/jalo jalo
```

Rename and modify `/etc/sudoers.d/010_pi-nopasswd` with `visudo`:

```diff
- pi ALL=(ALL) NOPASSWD: ALL
+ jalo ALL=(ALL) NOPASSWD: ALL
```
