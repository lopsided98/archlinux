FROM scratch
LABEL maintainer "lopsided"

ADD arch-rootfs/ /
ADD additional/ /

RUN : \
    # chmod /etc, because during add, there is /etc/resolv.conf
    # mounted (and therefore /etc/ created with the umask of the host)
    # if the umask is not ``
    && chmod 755 /etc \
    && pacman-key --init \
    && pacman-key --populate archlinuxarm \
    && pacman --noconfirm -Syu --needed base \
    # remove unneccessary packages again
    && pacman --noconfirm -Rsc \
         cryptsetup \
         device-mapper \
         dhcpcd \
         iproute2 \
         jfsutils \
         linux-raspberrypi \
         lvm2 \
         man-db \
         man-pages \
         mdadm \
         nano \
         netctl \
         openresolv \
         pciutils \
         raspberrypi-bootloader \
         raspberrypi-bootloader-x \
         raspberrypi-firmware \
         reiserfsprogs \
         s-nail \
         systemd-sysvcompat \
         usbutils \
         vi \
         wireless_tools \
         wpa_supplicant \
         xfsprogs \
    && rm -rf \
      /usr/share/man/* \
      /var/cache/pacman/pkg/* \
      /var/lib/pacman/sync/* \
      /README \
      /etc/pacman.d/mirrorlist.pacnew

CMD ["/bin/bash"]
