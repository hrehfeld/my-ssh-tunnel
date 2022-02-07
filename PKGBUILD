# Maintainer: Hauke Rehfeld <aur@haukerehfeld.de>
SCRIPT_DIR=$(cd $(dirname "${BASH_SOURCE[0]}") && pwd)
source="$SCRIPT_DIR/.env"

pkgname="my-ssh-tunnel-${TUNNEL_HOST}-${DESTINATION_PORT}-${TUNNEL_PORT}-${SOURCE_PORT}"
pkgver=1
pkgrel=1
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
source=( "$SCRIPT_DIR/from-destination" "$SCRIPT_DIR/to-destination")
sha256sums=('19408b0f69de5006bbdcb6fdc0b707ac213e70364cf5edaf111134e8c79c8796'
            '069865f6451af78d43aeb362779ae35bc4878b381e559f2340cc00045c8fc418')

noextract=()

_BINS=("from-destination " "to-destination")

prepare() {
  cd "$srcdir"
}

package() {
  set -x
  cd "$srcdir"
  for bin in ${_BINS[@]}
  do
    binname="${pkgname}-${bin}"
    install -Dm755 "$binname" "$pkgdir/usr/lib/${pkgname}/${binname}"
  done
  install -Dm644 ".env" "$pkgdir/usr/lib/${pkgname}/.env"
  set +x
}

# vim:set ts=2 sw=2 et:
