# Maintainer: Jan de Groot <jgc@archlinux.org>

pkgname=gobject-introspection
pkgver=1.33.9
pkgrel=1
pkgdesc="Introspection system for GObject-based libraries"
url="https://live.gnome.org/GObjectIntrospection"
arch=('x86_64' 'i686')
license=('LGPL' 'GPL')
depends=('glib2' 'python2')
makedepends=('cairo')
options=('!libtool')
source=(http://ftp.gnome.org/pub/gnome/sources/$pkgname/${pkgver%.*}/$pkgname-$pkgver.tar.xz)
sha256sums=('4d8283bcbf30f78e13e2d085a8be9a41a8b197a22ad48dc913e6ea7bec3fe8b0')

build() {
  cd "$pkgname-$pkgver"
  PYTHON=/usr/bin/python2 ./configure --prefix=/usr --disable-static
  make
}

package() {
  cd "$pkgname-$pkgver"
  make DESTDIR="$pkgdir" install

  sed -i '1s|#!/usr/bin/env python$|&2|' \
    "$pkgdir"/usr/lib/gobject-introspection/giscanner/*.py
}
