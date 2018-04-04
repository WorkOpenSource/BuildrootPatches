#
# Makefile to include Patches into Buildroot sources
#

BR_FOLDER=buildroot
BR_URL=git://git.buildroot.net/buildroot
BRANCH=2017.08

all: compile

$(BR_FOLDER):
ifeq (x$(wildcard $(BR_FOLDER))z,xz)
	git clone --depth=1 --branch $(BRANCH) $(BR_URL) $(BR_FOLDER)
	cd $(BR_FOLDER) && for PATCH in $(wildcard *.patch) ; do \
		echo "Patching $$PATCH..." ; \
		patch -p1 < ../$$PATCH || exit 1 ; \
	done
else
	@echo "Buildroot folder already created."
endif

compile: | $(BR_FOLDER)
	cd $(BR_FOLDER) && $(MAKE) defconfig
	cd $(BR_FOLDER) && $(MAKE)

clean:
	rm -rf $(BR_FOLDER)

.PHONY: all clean compile
