# $Id: PKGBUILD 58000 2009-11-03 08:17:51Z giovanni $
# Maintainer: James Rayner <iphitus@gmail.com>

pkgname=nppangband
pkgver=0.5.0.25
pkgrel=1.1
pkgdesc="A variant of Angband that attempts to take popular ideas from other variants"
url="http://www.assembla.com/wiki/show/NPPAngband"
depends=('ncurses' 'libx11')
makedepends=('libxaw' 'xorg-font-utils')
source=(http://www.assembla.com/spaces/NPPAngband/documents/dmfeFgWJir3PuseJe5afGb/download/npp050-rev25-src.zip)
license=('custom')
arch=('i686' 'x86_64')

build() {

  cd $srcdir/npp050-rev25-src/src
  sed 's@# define DEFAULT_PATH "./lib/"@# define DEFAULT_PATH "/usr/share/nppangband/"@' -i config.h
  sed -i 's/-D"USE_LFB"//g' Makefile.std # Remove framebuffer support, does not compile, 
  make -f Makefile.std


  # Fix fonts
  cd ../lib/xtra/font/
  tr -d '\r' < compile_bdf_fonts.sh > compile_bdf_fonts2.sh # Convert line endings dos->unix
  sed -i "s/\.bdf/\.bdf;/g" compile_bdf_fonts2.sh # fix syntax error, missing ;.
  bash compile_bdf_fonts2.sh # no shebang, use bash explicitly

  # Install
  cd $srcdir/npp050-rev25-src/
  mkdir -p $pkgdir/usr/bin $pkgdir/usr/share
  cp -R lib $pkgdir/usr/share/nppangband/
  chmod -R 775 $pkgdir/usr/share/nppangband/    
  chown -R root:games $pkgdir/usr/share/nppangband/
  install -m755 src/nppangband $pkgdir/usr/bin/nppangband

  # install custom license
  install -Dm644 COPYING $pkgdir/usr/share/licenses/$pkgname/COPYING
}

md5sums=('776d387ccbca31edf7eb30eb1402b0c9')
