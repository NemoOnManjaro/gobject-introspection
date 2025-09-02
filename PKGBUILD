# Maintainer: Jan Alexander Steffens (heftig) <heftig@archlinux.org>
# Maintainer: Fabian Bornschein <fabiscafe@archlinux.org>
# Contributor: Jan de Groot <jgc@archlinux.org>

pkgbase=gobject-introspection
pkgname=(
  gobject-introspection
  gobject-introspection-runtime
  libgirepository
)
pkgver=1.82.0
pkgrel=3
pkgdesc="Introspection system for GObject-based libraries"
url="https://wiki.gnome.org/Projects/GObjectIntrospection"
arch=(x86_64)
license=(
  GPL-2.0-or-later
  LGPL-2.0-or-later
)
_glibver=2.82.4
makedepends=(
  "glib2=$_glibver"
  cairo
  git
  glibc
  gtk-doc
  libffi
  libffi
  meson
  python
  python-mako
  python-markdown
  python-setuptools
  python-sphinx
)
source=(
  "https://github.com/GNOME/gobject-introspection/archive/refs/tags/$pkgver.tar.gz"
  "https://github.com/GNOME/glib/archive/refs/tags/$_glibver.tar.gz"
  "https://github.com/GNOME/gobject-introspection-tests/archive/refs/heads/main.tar.gz"
  0001-scanner-Ignore-_Complex.patch
)
b2sums=('SKIP'
        'SKIP'
        'SKIP'
        '1948e5122c99526052eb5b121f2eca1e72f476fce2907001097f7ac805fe64d39c667ede801991193d017840f4102fdeb973fe5f113ac31196d6a6131d439a79')
validpgpkeys=(
  923B7025EE03C1C59F42684CF0942E894B2EAFA0  # Philip Withnall <philip@tecnocode.co.uk>
  D4C501DA48EB797A081750939449C2F50996635F  # Marco Trevisan <marco@trevi.me>
)

prepare() {
  cd $pkgbase-$pkgver
  cp -r ../gobject-introspection-tests-main/* gobject-introspection-tests/
  # Unbreak WebKitGTK build
  # https://gitlab.gnome.org/GNOME/gobject-introspection/-/issues/519
  patch -p1 --input="${srcdir}/0001-scanner-Ignore-_Complex.patch"

#  git submodule init
#  git submodule set-url gobject-introspection-tests "$srcdir/gobject-introspection-tests"
#  git -c protocol.file.allow=always -c protocol.allow=never submodule update
}

build() {
  local meson_options=(
    -D glib_src_dir="$srcdir/glib-$_glibver"
    -D gtk_doc=true
  )

  arch-meson $pkgbase-$pkgver build "${meson_options[@]}"
  meson compile -C build
}

_pick() {
  local p="$1" f d; shift
  for f; do
    d="$srcdir/$p/${f#$pkgdir/}"
    mkdir -p "$(dirname "$d")"
    mv "$f" "$d"
    rmdir -p --ignore-fail-on-non-empty "$(dirname "$f")"
  done
}

package_gobject-introspection() {
  depends=(
    "gobject-introspection-runtime=$pkgver-$pkgrel"
    "libgirepository=$pkgver-$pkgrel"
    glib2
    glibc
    libffi
    python
    python-mako
    python-markdown
    python-setuptools
  )

  meson install -C build --destdir "$pkgdir"

  cd "$pkgdir"

  python -m compileall -d /usr/lib/$pkgbase usr/lib/$pkgbase
  python -O -m compileall -d /usr/lib/$pkgbase usr/lib/$pkgbase

  _pick libg usr/include/gobject-introspection-1.0
  _pick libg usr/lib/libgirepository-1.0.so*
  _pick libg usr/lib/pkgconfig/gobject-introspection*-1.0.pc
  _pick libg usr/lib/girepository-1.0/GIRepository-2.0.typelib
  _pick libg usr/share/gir-1.0/GIRepository-2.0.gir
  _pick libg usr/share/gtk-doc

  _pick runtime usr/lib/girepository-1.0
}

package_gobject-introspection-runtime() {
  pkgdesc+=" - runtime"
  depends=("libgirepository=$pkgver-$pkgrel")

  mv runtime/* "$pkgdir"
}

package_libgirepository() {
  pkgdesc+=" - runtime library"
  depends=(
    glib2
    glibc
    libffi
    libffi.so
    libg{lib,object,module}-2.0.so
  )
  provides=(libgirepository-1.0.so)

  mv libg/* "$pkgdir"
}

# vim:set sw=2 sts=-1 et:
