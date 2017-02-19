KVERSION:= $(shell uname -r)

CONFIG_OPENVSWITCH ?= m

#obj-$(CONFIG_OPENVSWITCH) += openvswitch.o

MOD_NAME = openvswitch
MDIR = kernel/net/openvswitch
obj-$(CONFIG_OPENVSWITCH) := $(MOD_NAME).o
$(MOD_NAME)-objs := actions.o \
        datapath.o \
        dp_notify.o \
        flow.o \
        flow_netlink.o \
        flow_table.o \
        vport.o \
        vport-internal_dev.o \
        vport-netdev.o

ccflags-y := -I$(src)/include
ccflags-y += -DDBG -DRT3298 -DRTBT_IFACE_PCI -DLINUX

MAKE = make
LINUX_SRC ?= /lib/modules/$(shell uname -r)/build
PWD := $(shell pwd)

all:
	$(MAKE) -C $(LINUX_SRC) M=$(PWD) modules

clean:
	$(MAKE) -C $(LINUX_SRC) M=$(PWD) clean

install:
	$(MAKE) INSTALL_MOD_PATH=$(DESTDIR) INSTALL_MOD_DIR=$(MDIR) \
		-C $(LINUX_SRC) M=$(PWD) modules_install
	depmod -a
	#three lines commented for dkms arch linux package: it autoinstalls the module
	#install -m 0755 -o root -g root  rtsx_pci.ko $(DESTDIR)/lib/modules/$(shell uname -r)/kernel/drivers/mfd/
	#install -m 0755 -o root -g root tools/rtbt $(DESTDIR)/usr/bin/
