# Created by: Daniel Solsona <daniel@ish.com.au>, Guido Falsi <madpilot@FreeBSD.org>
# $FreeBSD: head/sysutils/logstash5/Makefile 437841 2017-04-06 00:40:33Z tj $

PORTNAME=	logstash
PORTVERSION=	5.6.3
CATEGORIES=	sysutils java
MASTER_SITES=	http://artifacts.elastic.co/downloads/logstash/
PKGNAMESUFFIX=	5

MAINTAINER=	tj@FreeBSD.org
COMMENT=	Server-side data ingest and transfomation tool

LICENSE=	APACHE20

RUN_DEPENDS=	${LOCALBASE}/bin/bash:shells/bash

CONFLICTS=	logstash-[0-9]*

USES=		cpe
CPE_VENDOR=	elasticsearch
USE_JAVA=	yes
JAVA_VERSION=	1.8+
JAVA_EXTRACT=	yes
JAVA_RUN=	yes
NO_BUILD=	yes

LOGSTASH_DIR=	${PREFIX}/${PORTNAME}

USE_RC_SUBR=	logstash

LOGSTASH_HOME?=	${PREFIX}/${PORTNAME}
LOGSTASH_RUN?=	/var/run/${PORTNAME}
LOGSTASH_DATA_DIR?=	/var/db/${PORTNAME}

SUB_LIST=	LOGSTASH_DATA_DIR=${LOGSTASH_DATA_DIR} JAVA_HOME=${JAVA_HOME} \
		LOGSTASH_HOME=${LOGSTASH_HOME}

LOGSTASH_BIN_FILES=	  logstash
LOGSTASH_JRUBY_SUBDIR=	  vendor/jruby/bin
LOGSTASH_JRUBY_BIN_FILES=	ast irb jirb jruby jruby.sh rdoc testrb gem \
													jgem jirb_swing jruby.bash jrubyc rake ri
LOGSTASH_JRUBY_BIN_FILES_TO_DELETE= jrubyw.exe jruby.exe
LIBS_TO_DELETE= vendor/jruby/lib/jni/arm-Linux \
								vendor/jruby/lib/jni/i386-Linux \
								vendor/jruby/lib/jni/i386-SunOS \
								vendor/jruby/lib/jni/ppc64-Linux \
								vendor/jruby/lib/jni/ppc64le-Linux \
								vendor/jruby/lib/jni/sparcv9-SunOS \
								vendor/jruby/lib/jni/x86_64-Linux \
								vendor/jruby/lib/jni/x86_64-SunOS
LIBS_TO_STRIP=  vendor/jruby/lib/jni/x86_64-FreeBSD/libjffi-1.2.so

do-install:
	@${FIND} ${WRKSRC} -name '*.bat' -delete
	@${MKDIR} ${STAGEDIR}${ETCDIR}
	@${MKDIR} ${STAGEDIR}${LOGSTASH_RUN}
	@${MKDIR} ${STAGEDIR}${LOGSTASH_DATA_DIR}
	@(cd ${WRKSRC} && ${COPYTREE_SHARE} . ${STAGEDIR}${LOGSTASH_DIR})
	${INSTALL_DATA} ${FILESDIR}/logstash.conf.sample ${STAGEDIR}${ETCDIR}
.for x in ${LOGSTASH_BIN_FILES}
	@${CHMOD} ${BINMODE} ${STAGEDIR}${LOGSTASH_DIR}/bin/${x}
.endfor
.for x in ${LOGSTASH_JRUBY_BIN_FILES_TO_DELETE}
	@${RM} -f ${STAGEDIR}${LOGSTASH_DIR}/${LOGSTASH_JRUBY_SUBDIR}/${x}
.endfor
.for x in ${LOGSTASH_JRUBY_BIN_FILES}
	@${CHMOD} ${BINMODE} ${STAGEDIR}${LOGSTASH_DIR}/${LOGSTASH_JRUBY_SUBDIR}/${x}
.endfor
.for x in ${LIBS_TO_DELETE}
	@${RM} -rf ${STAGEDIR}${LOGSTASH_DIR}/${x}
.endfor

post-install:
.for x in ${LIBS_TO_STRIP}
	@${STRIP_CMD} ${STAGEDIR}${LOGSTASH_DIR}/${x}
.endfor

.include <bsd.port.mk>
