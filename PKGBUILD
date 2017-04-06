# Maintainer: Max Zhao < alcasa dot mz at gmail dot com >
# Contributor: Konstantin Gizdov < arch at kge dot pw >

pkgname=hiptext
pkgver=0.2
pkgrel=1
pkgdesc="Command line tool for rendering images and videos inside terminals."
arch=('any')
url="https://github.com/jart/hiptext"
license=('GPL')
depends=('gflags'
         'google-glog')
makedepends=('ffmpeg'
             'freetype2'
             'giflib'
             'libjpeg-turbo'
             'libpng12'
             'ragel')
source=("https://github.com/jart/$pkgname/releases/download/$pkgver/$pkgname-$pkgver.tar.gz"
        'build_with_latest_ffmpeg.patch')
sha256sums=('7f2217dec8775b445be6745f7bd439c24ce99c4316a9faf657bee7b42bc72e8f'
            '59482f694811569d08596c07c2461ad9adb6c74c500b6a8755889a78eb27f4b1')

prepare() {
	cd "$pkgname-$pkgver"
	patch -p1 -i "$srcdir/build_with_latest_ffmpeg.patch"
        ./configure --prefix=/usr             \
                    --includedir=/usr/include \
                    --libdir=/usr/lib         \
                    --datarootdir=/usr/share  \
                    --sysconfdir=/etc         \
                    --localstatedir=/var      \
                    --sharedstatedir=/com     \
                    LIBGFLAGS_LIBS="-lgflags" \
                    LIBGFLAGS_CFLAGS="-lgflags"
}

build() {
	cd "$pkgname-$pkgver"
	make
}

package() {
	cd "$pkgname-$pkgver"
	make DESTDIR="$pkgdir" install
}
