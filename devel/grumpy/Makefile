# $FreeBSD$

PORTNAME=	grumpy
PORTVERSION=	0.0.0.2017112101
CATEGORIES=	devel

MAINTAINER=	swills@FreeBSD.org
COMMENT=	Python to Go source code transcompiler and runtime

BROKEN_i386=	constant 2147762812 overflows int
DEPRECATED=	Uses deprecated version of python
EXPIRATION_DATE=	2020-09-15

USE_GITHUB=	yes
GH_ACCOUNT=	google
GH_TAGNAME=	3ec8795

USES=		gmake go:no_targets,run python:2.7 shebangfix
SHEBANG_FILES=	tools/benchcmp tools/coverparse tools/diffrange tools/grumpc
BINARY_ALIAS=	python=${PYTHON_CMD}

.include <bsd.port.options.mk>

.if ${ARCH} == "i386"
PLIST_SUB+=	ARCH=386
.else
PLIST_SUB+=	ARCH=${ARCH}
.endif

do-install:
	cd ${WRKSRC}/build/pkg && ${COPYTREE_SHARE} . ${STAGEDIR}${PREFIX}/go/pkg/
	cd ${WRKSRC}/build/src && ${COPYTREE_SHARE} . ${STAGEDIR}${PREFIX}/go/src/
	cd ${WRKSRC}/build/lib/python${PYTHON_VER}/site-packages && ${COPYTREE_SHARE} . ${STAGEDIR}${PYTHON_SITELIBDIR}
.for bin in benchcmp coverparse diffrange grumpc
	${INSTALL_SCRIPT} ${WRKSRC}/build/bin/${bin} ${STAGEDIR}${PREFIX}/bin/
.endfor

.include <bsd.port.mk>
