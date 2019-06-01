include $(TOPDIR)/rules.mk

PKG_NAME	:= crosswall
PKG_VERSION	:= 2019-06
PKG_RELEASE	 = testing

include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)/default
	SECTION			:= net
	CATEGORY		:= Network
	TITLE			:= crosswall - traffic diversion
	MAINTAINER		:= xiaofan <xfan1024@live.com>
	DEPENDS			:= +dns-selector
endef

define Package/$(PKG_NAME)
	$(Package/$(PKG_NAME)/default)
endef

define Package/$(PKG_NAME)/description
	traffic diversion from mainland and outland
endef

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/usr/libexec/crosswall
	$(INSTALL_BIN) ./files/usr/libexec/crosswall/add-route-list	$(1)/usr/libexec/crosswall/add-route-list
	$(INSTALL_BIN) ./files/usr/libexec/crosswall/start-dns		$(1)/usr/libexec/crosswall/start-dns
	$(INSTALL_BIN) ./files/usr/libexec/crosswall/stop-dns		$(1)/usr/libexec/crosswall/stop-dns
	$(INSTALL_DATA) ./files/usr/libexec/crosswall/common		$(1)/usr/libexec/crosswall/common
	$(INSTALL_DIR) $(1)/usr/share/crosswall
	gzip < ./files/usr/share/crosswall/dns_rule >			$(1)/usr/share/crosswall/dns_rule.gz
	gzip < ./files/usr/share/crosswall/ip_rule >			$(1)/usr/share/crosswall/ip_rule.gz
	$(INSTALL_DIR) $(1)/etc/hotplug.d/iface
	$(INSTALL_BIN) ./files/etc/hotplug.d/iface/99-crosswall		$(1)/etc/hotplug.d/iface/99-crosswall
	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_DATA) ./files/etc/config/crosswall			$(1)/etc/config/crosswall
endef

define Build/Prepare
	echo
endef

define Build/Compile
	echo
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
