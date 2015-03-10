pkgname=awbot-irk
pkgver=2.12
pkgrel=1

pkgdesc="send messages to IRC using irker"
url="http://www.catb.org/esr/irker/"
arch=('any')
license=('BSD')

conflicts=('irker' 'awbot' 'awbot-git')
provides=('irker' 'awbot' 'awbot-git')

backup=('etc/awbot-irk.conf')

depends=('python2' 'jshon')
makedepends=('xmlto' 'docbook-xml' 'docbook-xsl')

source=("http://www.catb.org/~esr/irker/irker-$pkgver.tar.gz"
	'24-hour-XMIT_TTL.patch'
	'awbot'
	'awbot-irk.conf'
	'awbot-irk'
	'awbot-irk.service'
       )

sha1sums=('332b1e647b3f06755f02c03262409909d278c372'
          'SKIP'
          'SKIP'
          'SKIP'
          'SKIP'
          'SKIP'
         )

build() {
	cd "$srcdir"
	sed -i -e 's,^conf=.*$,conf=/etc/awbot-irk.conf,' awbot awbot-irk
	cd irker-$pkgver
	patch -Np1 -i ../24-hour-XMIT_TTL.patch
	sed -i '1s|python|python2|' irk irkerd irkerhook.py
	make
}

package() {
	cd "$srcdir"
	install -Dm 755 awbot "$pkgdir"/usr/bin/awbot
	install -Dm 755 awbot-irk "$pkgdir"/usr/bin/awbot-irk
	install -Dm 644 awbot-irk.conf "$pkgdir"/etc/awbot-irk.conf
	install -Dm 644 awbot-irk.service "$pkgdir"/usr/lib/systemd/system/awbot-irk.service
	cd irker-$pkgver
	make DESTDIR="$pkgdir" install
	install -Dm 755 irkerhook.py "$pkgdir"/usr/bin/irkerhook.py
	install -Dm 755 irk "$pkgdir"/usr/bin/irk
	install -Dm 644 COPYING "$pkgdir"/usr/share/licenses/irker/LICENSE
}
