# Maintainer: Paul Hentschel <aur at hpminc dot com>

pkgname=fah-client-bastet
pkgver=8.3.18
pkgrel=1
pkgdesc="A distributed computing project for simulating protein dynamics"
arch=('x86_64')
url="https://github.com/FoldingAtHome/fah-client-bastet"
license=('GPL-3.0-or-later')
depends=(
  'expat'
  'openssl'
  'systemd-libs'
  'bzip2'
  'sqlite'
  'zlib'
)
makedepends=(
  'git'
  'scons'
  'v8-r'
)
provides=('fah-client-bastet')
source=(
  "git+https://github.com/CauldronDevelopmentLLC/cbang.git"
  "git+https://github.com/FoldingAtHome/fah-client-bastet.git#tag=v$pkgver"
  "config.xml"
)
sha256sums=('SKIP'
            '84b6a952206a9c423b629ff46bb602e2d500c3d230b149b927fdb0e615e18c74'
            '42eb7e85539a43c9a630a4df6f51519a69de459ca639cbad6d36d222f699ee9c')
install="$pkgname.install"

build() {
  scons -C cbang
  CBANG_HOME="$PWD/cbang" scons -C fah-client-bastet
}

package() {
  install -Dm 644 config.xml -t "${pkgdir}"/usr/share/doc/fah-client/
  cd $pkgname
  install -Dm 755 fah-client -t "${pkgdir}"/usr/bin/
  install -Dm 644 install/lin/fah-client.service -t "${pkgdir}"/usr/lib/systemd/system/
  install -dm 750 "${pkgdir}"/usr/share/polkit-1/rules.d/
  install -m 644 install/lin/fah-client.rules -t "${pkgdir}"/usr/share/polkit-1/rules.d/
  install -Dm 644 README.md -t "${pkgdir}"/usr/share/doc/fah-client/
  install -dm 755 "${pkgdir}"/var/lib/fah-client
  install -dm 755 "${pkgdir}"/var/log/fah-client
  install -dm 755 "${pkgdir}"/etc/fah-client
}

# vim:set ts=2 sw=2 et:
