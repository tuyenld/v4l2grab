Config.in
==========
config BR2_PACKAGE_MPK
	bool "Raspberry Pi helloword"
	select BR2_PACKAGE_LIBJPEG
	help
	  Helloworld

	  https://github.com/twam/v4l2grab



mpk.mk
==========
################################################################################
#
# My package
#
################################################################################

# cp ~/develop/buildroot/output/build/libjpeg-9d/.libs/libjpeg.so.9 /media/ldtuyen/4d8ee9e5-7438-4447-8979-27008eeeb594/usr/lib/ 
# ~/develop/buildroot$ make mpk-rebuild


MPK_VERSION = f8d8844d52387b3db7b8736f5e86156d9374f781
# MPK_SITE = git://github.com/kristjanvalur/soft-hwclock.git
MPK_SITE = git://github.com/twam/v4l2grab.git
MPK_LICENSE = MIT
MPK_LICENSE_FILES = LICENSE
MPK_DEST_DIR = /opt/mpk
MPK_SITE_METHOD = git
MPK_DEPENDENCIES = libjpeg # libjpeg will be compiled
MPK_AUTORECONF = YES 	   # ./autogen.sh, ./configure, make


# 	gcc v4l2grab.c -o v4l2grab -Wall -ljpeg -DIO_READ -DIO_MMAP -DIO_USERPTR
# $(MAKE) CXX="$(TARGET_CXX)" CC="$(TARGET_CC)" LD="$(TARGET_LD)" -C $(@D)

define MPK_BUILD_CMDS
	$(MAKE) CXX="$(TARGET_CXX)" CC="$(TARGET_CC)" LD="$(TARGET_LD)" -C $(@D)
endef

# $(eval $(generic-package))
$(eval $(autotools-package))
