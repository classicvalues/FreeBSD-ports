PORTNAME=	lua-language-server
DISTVERSION=	3.5.6
CATEGORIES=	devel

MAINTAINER=	adamw@FreeBSD.org
COMMENT=	Sumneko Lua development server and LSP client
WWW=		https://github.com/sumneko/lua-language-server

LICENSE=	MIT
LICENSE_FILE=	${WRKSRC}/LICENSE

LIB_DEPENDS=	libinotify.so:devel/libinotify

# BROKEN_FREEBSD_12=	3rd/bee.lua/bee/thread/spinlock.h:9:14: fatal error: 'immintrin.h' file not found

USES=		compiler:features dos2unix lua:build ninja:make
USE_GITHUB=	yes
GH_ACCOUNT=	sumneko
GH_TUPLE=	actboy168:bee.lua:a749943:bee/3rd/bee.lua \
		actboy168:bee.lua:680acbd:bee_luamake/3rd/luamake/3rd/bee.lua \
		actboy168:luamake:637d163:luamake/3rd/luamake \
		cppcxy:EmmyLuaCodeStyle:3fefe6e:emmyluacodestyle/3rd/EmmyLuaCodeStyle \
		bjornbytes:lovr-docs:8df44c6:lovr/3rd/lovr-api \
		love2d-community:love-api:69e7e01:love/3rd/love-api \
		sqmedeiros:lpeglabel:b5d7638:lpeglabel/3rd/lpeglabel

BINARY_ALIAS=	gcc=${CC}
DOS2UNIX_FILES=	3rd/bee.lua/bee/thread/spinlock.h \
		3rd/luamake/3rd/bee.lua/bee/thread/spinlock.h
SUB_FILES=	lua-language-server
PLIST_FILES=	bin/lua-language-server \
		${DATADIR_REL}/bin/lua-language-server \
		${DATADIR_REL}/bin/main.lua \
		${DATADIR_REL}/debugger.lua \
		${DATADIR_REL}/main.lua
PORTDATA=	locale meta script

.include <bsd.port.pre.mk>

.if ${CHOSEN_COMPILER_TYPE} == clang && ${COMPILER_VERSION} < 130
BUILD_DEPENDS+=	llvm13>0:devel/llvm13
CPP=		${LOCALBASE}/bin/clang-cpp13
CC=		${LOCALBASE}/bin/clang13
CXX=		${LOCALBASE}/bin/clang++13
.endif

# post-extract:
# 	${CP} -rp ${WRKSRC}/3rd/bee.lua ${WRKSRC}/3rd/luamake/3rd

post-patch:
	${REINPLACE_CMD} -e 's|%%CC%%|${CC}|; s|%%LOCALBASE%%|${LOCALBASE}|' \
		${WRKSRC}/3rd/luamake/compile/ninja/freebsd.ninja \
		${WRKSRC}/3rd/bee.lua/compile/common.lua

do-build:
	${DO_MAKE_BUILD} -C ${WRKSRC}/3rd/luamake -f compile/ninja/freebsd.ninja
	cd ${WRKSRC} && ${MAKE_ENV} ./3rd/luamake/luamake -v

do-install:
	${MKDIR} ${STAGEDIR}${DATADIR}/bin
	${INSTALL_SCRIPT} ${WRKDIR}/lua-language-server ${STAGEDIR}${PREFIX}/bin
	${INSTALL_PROGRAM} ${WRKSRC}/bin/lua-language-server ${STAGEDIR}${DATADIR}/bin
	${INSTALL_SCRIPT} ${WRKSRC}/bin/main.lua ${STAGEDIR}${DATADIR}/bin
	${INSTALL_DATA} ${WRKSRC}/debugger.lua ${STAGEDIR}${DATADIR}
	${INSTALL_DATA} ${WRKSRC}/main.lua ${STAGEDIR}${DATADIR}
	cd ${WRKSRC} && ${COPYTREE_SHARE} "locale meta script" ${STAGEDIR}${DATADIR}

.include <bsd.port.mk>
