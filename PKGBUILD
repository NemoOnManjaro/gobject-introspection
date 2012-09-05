# Maintainer: Jan de Groot <jgc@archlinux.org>

pkgname=gobject-introspection
pkgver=1.33.10
pkgrel=1
pkgdesc="Introspection system for GObject-based libraries"
url="https://live.gnome.org/GObjectIntrospection"
arch=('x86_64' 'i686')
license=('LGPL' 'GPL')
depends=('glib2' 'python2')
makedepends=('cairo')
options=('!libtool')
source=(http://ftp.gnome.org/pub/gnome/sources/$pkgname/${pkgver%.*}/$pkgname-$pkgver.tar.xz)
sha256sums=('b000d5a6edeeff11040e07a733b31725feffdc9ff73a10862ede911c868ffdd7')

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
