include $(TOPDIR)/rules.mk

PKG_NAME		:= kcptun
PKG_VERSION		:= 20181002
PKG_RELEASE		 = $(PKG_SOURCE_VERSION)
PKG_HASH		 = $(PKG_HASH_$(PKG_VERSION)_$(BINARY_ARCH_URL))

PKG_SOURCE_URL				= https://github.com/xtaci/kcptun/releases/download/v$(PKG_VERSION)
PKG_SOURCE					= kcptun-linux-$(BINARY_ARCH_URL)-$(PKG_VERSION).tar.gz
UNPACK_CMD					= mkdir "$(1)/" -p && tar -C "$(1)/" -xf "$(DL_DIR)/$(PKG_SOURCE)"

PKG_HASH_20181002_386		:= 341d49764fa50f8df45c173565a69abe1c65b7b6b12f0574ad39c8920ff3d98a
PKG_HASH_20181002_amd64		= 3d0fad12ba5222888b71a6335a73795d79cbd1a82f1abdaa65e98f6a72520164
PKG_HASH_20181002_arm		:= 078c840095a5607b5b8a2025c6d140746d3631abc13a60eb495bb8950f16b806
PKG_HASH_20181002_mips		:= 2a50a642bdd4a9eedbf01d30a39cd0fb6fd3b05efb1eaed00346fb69db51ed34
PKG_HASH_20181002_mipsle	:= 25d08bdf1a98b3d31cb3b6769313a2cbea908b3b532a0624ff621ff015f47066

ifeq ($(CONFIG_KCPTUN_DEFAULT_ARCH),y)
	ifeq ($(CONFIG_x86_64),y)
		CONFIG_KCPTUN_ARCH_X86_64	:= y
	else
	ifeq ($(CONFIG_i386),y)
		CONFIG_KCPTUN_ARCH_X86		:= y
	else
	ifeq ($(CONFIG_mips),y)
		CONFIG_KCPTUN_ARCH_MIPS		:= y
	else
	ifeq ($(CONFIG_mipsel),y)
		CONFIG_KCPTUN_ARCH_MIPSLE	:= y
	else
	ifeq ($(CONFIG_arm_v7),y)
		CONFIG_KCPTUN_ARCH_ARM7		:= y
	else
	ifeq ($(CONFIG_arm_v6),y)
		CONFIG_KCPTUN_ARCH_ARM6		:= y
	else
	ifeq ($(CONFIG_arm),y)
		CONFIG_KCPTUN_ARCH_ARM5		:= y
	endif
	endif
	endif
	endif
	endif
	endif
	endif
endif

ifeq ($(CONFIG_KCPTUN_ARCH_X86),y)
	BINARY_ARCH_URL := 386
else
ifeq ($(CONFIG_KCPTUN_ARCH_X86_64),y)
	BINARY_ARCH_URL := amd64
else
ifeq ($(CONFIG_KCPTUN_ARCH_ARM5),y)
	BINARY_ARCH_URL := arm
	BINARY_ARCH_FILENAME := arm5
else
ifeq ($(CONFIG_KCPTUN_ARCH_ARM6),y)
	BINARY_ARCH_URL := arm
	BINARY_ARCH_FILENAME := arm6
else
ifeq ($(CONFIG_KCPTUN_ARCH_ARM7),y)
	BINARY_ARCH_URL := arm
	BINARY_ARCH_FILENAME := arm7
else
ifeq ($(CONFIG_KCPTUN_ARCH_MIPS),y)
	BINARY_ARCH_URL := mips
else
ifeq ($(CONFIG_KCPTUN_ARCH_MIPSLE),y)
	BINARY_ARCH_URL := mipsle
endif
endif
endif
endif
endif
endif
endif


ifeq ($(BINARY_ARCH_FILENAME),)
	BINARY_ARCH_FILENAME = $(BINARY_ARCH_URL)
endif

include $(INCLUDE_DIR)/package.mk

define Package/kcptun/default
	SECTION		:= net
	CATEGORY	:= Network
	TITLE		:= kcptun
	MAINTAINER	:= xiaofan <xfan1024@live.com>
endef

define Package/kcptun
	$(Package/kcptun/default)
endef

define Package/kcptun/config
	menu "kcptun options"
		depends on PACKAGE_kcptun
		config KCPTUN_CLIENT
			bool "client"
			default y
		config KCPTUN_SERVER
			bool "server"
			default n
		config KCPTUN_DEFAULT_ARCH
			bool "auto choice binary arch"
			default y
			depends on x86_64 || i386 || mips || mipsel || arm
		choice
			prompt "Binary ARCH"
			depends on !KCPTUN_DEFAULT_ARCH
			default KCPTUN_ARCH_ARM5
			help
				Select the binary arch you want
			config KCPTUN_ARCH_X86
				bool "x86"
			config KCPTUN_ARCH_X86_64
				bool "x86-64"
			config KCPTUN_ARCH_ARM5
				bool "arm5"
			config KCPTUN_ARCH_ARM6
				bool "arm6"
			config KCPTUN_ARCH_ARM7
				bool "arm7"
			config KCPTUN_ARCH_MIPS
				bool "mips"
			config KCPTUN_ARCH_MIPSLE
				bool "mipsle"
		endchoice
	endmenu
endef

define Package/kcptun/install
	$(INSTALL_DIR) $(1)/usr/bin
	if [ "$(CONFIG_KCPTUN_CLIENT)" = y ]; then $(CP) "$(PKG_BUILD_DIR)/client_linux_$(BINARY_ARCH_FILENAME)" $(1)/usr/bin/kcptun-client; fi
	if [ "$(CONFIG_KCPTUN_SERVER)" = y ]; then $(CP) "$(PKG_BUILD_DIR)/server_linux_$(BINARY_ARCH_FILENAME)" $(1)/usr/bin/kcptun-server; fi
endef

define Build/Compile
	echo
endef

$(eval $(call BuildPackage,kcptun))
