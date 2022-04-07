![](virtual-machine-manager-settings.png "")

```sh
sudo -i
```

![](nixos-parted.png "")

```sh
parted /dev/vda -- mklabel gpt
parted /dev/vda -- mkpart primary 512MiB -8GiB
parted /dev/vda -- mkpart primary linux-swap -8GiB 100%
```

![](nixos-formatting.png "")

```sh
mkfs.ext4 -L nixos /dev/vda1
mkswap -L swap /dev/vda2
mkfs.fat -F 32 -n boot /dev/vda3
```

![](nixos-installing.png "")

```sh
mount /dev/disk/by-label/nixos /mnt
mount /dev/disk/by-label/boot /mnt/boot
swapon /dev/vda2
```

![](nixos-config.png "")
![](nixos-config-2.png "")

```sh
nixos-generate-config --root /mnt
vi /mnt/etc/nixos/configuration.nix
```

![](nixos-install.png "")

```sh
nixos-install
```

```sh
reboot
```

