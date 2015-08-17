# Maintainer: Moritz Kiefer <moritz.kiefer AT gmail DOT com>
pkgname=tomes-of-mephistopheles
pkgver=alpha2
pkgrel=1
pkgdesc="A dungeon-crawling-RPG currently in early state of development. Requires you to preorder Tomes of Mephistopheles."
arch=('i686' 'x86_64')
license=('custom')
url="http://tom.kot-in-action.com/"
_gamepkg="${pkgname}-${pkgver}.tar.gz"
_foldername=tomesofmephistopheles
source=('tomes-of-mephistopheles.desktop' 'tomes-of-mephistopheles')
md5sums=('25ebd7712b9f6ab62e8fe9f01f8b691d'
         'f2eeefc097261a47b0f45f0ba43a59a2')
build() {
  cd $srcdir

  msg "You need a full copy of this game in order to install it"
  msg "Searching for \"${_gamepkg}\"\
  in dir: $(readlink -f ${startdir})"
  pkgpath=${startdir}

  if [[ ! ( -f "${startdir}/${_gamepkg}" ) ]]; then
    error "Game package not found, please type absolute path to game setup package (/home/joe):"
    read pkgpath
    if [[ ! ( -f "${pkgpath}/${_gamepkg}" ) ]] ; then
       error "Unable to find game package." && return 1
   fi
  fi
  msg "Found game package, extracting..."
  ln -fs "${pkgpath}/${_gamepkg}" .
  tar xvf ${srcdir}/${_gamepkg} -C ${srcdir}
}
package() {
  cd ${srcdir}
  install -d ${pkgdir}/opt/${pkgname}
  cp -R ${srcdir}/${_foldername}/* ${pkgdir}/opt/${pkgname}

  rm -R ${pkgdir}/opt/${pkgname}/bin*
  rm -R ${pkgdir}/opt/${pkgname}/*.exe 
  rm -R ${pkgdir}/opt/${pkgname}/*.dll 
  rm -R ${pkgdir}/opt/${pkgname}/*.txt
  rm -R ${pkgdir}/opt/${pkgname}/engine_source.zip

  if [ "$CARCH" = "x86_64" ]; then
    sed -i s:/opt/tomes-of-mephistopheles/tomesofmephistopheles:/opt/tomes-of-mephistopheles/tomesofmephistopheles64: ${srcdir}/${pkgname}
    rm ${pkgdir}/opt/${pkgname}/${_foldername}
  else
    rm ${pkgdir}/opt/${pkgname}/${_foldername}64
  fi
  
  # Copy Icon to /usr/share/icons
  install -D -m644 ${pkgdir}/opt/${pkgname}/icons/tom_icon_128.png ${pkgdir}/usr/share/icons/${pkgname}.png

  # Install Launcher
  install -D -m755 ${srcdir}/${pkgname} ${pkgdir}/usr/bin/${pkgname}

  # Install Desktop
  install -D -m644 ${srcdir}/${pkgname}.desktop ${pkgdir}/usr/share/applications/${pkgname}.desktop
}

