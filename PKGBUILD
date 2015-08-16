pkgname=mingw32-gettext
pkgver=0.18.1.1
pkgrel=8
arch=(any)
pkgdesc="GNU internationalization library (mingw32)"
depends=(mingw32-runtime mingw32-libiconv)
makedepends=(mingw32-gcc)
options=(!strip !buildflags !libtool)
conflicts=(mingw32-gettext-static)
provides=(mingw32-gettext-static)
license=(GPL LGPL)
url="http://www.gnu.org/software/gettext/"
source=("http://ftp.gnu.org/pub/gnu/gettext/gettext-$pkgver.tar.gz"
"00-reloc-gettext-$pkgver.patch"
"01-reloc-gettext-$pkgver.patch"
"02-locale-gettext-$pkgver.patch"
"03-cygwin-gettext-$pkgver.patch"
"gettext-$pkgver-2.src.patch")
md5sums=('3dd55b952826d2b32f51308f2f91aa89'
         '986e89226388137fc98b51fff76c4626'
         'e3a1d4090e5b445a73694fdfb2b03de3'
         '6074fc0c4ee44df5cc4baab753a31b49'
         'a05ebe6a962cddf05d7d6a6d6c12d264'
         '2d807502f0d5717b937766d174f35654')

build()
{
  cd "$srcdir/gettext-$pkgver"
  
  patch -p2 -i ../00-reloc-gettext-$pkgver.patch
  patch -p2 -i ../01-reloc-gettext-$pkgver.patch
  patch -p2 -i ../02-locale-gettext-$pkgver.patch
  patch -p2 -i ../03-cygwin-gettext-$pkgver.patch
  patch -p2 -i ../gettext-$pkgver-2.src.patch
  
  cd "gettext-runtime"
  unset LDFLAGS
  export CFLAGS="$CFLAGS -mms-bitfields"
  mkdir -p build && cd build
  ../configure \
    --prefix=/usr/i486-mingw32 \
    --host=i486-mingw32 \
    --enable-shared \
    --enable-static \
    --enable-threads=win32
  make
}

package() {
  cd "$srcdir/gettext-$pkgver/gettext-runtime/build"
  make DESTDIR=$pkgdir install

  i486-mingw32-strip $pkgdir/usr/i486-mingw32/bin/*.exe
  i486-mingw32-strip -x -g $pkgdir/usr/i486-mingw32/bin/*.dll
  i486-mingw32-strip -g $pkgdir/usr/i486-mingw32/lib/*.a
  rm -rf "$pkgdir/usr/i486-mingw32/share"
}
