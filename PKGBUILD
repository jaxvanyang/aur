# Maintainer: Jax Young <jaxvanyang@gmail.com>

pkgname=mygo-git
_pkgname="${pkgname%-git}"
pkgver=0.1.0.r144.7ef2505
pkgrel=1
pkgdesc="My BetaGo implementation in PyTorch!"
arch=('any')
url="https://github.com/jaxvanyang/mygo"
license=('MIT')
depends=('python-pytorch' 'python-numpy')
makedepends=(
	'git'
	'git-lfs'
	'python-build'
	'python-installer'
	'python-wheel'
	'python-pdm-backend'
)
checkdepends=('python-pytest')
provides=("$_pkgname")
conflicts=("$_pkgname")

prepare() {
	rm -rf "$_pkgname" && git clone https://github.com/jaxvanyang/mygo.git
	cd "$_pkgname"
	git lfs install --local
	git lfs fetch
	git lfs checkout
}

pkgver() {
	cd "$_pkgname"
	printf "0.1.0.r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

build() {
	cd "$_pkgname"
	python -m build --wheel --no-isolation
}

check() {
	cd "$_pkgname"
	export CI=true
	pytest tests
}

package() {
	cd "$_pkgname"
	python -m installer --destdir "$pkgdir" dist/*.whl
	install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
