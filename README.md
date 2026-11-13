# qrca-pipewire-git

Arch Linux package for [Qrca](https://apps.kde.org/qrca/), KDE's QR code scanner, built from the
[`work/pipewire-camera`](https://github.com/u6bkep/qrca/tree/work/pipewire-camera) branch.

That branch makes Qrca capture camera frames through PipeWire instead of opening `/dev/video*`
directly. This makes cameras that need libcamera work, such as the Intel IPU3/IPU6 sensors in
Surface devices and many laptops. Stock Qrca (Qt Multimedia 6.11) finds no camera on them. When
PipeWire has no camera, Qrca falls back to Qt Multimedia as before.

It replaces the `qrca` package (`provides`/`conflicts`), including the Wi-Fi scanner that the
Plasma network widget opens.

## Install

```sh
git clone https://github.com/u6bkep/qrca-pipewire-pkgbuild.git
cd qrca-pipewire-pkgbuild
makepkg -si
```

For libcamera cameras, also install `libcamera`, `libcamera-ipa` and `pipewire-libcamera`, then
restart PipeWire (`systemctl --user restart pipewire wireplumber`). `cam -l` should list your
cameras.

To go back to the stock package: `sudo pacman -S qrca`.

## Updating

The package follows the branch, so `makepkg -si` again picks up new commits.
