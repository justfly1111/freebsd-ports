# $FreeBSD$

PORTNAME=	syncthing
PORTVERSION=	1.8.0
PORTREVISION=	1
DISTVERSIONPREFIX=	v
CATEGORIES=	net
MASTER_SITES=	https://github.com/syncthing/syncthing/releases/download/v${PORTVERSION}/
DISTNAME=	${PORTNAME}-source-${DISTVERSIONPREFIX}${PORTVERSION}
DISTFILES=	${DISTNAME}${EXTRACT_SUFX}

MAINTAINER=	swills@FreeBSD.org
COMMENT=	Encrypted file sync tool

LICENSE=	MPL20
LICENSE_FILE=	${WRKSRC}/${PORTNAME}/LICENSE

USES=		go

USE_GITHUB=	nodefault
GH_TUPLE=	lucas-clemente:quic-go:3fa290f:quicgo \
		marten-seemann:qtls-go115:f94d2ad:qtlsgo115

USE_RC_SUBR=	syncthing syncthing-discosrv syncthing-relaysrv syncthing-relaypoolsrv

BINS=		syncthing stdiscosrv strelaysrv strelaypoolsrv

.for x in ${BINS}
PLIST_FILES+=	bin/${x}
.endfor

PORTDOCS=	*

USERS=		syncthing
GROUPS=		syncthing

OPTIONS_DEFINE=	DOCS

NO_WRKSUBDIR=	yes

post-patch:
	${RM} -r ${WRKSRC}/syncthing/vendor/github.com/lucas-clemente/quic-go
	${MV} ${WRKSRC}/quic-go-3fa290f ${WRKSRC}/syncthing/vendor/github.com/lucas-clemente/quic-go
	${MV} ${WRKSRC}/qtls-go115-f94d2ad ${WRKSRC}/syncthing/vendor/github.com/marten-seemann/qtls-go115

do-build:
	@( cd ${WRKSRC}/${PORTNAME} ; \
		${SETENV} ${MAKE_ENV} CGO_ENABLED=0 GOFLAGS="-mod=vendor" go run build.go -version v${PORTVERSION} -no-upgrade build ; \
		${SETENV} ${MAKE_ENV} CGO_ENABLED=0 GOFLAGS="-mod=vendor" go run build.go -version v${PORTVERSION} -no-upgrade build stdiscosrv ; \
		${SETENV} ${MAKE_ENV} CGO_ENABLED=0 GOFLAGS="-mod=vendor" go run build.go -version v${PORTVERSION} -no-upgrade build strelaysrv ; \
		${SETENV} ${MAKE_ENV} CGO_ENABLED=0 GOFLAGS="-mod=vendor" go run build.go -version v${PORTVERSION} -no-upgrade build strelaypoolsrv ; \
		)

do-install:
.for x in ${BINS}
	${INSTALL_PROGRAM} ${WRKSRC}/${PORTNAME}/${x} \
		${STAGEDIR}${PREFIX}/bin/
.endfor
	${MKDIR} ${STAGEDIR}${DOCSDIR}
.for x in AUTHORS LICENSE README.md
	${INSTALL_DATA} ${WRKSRC}/${PORTNAME}/${x} \
		${STAGEDIR}${DOCSDIR}
.endfor

.include <bsd.port.mk>
