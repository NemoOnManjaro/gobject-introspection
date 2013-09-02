# Maintainer: Jan de Groot <jgc@archlinux.org>

pkgname=gobject-introspection
pkgver=1.37.6
pkgrel=1
pkgdesc="Introspection system for GObject-based libraries"
url="https://live.gnome.org/GObjectIntrospection"
arch=('x86_64' 'i686')
license=('LGPL' 'GPL')
depends=('glib2' 'python2' 'python2-mako')
makedepends=('cairo')
options=('!libtool')
source=(http://ftp.gnome.org/pub/gnome/sources/$pkgname/${pkgver::4}/$pkgname-$pkgver.tar.xz)
sha256sums=('6eebb4f6981be2f41dba184f27319d6448a9144b417b5bdf7e579c8ea0a340cf')

build() {
  cd "$pkgname-$pkgver"
  PYTHON=/usr/bin/python2 ./configure --prefix=/usr --disable-static --enable-doctool
  make
}

package() {
  cd "$pkgname-$pkgver"
  make DESTDIR="$pkgdir" install

  sed -i '1s|#!/usr/bin/env python$|&2|' \
    "$pkgdir"/usr/lib/gobject-introspection/giscanner/*.py
}
