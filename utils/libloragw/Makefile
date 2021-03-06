#
# Copyright (C) 2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=libloragw
PKG_VERSION:=5.0.1
PKG_RELEASE:=3

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://matrix.ha-vel.cz/source/

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

#PKG_BUILD_DEPENDS:=

include $(INCLUDE_DIR)/host-build.mk
include $(INCLUDE_DIR)/package.mk

define Package/libloragw/Default
  TITLE:=Libor Dluhos - lora-gateway package
  URL:=http://www.semtech.com/wireless-rf/lora.html
endef

define Package/libloragw
$(call Package/libloragw/Default)
  SECTION:=utils
  CATEGORY:=Network
  SUBMENU:=LoRaWAN
  DEPENDS:=+libmpsse +libftdi
endef

define Package/libloragw/description
  libloragw is a library to build a gateway based on 
  a Libor Dluhos LoRa multi-channel RF receiver (a.k.a. concentrator).
endef

TARGET_CFLAGS += $(FPIC) -O2 -Wall -Wextra -std=c99 -Iinc -I. -lm

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include/libloragw
	$(CP) $(PKG_BUILD_DIR)/libloragw/inc/* $(1)/usr/include/libloragw
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/libloragw/libloragw.a $(1)/usr/lib/
endef

define Package/libloragw/install
	$(INSTALL_DIR) $(1)/root/lora
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/libloragw/test* $(1)/root/lora
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/util_pkt_logger/util_pkt_logger $(1)/root/lora
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/util_tx_continuous/util_tx_continuous $(1)/root/lora
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/util_spi_stress/util_spi_stress $(1)/root/lora
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/util_tx_test/util_tx_test $(1)/root/lora
	$(INSTALL_DIR) $(1)/usr/lib
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/libloragw/libloragw.a $(1)/usr/lib
endef

$(eval $(call BuildPackage,libloragw))
