PORTNAME=	gemmi
DISTVERSIONPREFIX=	v
DISTVERSION=	0.5.7
CATEGORIES=	science # chemistry

MAINTAINER=	yuri@FreeBSD.org
COMMENT=	Macromolecular crystallography library and utilities
WWW=		https://gemmi.readthedocs.io/en/latest/

LICENSE=	MPL20
LICENSE_FILE=	${WRKSRC}/LICENSE.txt

USES=		cmake:testing compiler:c++17-lang # tests don't run, see https://github.com/project-gemmi/gemmi/issues/231

USE_GITHUB=	yes
GH_ACCOUNT=	project-gemmi

CMAKE_TESTING_TARGET=	check

OPTIONS_DEFINE=		FORTRAN

FORTRAN_USES=		fortran
FORTRAN_CMAKE_BOOL=	USE_FORTRAN
FORTRAN_BROKEN=		project option doesn't do anything, see https://github.com/project-gemmi/gemmi/issues/232

.include <bsd.port.mk>
