include $(TOPDIR)/rules.mk

PKG_NAME:=qosmate
PKG_VERSION:=1.7.0
PKG_RELASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/hudra0/qosmate.git
PKG_MIRROR_HASH:=adb4cd8e35777900544603b0e0f1900ec4a449e5a190f724153c9d1bcb939f46
PKG_SOURCE_DATE:=2025-10-21
PKG_SOURCE_VERSION:=05426f3a06312ae7c822d9cdf0badbc8e0c8fbfe
PKG_MIRROR_HASH:=adb4cd8e35777900544603b0e0f1900ec4a449e5a190f724153c9d1bcb939f46

PKG_MAINTAINER:=Markus Hütter <mh@hudra.net>
PKG_LICENSE:=GPL-3.0-or-later

include $(INCLUDE_DIR)/package.mk

define Package/qosmate
  SECTION:=net
  CATEGORY:=Base system
  TITLE:=QoSmate - Quality of Service management tool
  DEPENDS:=+kmod-sched +ip-full +kmod-veth +tc-full +kmod-netem +kmod-sched-ctinfo +kmod-ifb +kmod-sched-cake +kmod-sched-red
endef

define Package/qosmate/description
  QoSmate is a Quality of Service management tool for OpenWrt
endef

define Package/qosmate/conffiles
/etc/config/qosmate
endef

define Package/qosmate/install
	$(INSTALL_DIR) $(1)/etc
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_DIR) $(1)/etc/hotplug.d/iface
	$(INSTALL_DIR) $(1)/etc/config

	$(INSTALL_BIN) $(PKG_BUILD_DIR)/etc/qosmate.sh $(1)/etc/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/etc/init.d/qosmate $(1)/etc/init.d/
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/etc/hotplug.d/iface/13-qosmateHotplug $(1)/etc/hotplug.d/iface/
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/etc/config/qosmate $(1)/etc/config/
endef

$(eval $(call BuildPackage,qosmate))
