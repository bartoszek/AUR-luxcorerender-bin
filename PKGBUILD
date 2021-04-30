# Maintainer: Oliver Mangold <omgold@dray.be>
pkgname=luxcorerender-bin
pkgver=2.5
pkgrel=1
pkgdesc="LuxCoreRender is a physically correct, unbiased rendering engine (official binary version)."
arch=('x86_64')
license=('apache')
depends=(embree openimagedenoise gtk3)
optdepends=('ocl-icd: for gpu acceleration'
            'cuda: for OptiX/CUDA acceleration'
            'python: for pyluxcoretools')
makedepends=(python)
conflicts=(luxcorerender)
provides=(luxcorerender=${pkgver})
source=(
    "https://github.com/LuxCoreRender/LuxCore/releases/download/luxcorerender_v${pkgver}/luxcorerender-v${pkgver}-linux64.tar.bz2"
    "https://github.com/LuxCoreRender/LuxCore/releases/download/luxcorerender_v${pkgver}/luxcorerender-v${pkgver}-linux64-sdk.tar.bz2"
)
sha256sums=('7732a2eecb64cfe3e04699dd048b3b8fb2cefcc3a31aadf3c501789d470e68c1'
            'ec9a262864899da0f8713654bfd67036d902dd0bc73ecdf738698d64cbf1dee9')

package() {
    local _pyver=$(python -c "from sys import version_info; print(\"%d.%d\" % (version_info[0],version_info[1]))")

    cd "${srcdir}/LuxCore-sdk"
    install -Dm755 -t $pkgdir/usr/lib/ lib/lib{luxcore.so,OpenImageDenoise.so.0}
    install -Dm755 -t $pkgdir/usr/bin/ bin/luxcoreconsole
# Demos won't work: requires to be run in parent of scenes directory
# and have write permission to save output.
# Luxcoreui won't work with `-hdr.cfg` as there's a bug in `LuxCoreApp::LoadRenderConfig()`
    install -Dm755 -t $pkgdir/usr/share/luxcorerender/ bin/luxcore{ui,{,scene}demo}
    cp -r scenes  $pkgdir/usr/share/luxcorerender
    cd "${srcdir}/LuxCore"
    install -Dm755 -t $pkgdir/usr/lib/python${_pyver} pyluxcore.so
    install -Dm644 pyluxcoretools.zip $pkgdir/usr/lib/
}
