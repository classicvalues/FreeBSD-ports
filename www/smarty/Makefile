PORTNAME=	smarty
DISTVERSIONPREFIX=	v
PORTVERSION=	4.2.1
CATEGORIES=	www
PKGNAMESUFFIX=	${PHP_PKGNAMESUFFIX}

MAINTAINER=	sunpoet@FreeBSD.org
COMMENT=	PHP compiling template engine
WWW=		https://www.smarty.net/

LICENSE=	LGPL3+
LICENSE_FILE=	${WRKSRC}/LICENSE

USES=		cpe php:flavors,web
USE_PHP=	pcre

NO_ARCH=	yes
NO_BUILD=	yes

DATADIR=	${PREFIX}/share/smarty${PHP_PKGNAMESUFFIX}
SUB_FILES=	pkg-message

USE_GITHUB=	yes
GH_ACCOUNT=	smarty-php

do-install:
	${MKDIR} ${STAGEDIR}${DATADIR}
	cd ${WRKSRC}/libs && ${COPYTREE_SHARE} . ${STAGEDIR}${DATADIR}

.include <bsd.port.mk>
