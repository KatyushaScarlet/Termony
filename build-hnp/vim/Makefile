include ../utils/Makefrag

VERSION=9.2.0015

all: download/v$(VERSION).tar.gz
	rm -rf temp build
	mkdir -p temp build
	cd temp && tar xvf ../download/v$(VERSION).tar.gz
	cd temp/vim-$(VERSION) && cat ../../0001-fix-tcsetattr.diff | patch -Np1
	cd temp/vim-$(VERSION) && cat ../../0002-fix-viminfo-gid-check.diff | patch -Np1
	cd temp/vim-$(VERSION) && ./configure --prefix=$(PREFIX) vim_cv_uname_output=Linux --host $(OHOS_ARCH)-unknown-linux-musl --with-tlib=tinfow
	cd temp/vim-$(VERSION) && make -j $(shell nproc) && make install -j $(shell nproc) STRIP=$(OHOS_SDK_HOME)/native/llvm/bin/llvm-strip DESTDIR=$(shell pwd)/build
	mkdir -p ../sysroot
	cp -rfv build/data/app/base.org/base_1.0/. ../sysroot | tee file.lst

download/v$(VERSION).tar.gz:
	mkdir -p download
	cd download && $(WGET) https://github.com/vim/vim/archive/refs/tags/v$(VERSION).tar.gz
