# Contributor: Sasha Gerrand <alpine-pkgs@sgerrand.com>
# Maintainer: Sasha Gerrand <alpine-pkgs@sgerrand.com>
pkgname=stout
pkgver=0.1.0
pkgrel=0
pkgdesc="A C++ library for building sturdy software."
url="https://github.com/3rdparty/stout"
arch="all"
license="Apache-2.0"
depends=""
depends_dev="boost-dev gtest-dev protobuf-dev"
makedepends="$depends_dev autoconf automake gcc libtool"
install=""
subpackages="$pkgname-dev $pkgname-doc"
source="stout-0.1.0.tar.gz::https://github.com/3rdparty/stout/archive/master.tar.gz"

_builddir="$srcdir/$pkgname-master"
prepare() {
	local i
	cd "$_builddir"
	./bootstrap
	for i in $source; do
		case $i in
		*.patch) msg $i; patch -p1 -i "$srcdir"/$i || return 1;;
		esac
	done
}

build() {
	cd "$_builddir"
	./configure \
		--build=$CBUILD \
		--host=$CHOST \
		--prefix=/usr \
		--sysconfdir=/etc \
		--mandir=/usr/share/man \
		--localstatedir=/var \
		|| return 1
	make || return 1
}

package() {
	cd "$_builddir"
	mkdir -p "$pkgdir/usr/include/$pkgname/flags" || return 1
	install -Dm644 include/$pkgname/*.hpp "$pkgdir/usr/include/$pkgname/" || return 1
	install -Dm644 include/$pkgname/flags/*.hpp "$pkgdir/usr/include/$pkgname/flags/" || return 1
	mkdir -p "$pkgdir/usr/share/licenses/$pkgname" || return 1
	install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE" || return 1
}

md5sums="5b2adac814058f809db99ff01d2b5eaa  stout-0.1.0.tar.gz"
sha256sums="f3deac1abb543667c2f8a715f875a154a8fd4d08b2be666e512026f1ca105c8f  stout-0.1.0.tar.gz"
sha512sums="bb0427c847219ee6d12890e88e8a43ebcd24965c250013fb7b232f1e5eeab93a7ee52b280ba259255dcdb1ddbc1e3a5836feb2badf4fefad27e0ba8dcce51b25  stout-0.1.0.tar.gz"
