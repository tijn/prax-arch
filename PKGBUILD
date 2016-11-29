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
install=$pkgname.install
source=("https://github.com/ysbaddaden/$pkgname.cr/archive/v$pkgver.zip"
        "systemd-services.patch"
        "allow-systemd-interface-names.patch")
md5sums=('6b5d1bda255e5d37b5960e737df00022'
         '5d47fc4a9eef8f4774c426a7d48cce30'
         'f2351d77749ee9c949c237b79e3a02fe')

prepare() {
  cd "$pkgname.cr-$pkgver"
  if ! patch -R --dry-run -Np1 -i "${srcdir}/systemd-services.patch"; then
    patch -Np1 -i "${srcdir}/systemd-services.patch"
  fi
  patch -Np1 -i "${srcdir}/allow-systemd-interface-names.patch"
}

build() {
  cd "$pkgname.cr-$pkgver"
  make
}

# This simple package command works fine but namcap complains about file locations
package() {
  cd "$pkgname.cr-$pkgver"
  make PREFIX="$pkgdir/" install
  rm -rf "${pkgdir}/lib"
  install -D -m644 LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
  install -D -m644 install/arch/README.md "${pkgdir}/usr/share/doc/${pkgname}/arch-linux.md"
  install -D -m644 install/arch/prax-iptables.service "${pkgdir}/usr/lib/systemd/system/prax-iptables.service"
  install -D -m644 install/arch/prax.service "${pkgdir}/usr/lib/systemd/user/prax.service"
}

# package() {
#  cd "$pkgname.cr-$pkgver"
#  make all
#  install -D -m755 -t "${pkgdir}/usr/lib/${pkgname}" libexec/*
#  mkdir "${pkgdir}/usr/bin/"
#  cd "${pkgdir}/usr/bin/" && ln -sf "../lib/${pkgname}/prax"
#  cd -
#  install -D -m644 -t "${pkgdir}/usr/share/doc/${pkgname}" README.md LICENSE install/prax.desktop
#  install -D -m644 install/dnsmasq "${pkgdir}/etc/NetworkManager/dnsmasq.d/prax"
#  install -D -m644 install/dnsmasq "${pkgdir}/etc/dnsmasq.d/prax"
#  install -D -m644 LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"

#  # install arch specific files
#  install -D -m644 install/arch/README.md "${pkgdir}/usr/share/doc/${pkgname}/arch-linux.md"
#  install -D -m644 install/arch/prax-iptables.service "${pkgdir}/usr/lib/systemd/system/prax-iptables.service"
#  install -D -m644 install/arch/prax.service "${pkgdir}/usr/lib/systemd/user/prax.service"
# }
