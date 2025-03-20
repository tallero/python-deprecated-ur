# SPDX-License-Identifier: AGPL-3.0

#    ----------------------------------------------------------------------
#    Copyright © 2025  Pellegrino Prevete
#
#    All rights reserved
#    ----------------------------------------------------------------------
#
#    This program is free software: you can redistribute it and/or modify
#    it under the terms of the GNU Affero General Public License as published by
#    the Free Software Foundation, either version 3 of the License, or
#    (at your option) any later version.
#
#    This program is distributed in the hope that it will be useful,
#    but WITHOUT ANY WARRANTY; without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#    GNU Affero General Public License for more details.
#
#    You should have received a copy of the GNU Affero General Public License
#    along with this program.  If not, see <https://www.gnu.org/licenses/>.

# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Truocolo <truocolo@0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b>
# Maintainer: Pellegrino Prevete (dvorak) <pellegrinoprevete@gmail.com>
# Maintainer: Pellegrino Prevete (dvorak) <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>
# Maintainer: Felix Yan <felixonmars@archlinux.org>

_py="python"
_pyver="$( \
  "${_py}" \
    -V | \
    awk \
      '{print $2}')"
_pymajver="${_pyver%.*}"
_pyminver="${_pymajver#*.}"
_pynextver="${_pymajver%.*}.$(( \
  ${_pyminver} + 1))"
_pkg=deprecated
pkgname="${_py}-${_pkg}"
pkgver=1.2.16
pkgrel=1
_pkgdesc=(
  "Python @deprecated decorator"
  "to deprecate old python classes,"
  "functions or methods"
)
pkgdesc="${_pkgdesc[*]}"
_http="https://github.com"
_ns="tantale"
url="${_http}/${_ns}/${_pkg}"
license=(
  'MIT'
)
arch=(
  'any'
)
depends=(
  "${_py}>=${_pymajver}"
  "${_py}<${_pynextver}"
  "${_py}-wrapt"
)
makedepends=(
  'git'
  "${_py}-setuptools"
  "${_py}-build"
  "${_py}-installer"
  "${_py}-wheel"
)
checkdepends=(
  "${_py}-pytest"
)
source=(
  "git+${url}.git#tag=v${pkgver}"
)
sha512sums=(
  '065ad0b0a3ed355226578320422c8f6e3fa31bf10a66a73801cf119922373b32b62ba72ea2d8cfe3afb849240a0d2e59da199bdd2b3991c23d52ce30ff62db31'
)

build() {
  cd \
    "${_pkg}"
  "${_py}" \
    -m \
      build \
    --wheel \
    --no-isolation
}

check() {
  cd deprecated
  pytest
}

package() {
  cd \
    "${_pkg}"
  "${_py}" \
    -m \
      installer \
    --destdir="${pkgdir}" \
    "dist/"*".whl"
  install \
    -Dm644 \
    "LICENSE.rst" \
    -t \
    "${pkgdir}/usr/share/licenses/${pkgname}/"
}
