# Maintainer: Tijn Schuurmans <tijnschuurmans+prax at gmail dot com>
pkgname='prax'
pkgver='0.6.1'
pkgrel=1
pkgdesc="Rack proxy server for development"
arch=('any')
url="https://github.com/ysbaddaden/prax.cr"
license=('custom:CeCILL 2.1 License')
depends=('bash')
makedepends=('crystal' 'git')
optdepends=('dnsmasq: forward .dev domains to prax')
backup=('etc/NetworkManager/dnsmasq.d/prax')
source=("https://github.com/ysbaddaden/$pkgname.cr/archive/v$pkgver.zip")
md5sums=('6b5d1bda255e5d37b5960e737df00022')

build() {
  cd "$pkgname.cr-$pkgver"
  make
}

# This simple package command works fine but namcap complains about file locations
#package() {
#  cd "$pkgname.cr-$pkgver"
#  make PREFIX="$pkgdir/" install
#  install -D -m644 LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
  #install -D -m644 install/arch/prax-iptables.service "${pkgdir}/etc/systemd/system/prax-iptables.service"
  #install -D -m644 install/arch/prax.service "$pkgdir"/usr/lib/systemd/user/prax.service
#}

package() {
 cd "$pkgname.cr-$pkgver"
 make all
 install -D -m755 -t "${pkgdir}/usr/lib/${pkgname}" libexec/*
 mkdir "${pkgdir}/usr/bin/"
 cd "${pkgdir}/usr/bin/" && ln -sf "../lib/${pkgname}/prax"
 cd -
 install -D -m644 -t "${pkgdir}/usr/share/doc/${pkgname}" README.md LICENSE install/prax.desktop
 # install -D -m644 install/arch/README.md "${pkgdir}/usr/share/doc/${pkgname}/arch-linux.md"
 install -D -m644 install/dnsmasq "${pkgdir}/etc/NetworkManager/dnsmasq.d/prax"
 install -D -m644 install/dnsmasq "${pkgdir}/etc/dnsmasq.d/prax"
 install -D -m644 LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
 # install -D -m644 install/arch/prax-iptables.service "${pkgdir}/etc/systemd/system/prax-iptables.service"
 # install -D -m644 install/arch/prax.service "$pkgdir"/usr/lib/systemd/user/prax.service
}
