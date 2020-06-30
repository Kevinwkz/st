# Maintainer:

pkgname=st-kevinwkz-git
_pkgname=st
pkgver=0.8.4
pkgrel=1
epoch=1
pkgdesc="Kevin's fork of suckless's terminal emulator (st) with some patches"
url='https://github.com/Kevinwkz/st'
arch=('x86_64')
license=('MIT')
options=('zipman')
depends=('libxft')
makedepends=('ncurses' 'libxft-bgra' 'git')
optdepends=('dmenu: feed urls to dmenu')
source=('git://github.com/Kevinwkz/st')
sha1sums=('SKIP')

provides=("${_pkgname}")
conflicts=("${_pkgname}")

pkgver() {
    cd "${_pkgname}"
    printf "%s.r%s.%s" "$(awk '/^VERSION =/ {print $3}' config.mk)" \
        "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

prepare() {
    cd $srcdir/${_pkgname}
    # skip terminfo which conflicts with ncurses
    sed -i '/tic /d' Makefile
}

build() {
    cd "${_pkgname}"
    make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11
}

package() {
    cd "${_pkgname}"
    make PREFIX=/usr DESTDIR="${pkgdir}" install
    install -Dm644 LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
    install -Dm644 README.md "${pkgdir}/usr/share/doc/${pkgname}/README.md"
    #install -Dm644 .Xdefaults "${pkgdir}/usr/share/doc/${pkgname}/Xdefaults.example"
}
