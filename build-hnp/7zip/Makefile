include ../utils/Makefrag
VERSION=26.00

all: download/$(VERSION).tar.gz
	rm -rf temp build
	mkdir -p temp build
	cd temp && tar vxf ../download/$(VERSION).tar.gz

	# patch
	cd temp/7zip-$(VERSION)/CPP/7zip && patch -Np1 < ../../../../0001-fix-ohos-build.patch
	
	# build
	cd temp/7zip-$(VERSION)/CPP/7zip/Bundles/Alone2 && make -f ../../cmpl_clang.mak -j $(shell nproc)

	# install
	mkdir -p ../sysroot
	install -v -Dm755 temp/7zip-$(VERSION)/CPP/7zip/Bundles/Alone2/b/c/7zz ../sysroot/bin/7zz

download/$(VERSION).tar.gz:
	mkdir -p download
	cd download && wget -O $(VERSION).tar.gz https://github.com/ip7z/7zip/archive/refs/tags/$(VERSION).tar.gz
