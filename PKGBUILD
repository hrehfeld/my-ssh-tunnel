# Maintainer: Hauke Rehfeld <aur@haukerehfeld.de>
set -xe
source ".env"
set +e

pkgname="my-ssh-tunnel-${TUNNEL_HOST}-${DESTINATION_PORT}-${TUNNEL_PORT}-${SOURCE_PORT}"
set +x

pkgver=1
pkgrel=6
epoch=
pkgdesc=""
arch=('i686' 'x86_64')
url=""
license=('GPL')
groups=()
depends=("openssh")
makedepends=()
checkdepends=()
optdepends=()
provides=()
conflicts=()
replaces=()
backup=()
options=()
install=
changelog=
source=("from-destination" "to-destination" "ssh.template.service")
sha256sums=('a8df6ab00b0fdddcee40743487c844b48e6b697de7a72a11e6e41e93183b13c7'
            '128cbe4a9532dca5cc729d2e1c04f2186ce428d866273c8443ba80c919b15984'
            '465d5e12c99a3aea32dece38adf4277cfa2c6f1983a32ee225ecfd762f1ab123')





_bins=("from-destination" "to-destination")


_installdir="/usr/lib/${pkgname}"



_SYSTEMD_SERVICE_DIR="/etc/systemd/user"


noextract=()

prepare() {
  set -x
  cd "$srcdir"
  cp "../.env" "."
  for bin in ${source[@]}
  do
    [ -L "${srcdir}/${bin}" ] && cp -a --remove-destination $(readlink "${srcdir}/${bin}") "${srcdir}/${bin}"
    sed -i 's!${pkgdir}!'"${_installdir}"'!g' "$bin"
  done

  for bin in ${_bins[@]}
  do
    binname="${pkgname}-${bin}"
    binpath="/usr/bin/$binname"
    sed 's!${cmd}!'"${binpath}"'!g' "${srcdir}/ssh.template.service" > "${srcdir}/${bin}.service"
  done
  set +x
}

package() {
  set -x

  mkdir -p "${pkgdir}/usr/bin/"
  cd "$srcdir"
  install -Dm644 ".env" "${pkgdir}${_installdir}/.env"
  for bin in ${_bins[@]}
  do
    binname="${pkgname}-${bin}"
    binpath="/usr/bin/$binname"
    install -Dm755 "${srcdir}/${bin}" "${pkgdir}${_installdir}/${binname}"
    ln -sf "${_installdir}/$binname" "${pkgdir}${binpath}"

    install -Dm644 "${srcdir}/${bin}.service" "${pkgdir}${_SYSTEMD_SERVICE_DIR}/${binname}.service"
  done

  set +x
}

# vim:set ts=2 sw=2 et:
