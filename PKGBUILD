## dinit init, dinitctl, dinitcheck apps #Required
## Copyright (C) 2022 Dinit on Devuan
## LISENCE: GPLv3 or later
## Originaly author: Mobin Aydinfar <mobin@mobintestserver.ir>
# Maintainer: Dinit on Devuan Project <mobin@mobintestserver.ir>

pkgname=('dinit')
pkgver=0.14.0
pkgrel=1
pkgdesc="Service monitoring / "init" system -- dinit init"

## Note: dinit should be able to work properly on any architecture supported by gcc, BUT ONLY TESTED ON amd64!
## USE IT AT YOUR OWN RISK!
#arch=(any)
arch=('amd64')

url="https://github.com/davmac314/dinit"
license=('Apache')
depends=('libc6')
replaces=('sysvinit-core' 'runit-init' 'init' 'systemd' 'libnss-systemd' 'systemd-sysv' 'dinit-compat')
provides=('init')

## Unfortunately makedeb does not currently support 'priority'.
## Issue #190: https://github.com/makedeb/makedeb/issues/190
#priority='high'

makedepends=('gcc' 'make' 'g++' 'm4' 'build-essential')
source=("$url/releases/download/v$pkgver/$pkgname-$pkgver.tar.xz"
        mconfig.Linux)

## Warning: Its checksum only valid for 0.14.0! change it if you want newer/older version
sha256sums=('f58f53b6901b8a0a1788a1f0937766bd171570d3c067dcd4b66752229b047c0e'
            '2c16e2e4da36d465723cc69a693901d9ce3095517d0d711a116bcabe2aeb7dd1')

build() {
## Note: We use custom mconfig.Linux. Original mconfig.Linux is buggy on devuan ceres!
#  cd "$srcdir"/"$pkgname-$pkgver"/configs
#  chmod +x mconfig.Linux.sh
#  sh ./mconfig.Linux.sh
#  mv mconfig.Linux ../

  cd "$srcdir"
  mv mconfig.Linux "$pkgname-$pkgver"/mconfig
  cd "$pkgname-$pkgver"
  make DESTDIR="$pkgdir/"
}

check() {
  cd "$srcdir"/"$pkgname-$pkgver"/
  make DESTDIR="$pkgdir/" check
  make DESTDIR="$pkgdir/" check-igr
}

package() {
  cd "$srcdir"/"$pkgname-$pkgver"/
  make install DESTDIR="$pkgdir/"
  ln -s dinit "$pkgdir/sbin/init"
}
