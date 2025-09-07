# Best Practices `kubectl` Setup

## Setup `kubectl` for Raspberry Pi

Install gpg keys to the `trusted.gpg.d` directory

```bash
sudo curl -fsSLo /usr/share/keyrings/kubernetes-archive-keyring.gpg https://packages.cloud.google.com/apt/doc/apt-key.gpg
```

Add the Kubernetes `apt` repository

```bash
echo "deb [signed-by=/usr/share/keyrings/kubernetes-archive-keyring.gpg] https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list
```

Install `kubectl`

```bash
sudo apt update && sudo apt install -y kubectl
```
