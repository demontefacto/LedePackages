#
# Copyright (C) 2006-2015 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=keepalived
PKG_VERSION:=1.3.6
PKG_RELEASE:=2

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:= http://www.keepalived.org/software
PKG_MD5SUM:=ff1f0e460bdf8af5b5979715d1b7dfab
PKG_HASH:=c9ceb2896f0d9b634cf5ee86b1a529b1b43b3e9b

PKG_LICENSE:=GPL-2.0+
PKG_LICENSE_FILES:=COPYING
PKG_MAINTAINER:=Ben Kelly <ben@benjii.net>

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/kernel.mk

define Package/keepalived
  SECTION:=net
  CATEGORY:=Network
  TITLE:=Failover and monitoring daemon for LVS clusters
  URL:=http://www.keepalived.org/
  DEPENDS:=+PACKAGE_libnl-genl:libnl-genl +libopenssl +libip4tc +libip6tc +libxtables
endef

define Package/keepalived/description
 Failover and monitoring daemon for Linux Virtual Server (LVS) clusters.
endef

define Package/keepalived/conffiles
/etc/keepalived/keepalived.conf
endef

CONFIGURE_ARGS+= \
	--enable-vrrp \
	--enable-fwmark \
	--enable-sha1 \
	--disable-lvs \
	--disable-lvs-syncd \
	--disable-snmp \
	--disable-debug \
	--disable-profile \
	--with-kernel-dir="$(LINUX_DIR)/$(LINUX_UAPI_DIR)"

MAKE_FLAGS += \
		STRIP="/bin/true" \

define Package/keepalived/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(CP) $(PKG_INSTALL_DIR)/usr/sbin/keepalived $(1)/usr/sbin/
	$(INSTALL_DIR) $(1)/usr/bin
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/genhash $(1)/usr/bin/
	$(INSTALL_DIR) $(1)/etc/keepalived
	$(CP) $(PKG_INSTALL_DIR)/etc/keepalived/keepalived.conf $(1)/etc/keepalived/
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/keepalived.init $(1)/etc/init.d/keepalived
	$(INSTALL_DIR) $(1)/etc/keepalived
	$(INSTALL_BIN) ./files/vmac.sh $(1)/etc/keepalived/vmac.sh
endef

$(eval $(call BuildPackage,keepalived))
