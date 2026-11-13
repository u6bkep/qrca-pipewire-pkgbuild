# Maintainer: Ben Kepner <u6bkep@gmail.com>
# Based on the Arch Linux qrca package by Antonio Rojas <arojas@archlinux.org>

pkgname=qrca-pipewire-git
_pkgname=qrca
pkgver=27.03.70.r1.g3923a9b
pkgrel=1
pkgdesc='QR code scanner, patched to capture cameras through PipeWire (libcamera/IPU3/IPU6 support)'
arch=(x86_64)
url='https://github.com/u6bkep/qrca/tree/work/pipewire-camera'
license=(GPL-2.0-or-later GPL-3.0-or-later)
depends=(glibc
         kconfig
         kcontacts
         kcoreaddons
         kcrash
         kdbusaddons
         ki18n
         kio
         kirigami
         kirigami-addons
         knotifications
         kservice
         libgcc
         libpipewire
         libstdc++
         networkmanager-qt
         prison
         purpose
         qt6-base
         qt6-declarative
         qt6-multimedia
         qt6-svg
         xdg-utils)
makedepends=(extra-cmake-modules
             git)
optdepends=('pipewire-libcamera: cameras that need libcamera, such as Intel IPU3/IPU6 sensors')
provides=(qrca)
conflicts=(qrca)
source=("$_pkgname::git+https://github.com/u6bkep/qrca.git#branch=work/pipewire-camera")
sha256sums=('SKIP')

pkgver() {
  cd $_pkgname
  # KDE tags releases on their own branches, so master has no tag to describe;
  # take the version from CMakeLists.txt and count commits instead.
  local _ver
  _ver=$(sed -n 's/^set *(RELEASE_SERVICE_VERSION_\(MAJOR\|MINOR\|MICRO\) *"\([0-9]*\)").*/\2/p' CMakeLists.txt | paste -sd.)
  printf '%s.r%s.g%s' "$_ver" "$(git rev-list --count HEAD ^origin/master 2>/dev/null || git rev-list --count HEAD)" "$(git rev-parse --short=7 HEAD)"
}

build() {
  cmake -B build -S $_pkgname \
    -DCMAKE_BUILD_TYPE=None \
    -DBUILD_TESTING=OFF
  cmake --build build
}

package() {
  DESTDIR="$pkgdir" cmake --install build
}
