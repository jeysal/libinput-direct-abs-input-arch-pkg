# Maintainer: Tim Seckinger <seckinger.tim@gmail.com>

pkgname=libinput-direct-abs-input
pkgver=1.21.0.25fa250
pkgrel=1
pkgdesc="Input device management and event handling library"
url="https://github.com/jeysal/libinput-direct-abs-input"
arch=(x86_64)
license=(custom:X11)
provides=(libinput)
conflicts=(libinput)
depends=('mtdev' 'systemd' 'libevdev' 'libwacom')
# upstream doesn't recommend building docs
makedepends=('gtk4' 'meson' 'wayland-protocols' 'check') # 'doxygen' 'graphviz' 'python-sphinx' 'python-recommonmark'
optdepends=('gtk4: libinput debug-gui'
            'python-pyudev: libinput measure'
            'python-libevdev: libinput measure')
options=(debug)
source=(#https://gitlab.freedesktop.org/libinput/libinput/-/archive/$pkgver/$pkgname-$pkgver.tar.bz2)
        "$pkgname-$pkgver"::"git+https://github.com/jeysal/libinput-direct-abs-input#commit=25fa250"
        )
sha256sums=(#'3173d83e0f5a686606d2780129c802b865b6a0750c86db88d56097afc016a2dd')
            'SKIP')
#validpgpkeys=('3C2C43D9447D5938EF4551EBE23B7E70B467F0BF') # Peter Hutterer (Who-T) <office@who-t.net>

build() {
  arch-meson $pkgname-$pkgver build \
    -D udev-dir=/usr/lib/udev \
    -D documentation=false

  # Print config
  meson configure build

  meson compile -C build
}

check() {
  meson test -C build --print-errorlogs
}

package() {
  meson install -C build --destdir "$pkgdir"

  install -Dvm644 $pkgname-$pkgver/COPYING \
    "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
