# Maintainer: Maxime Gauduin <alucryd@archlinux.org>
# Contributor: Ethan Skinner <aur@etskinner.com>
# Contributor: Grégoire Seux <grego_aur@familleseux.net>
# Contributor: Dean Galvin <deangalvin3@gmail.com>
# Contributor: NicoHood <archlinux@nicohood.de>

pkgname=home-assistant
pkgdesc='Open source home automation that puts local control and privacy first'
pkgver=2021.5.0
pkgrel=1
arch=(any)
url=https://home-assistant.io/
license=(APACHE)
depends=(
  gcc
  python-aiohttp
  python-aiohttp-cors
  python-astral
  python-async-timeout
  python-attrs
  python-bcrypt
  python-certifi
  python-ciso8601
  python-cryptography
  python-httpx
  python-jinja
  python-pillow
  python-pip
  python-pyjwt
  python-pytz
  python-requests
  python-ruamel-yaml
  python-slugify
  python-sqlalchemy
  python-voluptuous
  python-voluptuous-serialize
  python-yaml
  python-yarl
)
makedepends=(
  git
  python-setuptools
)
optdepends=(
  'net-tools: Nmap host discovery'
  'openzwave: Z-Wave integration'
  'python-dtlssocket: Ikea Tradfri integration'
  'python-lxml: Meteo France integration'
)
_tag=ccf92e4721bf7c39c11c0239b81252342a244a35
source=(
  git+https://github.com/home-assistant/home-assistant.git#tag=${_tag}
  home-assistant.service
)
b2sums=('SKIP'
        '0df7bbfdac09e37294ac27567e677855c72d13be3aefbd23e0a8f101cf2148302affbe9b6b586b893f77fc990f665d7b95f4916583680c06abd8f74b5cdf3da9')

pkgver() {
  cd home-assistant

  git describe --tags
}

prepare() {
  cd home-assistant

  # lift hard dep constraints, we'll deal with breaking changes ourselves
  sed 's/==/>=/g' -i setup.py homeassistant/package_constraints.txt
}

build() {
  cd home-assistant

  python setup.py build
}

package() {
  cd home-assistant

  python setup.py install --root="${pkgdir}" --prefix=/usr --optimize=1 --skip-build

  install -Dm 644 ../home-assistant.service -t "${pkgdir}"/usr/lib/systemd/system/
}

# vim: ts=2 sw=2 et:
