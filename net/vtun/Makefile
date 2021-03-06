#
# Copyright (C) 2006-2009 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=vtun
PKG_VERSION:=3.0.2
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=@SF/vtun
PKG_MD5SUM:=d3d8bc4d58886498a1c338670eab9315

include $(INCLUDE_DIR)/package.mk

define Package/vtun
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+kmod-tun +liblzo +libopenssl
  TITLE:=VPN tunneling daemon
  URL:=http://vtun.sourceforge.net
  SUBMENU:=VPN
endef

define Package/vtun/conffiles
/etc/vtund.conf
endef

CONFIGURE_ARGS += \
	--with-lzo-headers="$(STAGING_DIR)/usr/include/lzo" \
	--with-lzo-lib="$(STAGING_DIR)/usr/lib/" \
	--with-ssl-headers="$(STAGING_DIR)/usr/include/openssl" \

CONFIGURE_VARS += \
	LIBS="$(TARGET_LDFLAGS)" \
	BLOWFISH_HDR_DIR="$(STAGING_DIR)/usr/include/openssl" \
	LZO_HDR_DIR="$(STAGING_DIR)/usr/include/lzo" \
	SSL_HDR_DIR="$(STAGING_DIR)/usr/include/openssl" \

define Build/Compile
	$(call Build/Compile/Default,vtund)
endef

define Package/vtun/install
	$(INSTALL_DIR) $(1)/etc
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/vtund.conf $(1)/etc/
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/vtund $(1)/usr/sbin/
endef

$(eval $(call BuildPackage,vtun))
