# Maintainer: Tianjiao Yin <ytj000@gmail.com>

pkgname=waf-docs
pkgver=1.7.9
pkgrel=1
pkgdesc="Documentation for Waf, a general-purpose build system modelled after Scons"
url="http://code.google.com/p/waf/"
arch=('any')
license=("BSD")
makedepends=("python2-sphinx" "texlive-latexextra" "asciidoc" 
             "dia" "imagemagick" "source-highlight"
             "dblatex" "waf" "graphviz<=2.28.0")
source=("https://waf.googlecode.com/files/waf-$pkgver.tar.bz2"
        "collapsiblesidebar.patch")
md5sums=('0f5a3ecf23e80a42324dac9415de09fb'
         'd6f863bbae3df76e26b7aa9267259d04')

build() {

  # Part 1, build waf documentation
  ###########################################################################

  cd "$srcdir/waf-$pkgver/docs/sphinx"
  sed -i "s/sphinx-build/sphinx-build2/g" Makefile
  patch conf.py $srcdir/collapsiblesidebar.patch

  make html
  make latex
  make -C build/latex
  mv build/latex/waf.pdf build
  rm build/latex -rf

  # Part 2, build waf book
  ###########################################################################

  cd "$srcdir/waf-$pkgver/docs/book"
  waf configure
  waf
}

package() {
  cd "$srcdir/waf-$pkgver/docs/sphinx"

  rm build/doctrees -rf
  mkdir -p $pkgdir/usr/share/doc/
  mv build $pkgdir/usr/share/doc/waf
  mv $srcdir/waf-$pkgver/docs/book/build $pkgdir/usr/share/doc/waf/book

  mkdir -p $pkgdir/usr/share/doc/waf/bookpdf
  mv $pkgdir/usr/share/doc/waf/book/*.pdf $pkgdir/usr/share/doc/waf/bookpdf
}

# vim:set ts=2 sw=2 et:
