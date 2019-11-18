# Based on https://aur.archlinux.org/packages/boringssl-git/
# Maintainer: Omar Roth <omarroth@protonmail.com>
pkgname="boringssl"
pkgver="1.1.0"
pkgrel=0
pkgdesc="BoringSSL is a fork of OpenSSL that is designed to meet Google's needs"
url="https://boringssl.googlesource.com/boringssl"
arch="all"
license="MIT"
depends=""
makedepends="cmake git go perl"
install=""
subpackages="$pkgname-dev $pkgname-doc"
source="https://boringssl.googlesource.com/boringssl/+archive/fips-android-20191020.tar.gz"
builddir="$srcdir/"

prepare() {
	cd "$builddir"
	cmake -DCMAKE_BUILD_TYPE=Release .
}

build() {
	cd "$builddir"
	make ssl crypto
}

check() {
	cd "$builddir"
#	make all_tests
}

package() {
	cd "$builddir"
	install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
	for i in *.md ; do
		install -Dm644 $i "$pkgdir/usr/share/doc/$pkgname/$i"
	done
	install -d "$pkgdir/usr/lib"
	install -d "$pkgdir/usr/include"
	cp -R include/openssl "$pkgdir/usr/include"

	install -Dm755 crypto/libcrypto.a "$pkgdir/usr/lib/libcrypto.a"
	install -Dm755 ssl/libssl.a "$pkgdir/usr/lib/libssl.a"
#	install -Dm755 decrepit/libdecrepit.a "$pkgdir/usr/lib/libdecrepit.a"
#	install -Dm755 libboringssl_gtest.a "$pkgdir/usr/lib/libboringssl_gtest.a"
}
sha512sums="9aa30d740bf46ba05c7b2277fb87e3a9c40cf09dc8c5a034c68c56e28ff8e0cbf5fb84151615ed334d1179408eea89230084c4da3c94bdd115c9f2cc746fd03f  fips-android-20191020.tar.gz"
