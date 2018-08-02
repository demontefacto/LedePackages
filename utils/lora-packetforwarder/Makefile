#
# Copyright (C) 2017 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=packet-forwarder
PKG_VERSION:=5.0.1
PKG_RELEASE:=2

PKG_BUILD_DIR:=$(BUILD_DIR)/packet-forwarder-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://matrix.ha-vel.cz/source/

include $(INCLUDE_DIR)/package.mk

define Package/packet-forwarder/Default
  TITLE:=Semtech packet-forwarder program
  URL:=https://github.com/Lora-net/packet_forwarder
endef

define Package/packet-forwarder
$(call Package/packet-forwarder/Default)
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=LoRaWAN
  DEPENDS:=+libloragw +librt +libmpsse
endef

define Package/packet-forwarder/description
  A LoRa packet forwarder is a program running on the host of a LoRa gateway
  that forwards RF packets receive by the concentrator to a server through a
  IP/UDP link, and emits RF packets that are sent by the server.
endef

define Package/packet-forwarder-utils
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=LoRaWAN
  TITLE:=Utilities for lora pakcet forwarder
  DEPENDS:=+libloragw +packet-forwarder
endef

CFLAGS += $(FPIC) -O2 -Wall -Wextra -std=c99 -Iinc -I. -lm

define Build/Compile
	$(MAKE) CC=$(TARGET_CC) LGW_PATH=$(BUILD_DIR)/libloragw-5.0.1/libloragw -C $(PKG_BUILD_DIR)
endef

define Package/packet-forwarder/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/lora_pkt_fwd/lora_pkt_fwd $(1)/usr/sbin
#	$(INSTALL_DIR) $(1)/etc/init.d
#	$(INSTALL_BIN) ./files/lora_pkt_fwd.init $(1)/etc/init.d/lora_pkt_fwd
	$(INSTALL_DATA) ./files/global_conf.json $(1)/usr/sbin
	$(INSTALL_DATA) ./files/local_conf.json $(1)/usr/sbin
endef

define Package/packet-forwarder-utils/install
	$(INSTALL_DIR) $(1)/root/lora/packet_forwarder
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/util_ack/util_ack $(1)/root/lora/packet_forwarder
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/util_sink/util_sink $(1)/root/lora/packet_forwarder
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/util_tx_test/util_tx_test $(1)/root/lora/packet_forwarder
endef

$(eval $(call BuildPackage,packet-forwarder))
$(eval $(call BuildPackage,packet-forwarder-utils))
