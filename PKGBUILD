# Fork maintainer: Christopher Crockett <qutebrowser-profile-pkgbuild@chray.cc>
# Original PKGBUILD file by: Pieter Joost van de Sande <pj@born2code.net>
# Original file from: (https://aur.archlinux.org/packages/qutebrowser-profile-git)

pkgname=qutebrowser-profile-chao
_pkgname="qutebrowser-profile"
provides=("qutebrowser-profile")
conflicts=("qutebrowser-profile-git")
pkgdesc="A fork of the simple wrapper script for qutebrowser that allows you to maintain different profiles"
url="https://github.com/chaorace/qutebrowser-profile"
pkgver=1
pkgrel=1
license=("MIT")
arch=("any")
makedepends=("git")
depends=("bash")
source=("qutebrowser-profile" "qutebrowser-profile.desktop" "LICENSE")
md5sums=("SKIP" "582d38d2e2ee4e95f5fc15b01cab3658" "c59c79cb36dda6da9a5fd8b20723c1ee")

pkgver() {
  cd "${srcdir}"
  git log -1 --format='%cd.%h' --date=short | tr -d -
}

package()
{
  chmod +x "${srcdir}/qutebrowser-profile"
  install -Dm755 "${srcdir}/qutebrowser-profile"         "${pkgdir}/usr/bin/${_pkgname}"
  install -Dm644 "${srcdir}/qutebrowser-profile.desktop" "${pkgdir}/usr/share/applications/qutebrowser-profile.desktop"
  install -Dm644 "${srcdir}/LICENSE"                     "${pkgdir}/usr/share/licenses/${_pkgname}/LICENSE"
}
