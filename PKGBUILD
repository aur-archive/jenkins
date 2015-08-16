#Contributor: Yahya Mohajer < yaya_2013 At yahoo Dot com >

pkgname=jenkins
pkgver=1.515
pkgrel=1
_wrapver=3.5.14
pkgdesc="Extensible Continuous Integration Server. Hudson forks"
url="http://jenkins-ci.org/"
arch=('i686' 'x86_64')
license=('MIT')
depends=('java-environment' 'ttf-dejavu' 'libcups' )
optdepends=('apache: a full featured webserver'
            'maven: a java project management and project comprehension tool')

conflicts=('jenkins')
provides=('jenkins')
options=(!strip !docs )

install=jenkins.install
backup=(opt/jenkins/conf/wrapper.conf)
source=(http://updates.jenkins-ci.org/download/war/${pkgver}/jenkins.war
        http://wrapper.tanukisoftware.org/download/$_wrapver/wrapper-delta-pack-$_wrapver.tar.gz
        'wrapper.conf'
        'jenkins')	

noextract=(jenkins.war)

md5sums=('a0a0f8cf8582f3daf539e495f1edb6a0'
         '1636c4b1960c404c3e2eecb23f19834f'
         'f81c36c4b4af84ca647775e0f3e21729'
         '65ec4b39356076e7b438184962d007a1')

build() {
  cd ${srcdir}

  # Create directory
  install -dm755 $pkgdir/opt/jenkins
  install -dm755 $pkgdir/opt/jenkins/bin
  install -dm755 $pkgdir/opt/jenkins/lib
  install -dm755 $pkgdir/opt/jenkins/conf
  install -dm755 $pkgdir/opt/jenkins/logs
  install -dm755 $pkgdir/opt/jenkins/tmp

  # prepare wrapper
  if [ $CARCH = 'x86_64' ]; then
    install -Dm755  $srcdir/wrapper-delta-pack-$_wrapver/bin/wrapper-linux-x86-64    $pkgdir/opt/jenkins/bin/wrapper
    install -Dm644 $srcdir/wrapper-delta-pack-$_wrapver/lib/libwrapper-linux-x86-64.so $pkgdir/opt/jenkins/lib/
  elif [ $CARCH = 'i686' ]; then
    install -Dm755  $srcdir/wrapper-delta-pack-$_wrapver/bin/wrapper-linux-x86-32 $pkgdir/opt/jenkins/bin/wrapper
    install -Dm644  $srcdir/wrapper-delta-pack-$_wrapver/lib/libwrapper-linux-x86-32.so $pkgdir/opt/jenkins/lib/
  fi
   install -Dm644 $srcdir/wrapper-delta-pack-$_wrapver/lib/wrapper.jar $pkgdir/opt/jenkins/lib/
   install -Dm644 $srcdir/wrapper-delta-pack-$_wrapver/logs/wrapper.log $pkgdir/opt/jenkins/logs/

   install -Dm644 $srcdir/jenkins.war $pkgdir/opt/jenkins/lib/

   install -Dm644 $srcdir/wrapper.conf $pkgdir/opt/jenkins/conf/
   install -Dm755 $srcdir/jenkins $pkgdir/opt/jenkins/bin/

   mkdir -p $pkgdir/var/lib/jenkins
   mkdir -p $pkgdir/opt/jenkins/run

}
