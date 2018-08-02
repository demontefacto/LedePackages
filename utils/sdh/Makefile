include $(TOPDIR)/rules.mk

PKG_NAME:=service-discovery-helper
PKG_VERSION:=20180122

PKG_SOURCE:=${PKG_NAME}.tar.gz
PKG_SOURCE_URL:=http://matrix.ha-vel.cz/packages/
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME).$(PKG_VERSION)

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/sdh-proxy
  SECTION:=net
  CATEGORY:=Network
  TITLE:=Service Discovery Helper
  DEPENDS:=+libpthread +libpcap
endef

define Package/sdh-proxy/description
	proxy for UDP packets
endef

define Build/Compile
	cd $(PKG_BUILD_DIR) ; \
	$(TARGET_CC) $(TARGET_CFLAGS) 
endef

define Package/sdh-proxy/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/sdh-proxy $(1)/usr/bin/
endef

$(eval $(call BuildPackage,sdh-proxy))
