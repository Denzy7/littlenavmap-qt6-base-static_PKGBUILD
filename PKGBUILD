# Maintainer: Dennis Maina <dennismyner7@gmail.com>
pkgname=littlenavmap-qt6-base-static
pkgver=6.12.0
pkgrel=1
pkgdesc="Static, self-contained QtCore (qtbase) for building the Little Xpconnect X-Plane plugin"
arch=(x86_64)
url="https://www.qt.io"
license=('LGPL-3.0-only OR GPL-2.0-only OR GPL-3.0-only')
makedepends=(cmake ninja perl python)
# static archives go into a .so plugin: keep the .a files, no LTO bytecode
options=(staticlibs !lto !debug)
_pkgfn=qtbase-everywhere-src-$pkgver
_prefix=/opt/$pkgname
source=("https://download.qt.io/official_releases/qt/${pkgver%.*}/$pkgver/submodules/$_pkgfn.tar.xz")
sha256sums=('a951bd163c7b80fc6b8c88d7668fb56abf91c152373e13c10666763238131307')

build() {
    # mirrors upstream build/linux/build_qt_static.sh, but every auto-detected
    # external library is disabled or bundled so the plugin linked against
    # this Qt only NEEDs libc/libm/libgcc_s (like the old Qt 5 lin.xpl)
    cmake -S $_pkgfn -B build -G Ninja \
        -DCMAKE_BUILD_TYPE=Release \
        -DCMAKE_INSTALL_PREFIX=$_prefix \
        -DCMAKE_POSITION_INDEPENDENT_CODE=ON \
        -DBUILD_SHARED_LIBS=OFF \
        -DQT_BUILD_EXAMPLES=OFF \
        -DQT_BUILD_TESTS=OFF \
        -DFEATURE_testlib=OFF \
        -DFEATURE_androiddeployqt=OFF \
        -DFEATURE_reduce_exports=ON \
        -DFEATURE_gui=OFF \
        -DFEATURE_dbus=OFF \
        -DFEATURE_system_pcre2=OFF \
        -DFEATURE_system_zlib=OFF \
        -DFEATURE_system_sqlite=OFF \
        -DFEATURE_sql_db2=OFF \
        -DFEATURE_sql_ibase=OFF \
        -DFEATURE_sql_mimer=OFF \
        -DFEATURE_sql_mysql=OFF \
        -DFEATURE_sql_oci=OFF \
        -DFEATURE_sql_odbc=OFF \
        -DFEATURE_sql_psql=OFF \
        -DFEATURE_system_doubleconversion=OFF \
        -DFEATURE_system_libb2=OFF \
        -DFEATURE_openssl=OFF \
        -DFEATURE_icu=OFF \
        -DFEATURE_glib=OFF \
        -DFEATURE_zstd=OFF \
        -DFEATURE_jemalloc=OFF \
        -DFEATURE_liburing=OFF \
        -DFEATURE_journald=OFF \
        -DFEATURE_libudev=OFF \
        -DFEATURE_libproxy=OFF \
        -DFEATURE_gssapi=OFF \
        -DFEATURE_brotli=OFF
    cmake --build build
}

package() {
    DESTDIR="$pkgdir" cmake --install build
    install -d "$pkgdir/usr/share/licenses/$pkgname"
    cp -r $_pkgfn/LICENSES/. "$pkgdir/usr/share/licenses/$pkgname/"
}
