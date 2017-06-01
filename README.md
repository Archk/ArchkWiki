# ArchkWiki
# wifi-menu
# nano /etc/pacman.d/mirrorlist
# pacman -Syy
#Partition
  sda        120G
  ├─sda1    vfat    512M    /boot/EFI
  ├─sda2    ext4    20G    /
  ├─sda3    ext4    20G    home
          mkfs.fat -F32 /dev/sda1    # 创建 FAT32 分区
          mkfs.ext4 /dev/sda2    # 创建 ext4 分区
          mkfs.ext4 /dev/sda3    # 创建 ext4 分区
              mount /dev/sda2 /mnt    # 挂载根目录
              mkdir /mnt/home    # 创建 /home 挂载点
              mount /dev/sda3 /mnt/home    # 挂载 /home
              mkdir -p /mnt/boot/EFI    # 创建 UEFI 挂载点
              mount /dev/sda1 /mnt/boot/EFI    # 挂载 UEFI 分区
# pacstrap /mnt base
# genfstab -U /mnt >> /mnt/etc/fstab
# cat /mnt/etc/fstab
# arch-chroot /mnt
# nano /etc/locale.gen    # 反注释
  locale-gen    # 生成 locale
  echo LANG=<locale>  > /etc/locale.conf # 设置默认 locale
# hwclock --systohc
# echo <主机名> > /etc/hostname
# nano /etc/hosts    # 将主机名填入 
#cat /etc/hostname
   <主机名>
# cat /etc/hosts
   127.0.0.1    localhost.localdomain    localhost
   ::1        localhost.localdomain    localhost
   127.0.1.1    <主机名>.localdomain    <主机名>
# pacman -S iw wpa_supplicant dialog
# wifi-menu    # 连接
# passwd
# pacman -S dosfstools grub efibootmgr
    grub-install --target=x86_64-efi --efi-directory=<EFI 分区挂载点> --bootloader-id=grub
    grub-mkconfig -o /boot/grub/grub.cfg
# exit    # 退回安装环境
# umount -R < / 挂载点>    # 卸载新分区
# reboot    # 重启
# 记得移除安装介质
# useradd -m -g users -s /usr/bin/bash <用户名>
    该命令创建一个名为 <用户名> 的用户，指定登陆 shell 为 bash，所属主用户组 users，用户文件夹位于 /home/<用户名>。
  # passwd <用户名>   # 设置密码
# pacman -S xf86-video-intel xorg-server xorg-xinit
# pacman -S urxvt-perls i3 firefox vim
#nano /etc/X11/xinit/xinitrc  行尾添加exec i3 注释最后几行
#vim $HOME/.Xresources
#git tmux vim emacs cscopectags htop nmap tcpdump socat tree wget
