include $(TOPDIR)/rules.mk

PKG_NAME:=ufp
PKG_VERSION:=0.0.1
PKG_RELEASE:=2

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/blogic/ufp.git
PKG_SOURCE_VERSION:=4536dd8e3719b2898f6fc7e24f60e8e3c1631193
PKG_MIRROR_HASH:=c8be2279f8630990f9e49b697c95733711fc1d691145a0d6926c6d5a70dbedfb

PKG_LICENSE:=GPL-2.0
PKG_MAINTAINER:=Felix Fietkau <nbd@nbd.name>

HOST_BUILD_DEPENDS:=ucode/host libubox/host
PKG_BUILD_DEPENDS:=ufp/host

CMAKE_SOURCE_SUBDIR:=src

include $(INCLUDE_DIR)/host-build.mk
include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/ufp
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=Device fingerprinting daemon
  DEPENDS:=+ucode +ucode-mod-fs +ucode-mod-struct +libubox +unetmsg
endef

define Build/Prepare
	$(Build/Prepare/Default)
	chmod +x $(PKG_BUILD_DIR)/scripts/convert-devices.uc
	$(Build/Patch)
endef

CMAKE_HOST_OPTIONS += \
	-DCMAKE_SKIP_RPATH=FALSE \
	-DCMAKE_INSTALL_RPATH="${STAGING_DIR_HOST}/lib"

define Package/ufp/install
	$(INSTALL_DIR) $(1)/usr/lib/ucode \
		$(1)/usr/share/ufp/db \
		$(1)/usr/sbin \
		$(1)/etc/init.d

	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/lib/ucode/uht.so \
		$(1)/usr/lib/ucode/

	$(INSTALL_DATA) $(PKG_BUILD_DIR)/plugins/* \
		$(1)/usr/share/ufp/

	$(INSTALL_DATA) $(PKG_BUILD_DIR)/modules/*.uc \
		$(1)/usr/share/ufp/

	$(INSTALL_BIN) ./files/etc/init.d/ufp \
		$(1)/etc/init.d/ufp

	$(INSTALL_BIN) $(PKG_BUILD_DIR)/ufpd $(1)/usr/sbin/ufpd

	$(UCODE) $(PKG_BUILD_DIR)/scripts/convert-devices.uc \
		$(1)/usr/share/ufp/devices.bin \
		$(PKG_BUILD_DIR)/data/*.json

	$(UCODE) $(PKG_BUILD_DIR)/scripts/convert-devices.uc \
		$(1)/usr/share/ufp/db/oui.bin \
		$(PKG_BUILD_DIR)/modules/oui.json
endef

$(eval $(call BuildPackage,ufp))
$(eval $(call HostBuild))
