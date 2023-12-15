# Maintainer:
# Contributor: kj_sh604 <43.splash@gmail.com>

pkgname=agave
pkgver=0.4.7
pkgrel=604
pkgdesc="Colorscheme designer tool for GNOME"
arch=('x86_64')
url="https://web.archive.org/web/20170327063642/http://home.gna.org/colorscheme/"
license=('GPL')
depends=('libglademm')
makedepends=('gnome-doc-utils' 'intltool' 'boost')

# use this source when PKGBUILD breaks in the future:
# source=(https://aedrielkylejavier.me/assets/$pkgname/${pkgname}_$pkgver.orig.tar.gz

source=(http://archive.ubuntu.com/ubuntu/pool/universe/a/$pkgname/${pkgname}_$pkgver.orig.tar.gz
        agave-0.4.7-mdv-fix-str-fmt.patch
        schemebox.patch
        drop-libgnome.patch
        fix-build-without-gconf.patch)

prepare() {
  cd $pkgname-$pkgver

  # Build fix from Fedora
  patch -Np1 -i ../agave-0.4.7-mdv-fix-str-fmt.patch

  # Another build fix
  patch -Np1 -i ../schemebox.patch

  # Remove deprecated libgnome dependency
  patch -Np1 -i ../drop-libgnome.patch

  # Fix build without gconfmm installed
  patch -Np1 -i ../fix-build-without-gconf.patch
}

build() {
  cd $pkgname-$pkgver
  CXXFLAGS+=' -std=c++11'
  ./configure --prefix=/usr --sysconfdir=/etc --localstatedir=/var \
              --disable-scrollkeeper --disable-gnome --disable-gconf
  make
}

package() {
  cd $pkgname-$pkgver
  make DESTDIR="$pkgdir" install
  rm "$pkgdir/agave.schemas"
}
