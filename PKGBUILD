# Maintainer: Tim Seckinger <seckinger.tim@gmail.com>

pkgname=libinput-direct-abs-input
pkgver=1.20.0.aedbb861
pkgrel=1
pkgdesc="Input device management and event handling library"
url="https://github.com/jeysal/libinput-direct-abs-input"
arch=(x86_64)
license=(custom:MIT)
provides=(libinput)
conflicts=(libinput)
depends=('mtdev' 'systemd' 'libevdev' 'libwacom')
# upstream doesn't recommend building docs
makedepends=('gtk4' 'meson' 'wayland-protocols') # 'doxygen' 'graphviz' 'python-sphinx' 'python-recommonmark'
optdepends=('gtk4: libinput debug-gui'
            'python-pyudev: libinput measure'
            'python-libevdev: libinput measure')
source=(#https://freedesktop.org/software/$pkgname/$pkgname-$pkgver.tar.xz{,.sig}
        #https://gitlab.freedesktop.org/libinput/libinput/-/archive/$pkgver/$pkgname-$pkgver.tar.bz2 #{,.sig}.tar.bz2
        "$pkgname-$pkgver"::"git+https://github.com/jeysal/libinput-direct-abs-input#commit=aedbb861"
)
sha512sums=(#'f4b776d0da78c687ba21b430a04941ac6b43f68970c82ec9f7360358fdea5ed6a873948ce66a25bcdd64d4b95fa4bf705cc24dbc25c7c0f5fd2d0efbd763f298'
            'SKIP')
# sha512sums=('145b0e0760929137ab442b2030b4b42f6df54a3ae61c47c929e1a74857a170f0f2a56bb7522b7d1d9c0943028ac54c7728cf8d66a0c384f6118f31d6625ab44c')
#validpgpkeys=('3C2C43D9447D5938EF4551EBE23B7E70B467F0BF') # Peter Hutterer (Who-T) <office@who-t.net>

build() {
  arch-meson $pkgname-$pkgver build \
    -D udev-dir=/usr/lib/udev \
    -D tests=false \
    -D documentation=false

  # Print config
  meson configure build
  meson compile -C build
}

package() {
  DESTDIR="$pkgdir" meson install -C build

  install -Dvm644 $pkgname-$pkgver/COPYING \
    "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
