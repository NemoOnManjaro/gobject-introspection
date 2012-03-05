# Maintainer: Jan de Groot <jgc@archlinux.org>

pkgname=gobject-introspection
pkgver=1.31.20
pkgrel=1
pkgdesc="Introspection system for GObject-based libraries"
url="http://live.gnome.org/GObjectInstrospection"
arch=('x86_64' 'i686')
license=('LGPL' 'GPL')
depends=('glib2' 'python2')
makedepends=('cairo')
options=('!libtool')
source=(http://ftp.gnome.org/pub/gnome/sources/$pkgname/${pkgver%.*}/$pkgname-$pkgver.tar.xz)
sha256sums=('e1552884b642e7e5a56a175ae85bfdebfd16c29a7bbe4f6ca9cdf591e333f070')

build() {
  cd "$srcdir/$pkgname-$pkgver"
  PYTHON=/usr/bin/python2 ./configure --prefix=/usr --disable-static
  make
}

package() {
  cd "$srcdir/$pkgname-$pkgver"
  make DESTDIR="$pkgdir" install

  sed -i '1s|#!/usr/bin/env python$|&2|' \
    "$pkgdir"/usr/lib/gobject-introspection/giscanner/*.py
}
