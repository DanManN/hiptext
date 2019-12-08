# Maintainer: Max Zhao < alcasa dot mz at gmail dot com >
# Contributor: Konstantin Gizdov < arch at kge dot pw >
# Contributor: Daniel Nakhimovich < dnahimov at gmail dot com >

pkgname=hiptext
pkgver=0.2
pkgrel=2
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
        'hiptext.sh'
        'freetype_config.patch'
        'build_with_latest_ffmpeg.patch'
        'gflags_namespace.patch'
        'video_flicker.patch'
        'add_gif_extension.patch')
sha256sums=('7f2217dec8775b445be6745f7bd439c24ce99c4316a9faf657bee7b42bc72e8f'
            'bd97c23995f372326d8d2b0b70591b595e169dbd0006317c299bfd6f44df43dc'
            '9d3e5801a92ddd4bd278f3d515cf16d7d969f2c319bb05559ccf5299c37fbebe'
            '59482f694811569d08596c07c2461ad9adb6c74c500b6a8755889a78eb27f4b1'
            'ba251b4847be9f45192b60605d6211254f46c310909f706ce91eb9ff9d4f4e15'
            'c9ddd3e4266a4f6fd0b92bf1c23d7bb5bf6ec150dfa67c76b5f17df6a92a3d49'
            '7f0ac14122bcf0c22c0ca2859f54746c95663782b2d1a2a47cfd477a72841ae4')

prepare() {
    cd "$pkgname-$pkgver"
    msg2 'Applying patches...'
    patch -p1 -i "$srcdir/build_with_latest_ffmpeg.patch"
    patch -p1 -i "$srcdir/video_flicker.patch"
    patch -p1 -i "$srcdir/freetype_config.patch"
    patch -p1 -i "$srcdir/add_gif_extension.patch"
    # patch -p1 -i "$srcdir/gflags_namespace.patch"  # optional
    msg2 'Running Autogen... '
    ./autogen.sh || ./autogen.sh
    msg2 'Configuring...'
     ./configure --prefix=/usr             \
                 --includedir=/usr/include \
                 --libdir=/usr/lib         \
                 --datarootdir=/usr/share  \
                 --sysconfdir=/etc         \
                 --localstatedir=/var      \
                 --sharedstatedir=/com     \
    #             LIBGFLAGS_LIBS="-lgflags" \
    #             LIBGFLAGS_CFLAGS="-lgflags"
}

build() {
    cd "$pkgname-$pkgver"
    msg2 'Building...'
    make
}

package() {
    cd "$pkgname-$pkgver"
    msg2 'Installing...'
    make DESTDIR="$pkgdir/usr/share/$pkgname" install
    install -d "$pkgdir/usr/share/$pkgname/fonts"
    install -Dm644 "$srcdir/$pkgname-$pkgver/DejaVuSansMono.ttf" \
                   "$pkgdir/usr/share/hiptext/fonts/DejaVuSansMono.ttf"
    install -Dm755 "$srcdir/hiptext.sh" "$pkgdir/usr/bin/hiptext"
}
