pkgname=st
pkgver=0.7
pkgrel=1
pkgdesc='A simple virtual terminal emulator for X.'
arch=('i686' 'x86_64')
license=('MIT')
depends=('libxft' 'libxext')
makedepends=('ncurses')
url="http://st.suckless.org"

source=(http://dl.suckless.org/st/$pkgname-$pkgver.tar.gz
        http://st.suckless.org/patches/solarized/st-no_bold_colors-$pkgver.diff
        http://st.suckless.org/patches/solarized/st-solarized-dark-$pkgver.diff
        http://st.suckless.org/patches/scrollback/st-scrollback-$pkgver.diff
        config.h)

md5sums=('SKIP'
         'SKIP'
         'SKIP'
         'SKIP'
         'SKIP')

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
