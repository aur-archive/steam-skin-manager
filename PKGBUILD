# Maintainer: Alucryd <alucryd at gmail dot com>

pkgname=steam-skin-manager
pkgver=3.9.1
pkgrel=2
pkgdesc="GUI for Steam skins management"
arch=('i686' 'x86_64')
url="http://iubuntu.cz/Steam/"
license=('GPL3')
depends=('steam' 'qtwebkit')
install=${pkgname}.install
options=('!strip' 'emptydirs')
source=("steam-skin-manager-${pkgver}.deb::http://iubuntu.cz/Steam/steam-skin-installer.deb" 'steam-skin-manager.desktop' 'steam-wb.desktop')
sha256sums=('0ae53534232ef410839934bf6505da1f6d2c16f2a838b2d474b88bdec6a7585b'
            'ec6fdcdfa6eb5483fd6e996a38cd89dd9dbac70c119cd764aa25e0da6e7d04e2'
            '55c6d96cf70bc853c8aebc173484889db87213939bcace74eb2a6c66eb388f90')

build() {
  cd "${srcdir}"

  tar -xf data.tar.gz
  rm -rf usr/share/{applications/*,icons,pixmaps/steamwb.svg,steam}
  cp *.desktop usr/share/applications/
}

package() {
  cd "${srcdir}"

  cp -dr --no-preserve=ownership usr "${pkgdir}"/

# Fix paths for i686
  if  [[ ${CARCH} == i686 ]] ; then
    mv "${pkgdir}"/usr/lib32 "${pkgdir}"/usr/lib
  fi

# Fix permissions
  find "${pkgdir}" -type d -exec chmod 755 {} +
  find "${pkgdir}" -type f -exec chmod 644 {} +
  chmod 755 "${pkgdir}"/usr/bin/{steam-{skin,wb},SteamSkinManager}
  install -dm755 "${pkgdir}"/usr/share/steam/skins
}

# vim: ts=2 sw=2 et:
