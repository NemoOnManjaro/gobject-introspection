# Maintainer: Jan de Groot <jgc@archlinux.org>
pkgname=gobject-introspection
pkgver=0.10.5
pkgrel=1
pkgdesc="Introspection system for GObject-based libraries"
url="http://live.gnome.org/GObjectInstrospection"
arch=('x86_64' 'i686')
license=('LGPL' 'GPL')
depends=('libffi' 'glib2' 'python2')
makedepends=('cairo')
conflicts=('gir-repository')
replaces=('gir-repository')
options=('!libtool')
source=(http://ftp.gnome.org/pub/gnome/sources/${pkgname}/0.10/${pkgname}-${pkgver}.tar.bz2)
sha256sums=('fe033c5c89fb8a6019bbb15ad1d30e8e99280bf274b2e269f00faaf8a8f58325')

build() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  PYTHON=/usr/bin/python2 ./configure --prefix=/usr --disable-static
  make
}

package() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  make DESTDIR="${pkgdir}" install

  sed -i '1s|#!/usr/bin/env python$|&2|' \
    "${pkgdir}"/usr/lib/gobject-introspection/giscanner/*.py
}
