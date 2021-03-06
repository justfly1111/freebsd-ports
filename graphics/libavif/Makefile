# $FreeBSD$

PORTNAME=	libavif
DISTVERSIONPREFIX=	v
DISTVERSION=	0.8.1
PORTREVISION=	1
CATEGORIES=	graphics

PATCH_SITES=	https://github.com/${GH_ACCOUNT}/${GH_PROJECT}/commit/
PATCHFILES+=	274766b5e5a4.patch:-p1 # https://github.com/AOMediaCodec/libavif/pull/270

MAINTAINER=	jbeich@FreeBSD.org
COMMENT=	Library for encoding and decoding .avif files

LICENSE=	BSD2CLAUSE
LICENSE_FILE=	${WRKSRC}/LICENSE

LIB_DEPENDS=	libpng.so:graphics/png

USES=		cmake compiler:c11 jpeg localbase:ldflags pkgconfig
USE_GITHUB=	yes
USE_LDCONFIG=	yes
GH_ACCOUNT=	AOMediaCodec
CMAKE_ON=	AVIF_BUILD_APPS

OPTIONS_DEFINE=	AOM DAV1D GAV1 PIXBUF RAV1E
OPTIONS_DEFAULT=AOM DAV1D PIXBUF
OPTIONS_SUB=	yes

AOM_DESC=		AV1 encoding/decoding via libaom
AOM_LIB_DEPENDS=	libaom.so:multimedia/aom
AOM_CMAKE_BOOL=		AVIF_CODEC_AOM

DAV1D_DESC=		AV1 decoding via libdav1d
DAV1D_LIB_DEPENDS=	libdav1d.so:multimedia/dav1d
DAV1D_CMAKE_BOOL=	AVIF_CODEC_DAV1D

GAV1_DESC=		AV1 decoding via libgav1
GAV1_LIB_DEPENDS=	libgav1.so:multimedia/libgav1
GAV1_CMAKE_BOOL=	AVIF_CODEC_LIBGAV1

PIXBUF_USES=		gnome
PIXBUF_USE=		GNOME=gdkpixbuf2
PIXBUF_CMAKE_BOOL=	AVIF_BUILD_GDK_PIXBUF

RAV1E_DESC=		AV1 encoding via librav1e
RAV1E_LIB_DEPENDS=	librav1e.so:multimedia/librav1e
RAV1E_CMAKE_BOOL=	AVIF_CODEC_RAV1E

.include <bsd.port.mk>
