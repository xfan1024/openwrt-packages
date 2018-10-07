include $(TOPDIR)/rules.mk

PKG_NAME:=dns-selector
PKG_VERSION:=2018-10
PKG_RELEASE=$(PKG_SOURCE_VERSION)

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL=https://github.com/xfan1024/dns-selector
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=ead5426c82649e09076a9055a2304d523d28e01d
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION).tar.gz
PKG_MAINTAINER:=xiaofan <xfan1024@live.com>
include $(INCLUDE_DIR)/package.mk

define Package/dns-selector/default
  SECTION:=net
  CATEGORY:=Network
  TITLE:=dns-selector
endef

define Package/dns-selector
  $(Package/dns-selector/default)
  DEPENDS := +libc +boost-program_options +boost-system
ifeq ($(PACKAGE_dns_selector_using_boost_regex),y)
  REGEX_LDFLAGS  = -lboost_regex
  REGEX_CXXFLAGS = -DUSING_BOOST_REGEX=1
  DEPENDS       += +boost-regex
endif
endef

define Package/dns-selector/config
	config PACKAGE_dns_selector_using_boost_regex
		bool "use boost::regex instead of std::regex"
		default n
endef

define Package/dns-selector/install
  $(INSTALL_DIR) $(1)/usr/bin/; \
  $(INSTALL_BIN) $(PKG_BUILD_DIR)/dns-selector $(1)/usr/bin; \
	$(CP) -avT ./files $(1); \

endef



define Build/Compile
  CXX="$(TARGET_CROSS)g++" \
  CXXFLAGS="-std=c++11 -O3 $(REGEX_CXXFLAGS)" \
  LDFLAGS="-s -lboost_system -lboost_program_options $(REGEX_LDFLAGS) -pthread" \
  $(MAKE) -C $(PKG_BUILD_DIR)
endef

$(eval $(call BuildPackage,dns-selector))
