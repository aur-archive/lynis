# Maintainer: Levente Polyak <levente[at]leventepolyak[dot]net>
# Contributor: Sébastien Luttringer <seblu@aur.archlinux.org>

pkgname=lynis
pkgver=2.1.0
pkgrel=1
pkgdesc='Security and system auditing tool to harden Unix/Linux systems'
url='https://cisofy.com/lynis/'
license=('GPL3')
arch=('any')
backup=('etc/lynis/default.prf')
depends=('sh')
optdepends=(
  'net-tools: networking tests'
  'bash-completion: completion for bash'
)
source=(${pkgname}-${pkgver}.tar.gz::https://github.com/CISOfy/${pkgname}/archive/${pkgver}.tar.gz)
sha512sums=('4ed7fc11b14896518457e5ac8ada35cb8afc798f9fbc6b1b4d9f971b64a93f76215c1c3b2506ac0c12a478f53248eab0fd93347bc262f5fb6c0fe4e663c2e346')

prepare() {
  cd ${pkgname}-${pkgver}
  sed -e 's|/path/to/lynis|/usr/bin/lynis|g' -i extras/systemd/lynis.service
}

package() {
  cd ${pkgname}-${pkgver}

  # profile
  install -Dm 644 default.prf "${pkgdir}/etc/${pkgname}/default.prf"

  # binary
  install -Dm 755 "${pkgname}" "${pkgdir}/usr/bin/${pkgname}"

  # plugins, include, db
  install -d "${pkgdir}/usr/share/${pkgname}"
  cp -a db include plugins "${pkgdir}/usr/share/${pkgname}"

  # doc files
  install -d "${pkgdir}/usr/share/doc/${pkgname}"
  install -m 644 -t "${pkgdir}/usr/share/doc/${pkgname}" README INSTALL CHANGELOG FAQ

  # manpage
  install -Dm 644 "${pkgname}.8" "${pkgdir}/usr/share/man/man8/${pkgname}.8"

  # completion
  install -Dm 644 extras/bash_completion.d/${pkgname} "${pkgdir}/usr/share/bash-completion/completions/${pkgname}"

  # systemd
  install -d "${pkgdir}/usr/lib/systemd/system/"
  install -m 644 extras/systemd/{lynis.service,lynis.timer} "${pkgdir}/usr/lib/systemd/system/"
}

# vim:set ts=2 sw=2 ft=sh et:
