# Maintainer: Ben Edwards <ben@artfuldodge.io>
# Contributors: Lukas Fleischer, Simon Zimmermann

pkgname='pass-diceware'
pkgver=1.7.3
pkgrel=1
pkgdesc='Stores, retrieves, generates, and synchronizes passwords securely, with 100% more diceware'
arch=('any')
url='https://www.passwordstore.org/'
license=('GPL2')
depends=('xclip' 'bash' 'gnupg' 'tree' 'diceware')
checkdepends=('git')
optdepends=('git: for Git support'
            'dmenu: for passmenu'
            'qrencode: for QR code support')
provides=('pass' 'passmenu')
conflicts=('pass' 'passmenu')
source=('pass.patch'
        "https://git.zx2c4.com/password-store/snapshot/password-store-${pkgver}.tar.xz")
sha256sums=('ff51f6a035fe5e116643bf66e1884b494fa599a74bbf858fe50b48033dde6527'
            '2b6c65846ebace9a15a118503dcd31b6440949a30d3b5291dfb5b1615b99a3f4')

check() {
  cd "${srcdir}/password-store-$pkgver/"
  make test
}

package() {
  cd "${srcdir}/password-store-$pkgver/"
  make DESTDIR="${pkgdir}" WITH_ALLCOMP=yes install
  patch "${pkgdir}/usr/bin/pass" "${srcdir}/pass.patch"

  cd contrib/dmenu
  install -Dm0755 passmenu "${pkgdir}/usr/bin/passmenu"
}
