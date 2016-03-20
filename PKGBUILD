# Maintainer: Jan de Groot <jgc@archlinux.org>

pkgbase=gobject-introspection
pkgname=('gobject-introspection' 'gobject-introspection-runtime')
pkgdesc="Introspection system for GObject-based libraries"
pkgver=1.47.92
pkgrel=2
url="https://live.gnome.org/GObjectIntrospection"
arch=('x86_64' 'i686')
license=('LGPL' 'GPL')
depends=('python' 'python-mako')
makedepends=('cairo')
options=('!emptydirs')
source=(https://download.gnome.org/sources/$pkgbase/${pkgver:0:4}/$pkgbase-$pkgver.tar.xz)
sha256sums=('c8ced38348e436222fda5e0abdc31022e8017d8732fe69da5c92285a37766ac8')

prepare() {
  cd $pkgbase-$pkgver
}

build() {
  cd $pkgbase-$pkgver
  ./configure --prefix=/usr --disable-static --enable-doctool
  make
}

package_gobject-introspection-runtime() {
  pkgdesc+=" - runtime files"
  depends=('glib2')
  cd $pkgbase-$pkgver
  make DESTDIR="$pkgdir" install-libLTLIBRARIES install-typelibsDATA
}

package_gobject-introspection() {
  depends+=("gobject-introspection-runtime=$pkgver")

  cd $pkgbase-$pkgver
  make DESTDIR="$pkgdir" install
  make DESTDIR="$pkgdir" uninstall-libLTLIBRARIES uninstall-typelibsDATA
}
