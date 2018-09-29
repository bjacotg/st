# Maintainer: Bastien Jacot-Guillarmod bjacotg@gmail.com
pkgname=st
pkgver=0.7
pkgrel=2
pkgdesc='A simple virtual terminal emulator for X.'
arch=('i686' 'x86_64')
license=('MIT')
depends=('libxft')
makedepends=('ncurses', 'powerline-fonts')
url="http://st.suckless.org"

source=(http://dl.suckless.org/st/$pkgname-$pkgver.tar.gz
        http://st.suckless.org/patches/solarized/st-no_bold_colors-$pkgver.diff
        http://st.suckless.org/patches/solarized/st-solarized-dark-$pkgver.diff
        config.h)

sha256sums=('f7870d906ccc988926eef2cc98950a99cc78725b685e934c422c03c1234e6000'
            '2e8cdbeaaa79ed067ffcfdcf4c5f09fb5c8c984906cde97226d4dd219dda39dc'
            '4782f52c4147a352579586c1b066f9fd1da934e580cbd3b78943f058394d9883'
            'd53183d8fea8f266aa96a88d6cab5245cf80d76ecbd79489729a064d96a51512')

prepare() {
  cd "$srcdir"/$pkgname-$pkgver
  sed -i '/\@tic /d' Makefile
  cp "$srcdir"/config.h config.h
}

build() {
  cd "$srcdir"/$pkgname-$pkgver
  patch -i "$srcdir/st-no_bold_colors-$pkgver.diff"
  patch -i "$srcdir/st-solarized-dark-$pkgver.diff"
  make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11
}

package() {
  cd "$srcdir"/$pkgname-$pkgver
  make PREFIX=/usr DESTDIR="$pkgdir" TERMINFO="$pkgdir/usr/share/terminfo" install
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  install -Dm644 README "$pkgdir/usr/share/doc/$pkgname/README"
}
