# Maintainer: Arch Haskell Team <arch-haskell@haskell.org>
_hkgname=kibro
pkgname=haskell-kibro
pkgver=0.4.3
pkgrel=3
pkgdesc="Web development framework."
url="http://hackage.haskell.org/package/${_hkgname}"
license=('custom:BSD3')
arch=('i686' 'x86_64')
makedepends=()
depends=('ghc' 'haskell-configfile' 'haskell-cgi=3001.1.7.3' 'haskell-containers=0.3.0.0' 'haskell-data-default' 'haskell-directory=1.0.1.1' 'haskell-fastcgi' 'haskell-filepath=1.1.0.4' 'haskell-haskell98=1.0.1.1' 'haskell-mtl' 'haskell-process=1.0.1.3' 'haskell-random=1.0.0.2' 'haskell-regex-compat=0.93.1' 'haskell-regexpr' 'haskell-safe' 'haskell-strict' 'haskell-unix=2.4.0.2' 'haskell-xhtml=3000.2.0.1')
options=('strip')
source=(http://hackage.haskell.org/packages/archive/${_hkgname}/${pkgver}/${_hkgname}-${pkgver}.tar.gz)
install=${pkgname}.install
build() {
    cd ${srcdir}/${_hkgname}-${pkgver}
    runhaskell Setup configure -O --enable-split-objs --enable-shared \
       --prefix=/usr --docdir=/usr/share/doc/${pkgname} --libsubdir=\$compiler/site-local/\$pkgid
    runhaskell Setup build
    runhaskell Setup haddock
    runhaskell Setup register   --gen-script
    runhaskell Setup unregister --gen-script
    sed -i -r -e "s|ghc-pkg.*unregister[^ ]* |&'--force' |" unregister.sh
}
package() {
    cd ${srcdir}/${_hkgname}-${pkgver}
    install -D -m744 register.sh   ${pkgdir}/usr/share/haskell/${pkgname}/register.sh
    install    -m744 unregister.sh ${pkgdir}/usr/share/haskell/${pkgname}/unregister.sh
    install -d -m755 ${pkgdir}/usr/share/doc/ghc/html/libraries
    ln -s /usr/share/doc/${pkgname}/html ${pkgdir}/usr/share/doc/ghc/html/libraries/${_hkgname}
    runhaskell Setup copy --destdir=${pkgdir}
    install -D -m644 LICENSE ${pkgdir}/usr/share/licenses/${pkgname}/LICENSE
    rm -f ${pkgdir}/usr/share/doc/${pkgname}/LICENSE
}
md5sums=('b42eaab79c4792ce74149526d3cfb26a')
