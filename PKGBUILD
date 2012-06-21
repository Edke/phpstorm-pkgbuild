# Maintainer: Eduard Kracmar <edke.kraken[at]gmail[dot]com>
# Contributor: D. Can Celasun <dcelasun[at]gmail[dot]com>
# Contributor: Slava Volkov <sv99sv[at]gmail[dot]com>

pkgname=phpstorm-eap
_pkgname=PhpStorm # Directory name in the tar file
pkgver=117.609
pkgbuild=117.609
pkgrel=1
pkgdesc="Lightweight and Smart PHP IDE. 30-day free trial."
arch=('i686' 'x86_64')
url="http://www.jetbrains.com/phpstorm/"
license=('custom')
depends=('java-runtime>=6')
conflicts=('phpstorm')
source=(http://download.jetbrains.com/webide/PhpStorm-EAP-$pkgbuild.tar.gz)
#source=(http://download.jetbrains.com/webide/PhpStorm-4.0.2.tar.gz)
md5sums=('8636aad61efa28f9709cc8c02f250c29')

build() {
  cd ${srcdir}
  mkdir -p ${pkgdir}/opt/${pkgname} || return 1
  cp -R ${srcdir}/${_pkgname}-${pkgbuild}/* ${pkgdir}/opt/${pkgname} || return 1
#  cp -R ${srcdir}/${_pkgname}-${pkgver}/* ${pkgdir}/opt/${pkgname} || return 1
  if [[ $CARCH = 'i686' ]]; then
     rm -f ${pkgdir}/opt/${pkgname}/bin/libyjpagent-linux64.so
     rm -f ${pkgdir}/opt/${pkgname}/bin/fsnotifier64
  fi
  if [[ $CARCH = 'x86_64' ]]; then
     rm -f ${pkgdir}/opt/${pkgname}/bin/libyjpagent-linux.so
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

  mkdir -p ${pkgdir}/usr/bin/ || return 1
  mkdir -p ${pkgdir}/usr/share/applications/ || return 1
  mkdir -p ${pkgdir}/usr/share/pixmaps/ || return 1
  mkdir -p ${pkgdir}/usr/share/licenses/${pkgname}/ || return 1
  install -m 644 ${startdir}/phpstorm.desktop ${pkgdir}/usr/share/applications/
  install -m 644 ${pkgdir}/opt/${pkgname}/bin/webide.png ${pkgdir}/usr/share/pixmaps/phpstorm.png
  install -m 644 ${srcdir}/${_pkgname}-${pkgbuild}/license/${_pkgname}_license.txt ${pkgdir}/usr/share/licenses/${pkgname}/${_pkgname}_license.txt
  ln -s /opt/$pkgname/bin/phpstorm.sh "$pkgdir/usr/bin/phpstorm"
}
