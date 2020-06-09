TARGET := $(shell find * -maxdepth 0 -type d -name propellergcc\*)

all: $(TARGET)

.PHONY: $(TARGET)

$(TARGET):
	@echo $@
	# Loader
	rm $@/target -rf
	rsync -R -avh --ignore-errors --include-from='include-list.txt' --exclude='*' $@/./* $@/target
	sed 's/toolchain-propeller/tool-propeller-load/g' $@/package.json > $@/target/package.json
	cd $@/target && tar czf ../../$(subst propellergcc,loader,$@).tar.gz *

	# Toolchain
	rm $@/target -rf
	rsync -R -avh --ignore-errors --exclude-from='exclude-list.txt' --include='*' $@/./* $@/target
	cd $@/target && tar czf ../../$(subst propellergcc,toolchain,$@).tar.gz *

