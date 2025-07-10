include $(TOPDIR)/rules.mk

PKG_NAME:=rmnet-nss
PKG_VERSION:=1.0.0
PKG_RELEASE:=1

include $(INCLUDE_DIR)/kernel.mk
include $(INCLUDE_DIR)/package.mk

define KernelPackage/rmnet-nss
  SECTION:=kernel
  CATEGORY:=Kernel modules
  SUBMENU:=Network Support
  DEPENDS:=@TARGET_qualcommax +kmod-qca-nss-drv
  TITLE:=RMNET NSS interface module
  FILES:=$(PKG_BUILD_DIR)/rmnet_nss.ko
  KCONFIG:=CONFIG_RMNET_DATA=y
  AUTOLOAD:=$(call AutoLoad,42,rmnet-nss)
endef

define KernelPackage/rmnet-nss/Description
RMNET-NSS is the modular interface from the RMNET driver to the NSS driver.
endef


define Build/Compile
	$(KERNEL_MAKE) CROSS_COMPILE="$(TARGET_CROSS)" \
		ARCH="$(LINUX_KARCH)" \
		M="$(PKG_BUILD_DIR)" \
		EXTRA_CFLAGS="-I$(STAGING_DIR)/usr/include/qca-nss-drv \
			     $(EXTRA_CFLAGS)" \
		modules
endef

$(eval $(call KernelPackage,rmnet-nss))
