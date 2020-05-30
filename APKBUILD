# Based on https://aur.archlinux.org/packages/boringssl-git/
# Maintainer: Omar Roth <omarroth@protonmail.com>
pkgname=boringssl
pkgver=1.1.0
pkgrel=0
pkgdesc="BoringSSL is a fork of OpenSSL that is designed to meet Google's needs"
url="https://boringssl.googlesource.com/boringssl"
arch="all"
license="MIT"
replaces="openssl libressl"
depends="!openssl-libs-static"
makedepends_host="linux-headers"
makedepends="cmake git go perl"
subpackages="$pkgname-static $pkgname-dev $pkgname-doc"
source="bfe527f.tar.gz::https://github.com/google/boringssl/tarball/bfe527f"
builddir="$srcdir/google-boringssl-bfe527f"

prepare() {
	:
}

build() {
	cmake -DCMAKE_BUILD_TYPE=Release .
	make ssl crypto
}

check() {
	make all_tests
}

package() {
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
sha512sums="2c3a7029b4ba55146e2d911c90fdf805b10b9def594154f0567dd3003f415b56fec59d5d824ed5d616c3da9dba7d32aa52605d1a6901bdf5c087860bc009e3a4  bfe527f.tar.gz"
