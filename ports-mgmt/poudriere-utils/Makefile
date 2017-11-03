# Created by: Enrico M. Crisostomo <enrico.m.crisostomo@gmail.com>
# $FreeBSD$

PORTNAME=	poudriere-utils
PORTVERSION=	1.0.0
CATEGORIES=	ports-mgmt
MASTER_SITES=	https://github.com/emcrisostomo/poudriere-utils/releases/download/${PORTVERSION}/
# The package name suffix is only used when testing the port with non-release
# source distributions (which currently use the -current suffix).
# PKGNAMESUFFIX=	-current
DISTNAME=	poudriere-utils-${DISTVERSIONPREFIX}${DISTVERSION}${DISTVERSIONSUFFIX}

MAINTAINER=	enrico.m.crisostomo@gmail.com
COMMENT=	Shell scripts that simplifies the management of Poudriere jails.

LICENSE=	BSD3CLAUSE
#LICENSE_FILE=	${WRKSRC}/LICENSE

# Overriding the fetch command because GitHub currently returns a 302 when
# downloading a file attached to a release.  The only way I know to follow
# the redirection is using wget.
FETCH_DEPENDS=	wget:${PORTSDIR}/ftp/wget

# Using:
#   * -nc: To avoid clobbering an existing file.
#   * --no-check-certificate: To ignore certificate validation, since GitHub
#                             certificate would not be accepted by wget.
FETCH_CMD=	wget
FETCH_BEFORE_ARGS=	-nc --no-check-certificate
DISABLE_SIZE=	yes

GNU_CONFIGURE=	yes

BUILD_DEPENDS=  zsh:${PORTSDIR}/shells/zsh poudriere:${PORTSDIR}/ports-mgmt/poudriere
RUN_DEPENDS=    ${BUILD_DEPENDS}

.include <bsd.port.mk>
