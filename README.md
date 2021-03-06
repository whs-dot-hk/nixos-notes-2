# Virtual Machine Manager Settings
Choose `UEFI` with no secure boot

![](virtual-machine-manager-settings.png "")

# Partitioning
```sh
sudo -i
```

```sh
parted /dev/vda -- mklabel gpt
parted /dev/vda -- mkpart primary 512MiB -8GiB
parted /dev/vda -- mkpart primary linux-swap -8GiB 100%
parted /dev/vda -- mkpart ESP fat32 1MiB 512MiB
parted /dev/vda -- set 3 esp on
```

![](nixos-parted.png "")

# Formatting
```sh
mkfs.ext4 -L nixos /dev/vda1
mkswap -L swap /dev/vda2
mkfs.fat -F 32 -n boot /dev/vda3
```

![](nixos-formatting.png "")

# Mounting
```sh
mount /dev/disk/by-label/nixos /mnt
mount /dev/disk/by-label/boot /mnt/boot
swapon /dev/vda2
```

![](nixos-installing.png "")

# Configuring
```sh
nixos-generate-config --root /mnt
vi /mnt/etc/nixos/configuration.nix
```

![](nixos-config.png "")
![](nixos-config-2.png "")

# Installing
```sh
nixos-install
```

![](nixos-install.png "")

# Success
Install finish reboot into the newly installed NixOS
```sh
reboot
```

![](nixos-install-finish.png "")

# Add User
```sh
useradd -m whs
passwd whs
```

![](nixos-useradd.png "")

# Install Vim
Add the line to `configuration.nix`
```
environment.systemPackages = with pkgs; [ vim ];
```
Run
```sh
nixos-rebuild switch
```

![](install-vim.png "")

# Reference
* https://nixos.org/manual/nixos/stable/index.html#ch-installation
* https://nixos.wiki/wiki/Vim
