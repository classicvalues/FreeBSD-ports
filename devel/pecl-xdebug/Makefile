PORTNAME=	xdebug
DISTVERSION=	3.1.6
CATEGORIES=	devel pear

MAINTAINER=	pizzamig@FreeBSD.org
COMMENT=	Xdebug extension for PHP
WWW=		https://www.xdebug.org/

LICENSE=	PHP30
LICENSE_FILE=	${WRKSRC}/LICENSE

CONFIGURE_ARGS=	--enable-xdebug
USES=		php:pecl,zend tar:tgz
IGNORE_WITH_PHP=	82

SUB_FILES=	pkg-message

.include <bsd.port.mk>
