

1. Create a bare VM with admin account for target distro (Ubuntu, RedHat/Rocky)

```bash
sudo cloud-init clean --logs
sudo apt update
sudo apt install -y qemu-guest-agent
sudo systemctl enable --now qemu-guest-agent
sudo sed -i '/^#HostKey/d' /etc/ssh/sshd_config
echo "HostKey /etc/ssh/ssh_host_ed25519_key" | sudo tee -a /etc/ssh/sshd_config
sudo rm /etc/ssh/ssh_host_* && sudo dpkg-reconfigure openssh-server
```