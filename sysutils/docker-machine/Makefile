PORTNAME=		docker-machine
PORTVERSION=		0.16.2
DISTVERSIONPREFIX=	v
PORTREVISION=		6
CATEGORIES=		sysutils

MAINTAINER=		ports@FreeBSD.org
COMMENT=		Tool to create Docker hosts
WWW=		https://github.com/docker/machine/

LICENSE=		APACHE20
LICENSE_FILE=		${WRKSRC}/LICENSE

PLIST_FILES=		bin/docker-machine

USE_GITHUB=		yes

USES=	go

GH_ACCOUNT=	docker
GH_PROJECT=	machine

GO_PKGNAME=	github.com/${GH_ACCOUNT}/${GH_PROJECT}
GO_TARGET=	github.com/${GH_ACCOUNT}/${GH_PROJECT}/cmd/${PORTNAME}

.include <bsd.port.mk>
