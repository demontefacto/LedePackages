#
# Copyright (C) 2006-2016 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=cron
PKG_VERSION:=3.0pl1
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://matrix.ha-vel.cz/source
PKG_MD5SUM:=4c64aece846f8483daf440f8e3dd210f

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/kernel.mk

define Package/mcron/Default
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=mCron
  URL:=https://www.gnu.org/software/mcron
endef

define Package/mcron
$(call Package/mcron/Default)
  DEPENDS:=
  MENU:=1
endef

define Package/mcron/description
gnu crond
endef


CONFIGURE_VARS+= \
	CFLAGS="$$$$CFLAGS $(FPIC)" \
	LDFLAGS="$$$$LDFLAGS -lm -lz" \


define Package/mcron/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/crond $(1)/usr/sbin/
endef

$(eval $(call BuildPackage,mcron))
