include $(TOPDIR)/rules.mk

PKG_NAME:=hirkn
PKG_VERSION:=0.2.0
PKG_RELEASE:=1
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE
PKG_MAINTAINER:=danpashin <danypashin@yandex.ru>

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/danpashin/hirkn/tar.gz/v$(PKG_VERSION)?
PKG_HASH:=bab6195e6cc90ea6b9f2973440746e97604dd12618b26f94b53c75b9d812b894

PKG_BUILD_DEPENDS:=rust/host openssl

include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/rust/rust-package.mk

define Package/hirkn
  SECTION:=net
  CATEGORY:=Network
  TITLE:=RKN bypass utility
  DEPENDS:=$(RUST_ARCH_DEPENDS) +libopenssl +nftables-json
endef

define Package/hirkn/conffiles
/etc/hirkn/config.yaml
endef

define Package/hirkn/description
RKN bypass utility
endef

define Package/hirkn/install
	$(INSTALL_DIR) $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/bin/* $(1)/usr/bin/

	$(INSTALL_DIR) $(1)/etc/init.d/
	$(INSTALL_BIN) ./files/hirkn.init $(1)/etc/init.d/hirkn

	$(INSTALL_DIR) $(1)/etc/hirkn/
	$(INSTALL_DATA) ./files/hirkn.config $(1)/etc/hirkn/config.yaml.example
endef

$(eval $(call RustBinPackage,hirkn))
$(eval $(call BuildPackage,hirkn))
