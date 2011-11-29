# Maintainer: Eduard Kracmar <edke.kraken[at]gmail[dot]com>
# Contributor: D. Can Celasun <dcelasun[at]gmail[dot]com>
# Contributor: Slava Volkov <sv99sv[at]gmail[dot]com>

pkgname=phpstorm-eap
_pkgname=PhpStorm # Directory name in the tar file
pkgver=111.19
pkgrel=1
pkgdesc="Lightweight and Smart PHP IDE. 30-day free trial."
arch=('i686' 'x86_64')
url="http://www.jetbrains.com/phpstorm/"
license=('custom')
depends=('java-runtime>=6')
conflicts=('phpstorm')
#source=(http://download.jetbrains.com/webide/PhpStorm-EAP-$pkgver.tar.gz) kept for upcoming EAP builds
source=(http://download.jetbrains.com/webide/PhpStorm-3.0.tar.gz)
md5sums=('990e003faba72b0a546cd3c287bdeff8')

build() {
  cd ${srcdir}
  mkdir -p ${pkgdir}/opt/${pkgname} || return 1
  cp -R ${srcdir}/${_pkgname}-${pkgver}/* ${pkgdir}/opt/${pkgname} || return 1
  if [[ $CARCH = 'i686' ]]; then
    rm -f ${pkgdir}/opt/${pkgname}/bin/libyjpagent64.so
    rm -f ${pkgdir}/opt/${pkgname}/bin/libbreakgen64.so
     rm -f ${pkgdir}/opt/${pkgname}/bin/fsnotifier64
  fi
  if [[ $CARCH = 'x86_64' ]]; then
     rm -f ${pkgdir}/opt/${pkgname}/bin/libyjpagent.so
     rm -f ${pkgdir}/opt/${pkgname}/bin/libbreakgen.so
     rm -f ${pkgdir}/opt/${pkgname}/bin/fsnotifier
  fi

(
cat <<EOF
[Desktop Entry]
Version=${pkgver}
Name=PhpStorm
Icon=phpstorm
GenericName=Lightweight and Smart PHP IDE
Comment=Lightweight and Smart PHP IDE 30-day free trial
Exec=/opt/${pkgname}/bin/phpstorm.sh
Terminal=false
Type=Application
Categories=Development
EOF
) > ${startdir}/phpstorm.desktop

  mkdir -p ${pkgdir}/usr/share/applications/ || return 1
  mkdir -p ${pkgdir}/usr/share/pixmaps/ || return 1
  mkdir -p ${pkgdir}/usr/share/licenses/${pkgname}/ || return 1
  install -m 644 ${startdir}/phpstorm.desktop ${pkgdir}/usr/share/applications/
  install -m 644 ${pkgdir}/opt/${pkgname}/bin/webide.png ${pkgdir}/usr/share/pixmaps/phpstorm.png
  install -m 644 ${srcdir}/${_pkgname}-${pkgver}/license/${_pkgname}_license.txt ${pkgdir}/usr/share/licenses/${pkgname}/${_pkgname}_license.txt
}
