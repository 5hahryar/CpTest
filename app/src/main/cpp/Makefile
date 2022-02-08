SBINDIR?=/sbin
SHARED_LIBS = y
ifneq ($(SHARED_LIBS),y)
DEFINES+= -DNO_SHARED_LIBS
endif

CC := gcc
HOSTCC ?= $(CC)
DEFINES += -D_GNU_SOURCE
# Turn on transparent support for LFS
DEFINES += -D_FILE_OFFSET_BITS=64 -D_LARGEFILE_SOURCE -D_LARGEFILE64_SOURCE
CCOPTS = -O2
WFLAGS := -Wall -Wstrict-prototypes  -Wmissing-prototypes
WFLAGS += -Wmissing-declarations -Wold-style-definition -Wformat=2

CFLAGS := $(WFLAGS) $(CCOPTS) $(DEFINES) $(CFLAGS)

IPOBJ=ipneigh.o dnet_ntop.o ipx_ntop.o ipx_pton.o libnetlink.o ll_map.o mpls_ntop.o

ALLOBJ=$(IPOBJ)
TARGETS=ip

all: $(TARGETS)

ip: $(IPOBJ)
	$(QUIET_LINK)$(CC) $^ $(LDFLAGS) $(LDLIBS) -o $@

install: all
	install -m 0755 $(TARGETS) $(DESTDIR)$(SBINDIR)

clean:
	rm -f $(ALLOBJ) $(TARGETS)

ifeq ($(SHARED_LIBS),y)
LDFLAGS += -Wl,-export-dynamic
endif
