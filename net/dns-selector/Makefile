include $(TOPDIR)/rules.mk

PKG_NAME	:= dns-selector
PKG_VERSION	:= 2018-10
PKG_RELEASE	 = $(PKG_SOURCE_VERSION)

PKG_SOURCE_PROTO		:= git
PKG_SOURCE_URL			:= https://github.com/xfan1024/dns-selector
PKG_SOURCE_SUBDIR		:= $(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION		:= fa894c2ef26a29ec7e9843849160d18826d97440
PKG_SOURCE				:= $(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION).tar.gz
PKG_MIRROR_HASH			:= 3e48ad79582704ad92493581258afec3b542e131c746cb6505a1e184ed86d31f


include $(INCLUDE_DIR)/package.mk

define Package/dns-selector/default
	SECTION			:= net
	CATEGORY		:= Network
	TITLE			:= DNS Selector
	MAINTAINER		:= xiaofan <xfan1024@live.com>
	DEPENDS			:= +libc +boost +boost-program_options +boost-system
endef

define Package/dns-selector
	$(Package/dns-selector/default)
ifeq ($(PACKAGE_dns_selector_using_boost_regex),y)
	REGEX_LDFLAGS	 = -lboost_regex
	REGEX_CXXFLAGS	 = -DUSING_BOOST_REGEX=1
	DEPENDS			+= +boost-regex
endif
endef

define Package/dns-selector/description
	dispatch dns request to different dns server by rule
endef

define Package/dns-selector/config
	config PACKAGE_dns_selector_using_boost_regex
		depends on PACKAGE_dns-selector
		bool "use boost::regex instead of std::regex"
		default n
endef

define Package/dns-selector/install
	$(INSTALL_DIR) $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/dns-selector $(1)/usr/bin
endef

define Build/Compile
	CXX="$(TARGET_CROSS)g++" \
	CXXFLAGS="-std=c++11 -O3 $(REGEX_CXXFLAGS)" \
	LDFLAGS="-s -lboost_system -lboost_program_options $(REGEX_LDFLAGS) -pthread" \
	$(MAKE) -C $(PKG_BUILD_DIR)
endef

$(eval $(call BuildPackage,dns-selector))
