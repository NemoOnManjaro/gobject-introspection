# Maintainer: Jan de Groot <jgc@archlinux.org>
pkgname=gobject-introspection
pkgver=0.10.3
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
sha256sums=('1d5fb9b094b170ff13d22886f60b148522432a654ddc832371bf94b89ec3840b')

build() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  PYTHON=/usr/bin/python2 ./configure --prefix=/usr --disable-static
  make
}

package() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  make DESTDIR="${pkgdir}" install

  sed -i "s|#!/usr/bin/env python|#!/usr/bin/env python2|" \
    "${pkgdir}"/usr/lib/gobject-introspection/giscanner/*.py
}
