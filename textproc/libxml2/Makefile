PORTNAME=	libxml2
DISTVERSION=	2.10.3
PORTREVISION?=	1
CATEGORIES?=	textproc gnome
MASTER_SITES=	GNOME/sources/${PORTNAME}/${DISTVERSION:R}/
DIST_SUBDIR=	gnome

MAINTAINER=	desktop@FreeBSD.org
COMMENT?=	XML parser library for GNOME
WWW=		http://xmlsoft.org/

LICENSE=	MIT

# Upstream offers CMake in addition to autotools, but we use the latter.
# CMake is a heavy build system, heavier than autotools, and this
# port has many consumers of its core functionality. Some such
# consumers, especially when optioned appropriately (and users have
# a right to do so), may become dependencies of dependencies of CMake.
# Additionally, some consumers rely on symbol versioning that CMake
# does not support (as of Q2 2022) without a hack. Please consider the
# effects of the ecosystem and technical merits before considering
# switching build systems again. Any changes to this end not dogfooded
# thoroughly may be reverted.
USES+=		cpe iconv libtool localbase pathfix pkgconfig tar:xz
CPE_VENDOR=	xmlsoft
GNU_CONFIGURE=	yes
USE_LDCONFIG=	yes

INSTALL_TARGET=	install-strip
TEST_TARGET=	check

PLIST_SUB+=	LIBVERSION=${DISTVERSION}

# Don't build with Python support unless requested
CONFIGURE_ARGS=		--sysconfdir=${PREFIX}/share/ \
			--with-lzma=/usr \
			--${LIBXML2_SLAVE:Dwith:Uwithout}-python${LIBXML2_SLAVE:D=${PYTHON_CMD}:U}

OPTIONS_DEFINE=	DOCS ICU MEM_DEBUG READLINE STATIC THREAD_ALLOC
OPTIONS_DEFAULT=	READLINE STATIC
OPTIONS_SUB=		yes

MEM_DEBUG_DESC=		Memory debugging (DEVELOPERS ONLY!)
READLINE_DESC=		History for xmllint
THREAD_ALLOC_DESC=	Per-thread memory (DEVELOPERS ONLY!)

ICU_LIB_DEPENDS=		libicudata.so:devel/icu
ICU_CONFIGURE_WITH=		icu
MEM_DEBUG_CONFIGURE_WITH=	mem-debug
READLINE_LIB_DEPENDS=		libreadline.so:devel/readline
READLINE_CONFIGURE_WITH=	history \
				readline
STATIC_CONFIGURE_ENABLE=	static
THREAD_ALLOC_CONFIGURE_WITH=	thread-alloc

post-patch:
.for f in catalog.c xmlcatalog.c xmllint.c doc/xmllint.1
	@${REINPLACE_CMD} -e \
		's|/etc/xml/catalog|${LOCALBASE}/share/xml/catalog|g; \
		 s|/etc/sgml/catalog|${LOCALBASE}/share/sgml/catalog|g' \
		${WRKSRC}/${f}
.endfor

.if !defined(LIBXML2_SLAVE)
post-install:
# Documentation should be in DOCSDIR
	@${MV} ${STAGEDIR}${PREFIX}/share/gtk-doc/html/libxml2 \
		${STAGEDIR}${DOCSDIR}/devhelp
	@${RM} -r ${STAGEDIR}${PREFIX}/share/gtk-doc
# Install remaining documentation that's not connected to autotools
	${INSTALL_MAN} ${WRKSRC}/doc/*.html ${STAGEDIR}${DOCSDIR}
.endif

.include <bsd.port.mk>
