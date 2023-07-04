CONDA_USERNAME=molinerislab

PACKAGE=$(shell [ -f package/name ] && cat package/name)

.DELETE_ON_ERROR:

package/name:
	mkdir `dirname $@`
	conda-build --output --output-folder package . > $@

$(PACKAGE): package/name
	conda-build --output-folder package . 

build: $(PACKAGE)
	@echo done

platforms: $(PACKAGE)
	mkdir $@
	conda convert --platform all $< -o $@

upload: platforms
	PACKAGE_NAME=$$(basename $(PACKAGE));\
	anaconda login;\
	anaconda upload --user $(CONDA_USERNAME) package/linux-64/$$(PACKAGE_NAME);\
	anaconda upload --user $(CONDA_USERNAME) package/linux-32/$$(PACKAGE_NAME);\
	anaconda upload --user $(CONDA_USERNAME) package/linux-aarch64/$$(PACKAGE_NAME);\
	anaconda upload --user $(CONDA_USERNAME) package/linux-armv6l/$$(PACKAGE_NAME);\
	anaconda upload --user $(CONDA_USERNAME) package/linux-armv7l/$$(PACKAGE_NAME);\
	anaconda upload --user $(CONDA_USERNAME) package/linux-ppc64/$$(PACKAGE_NAME);\
	anaconda upload --user $(CONDA_USERNAME) package/linux-ppc64le/$$(PACKAGE_NAME);\
	anaconda upload --user $(CONDA_USERNAME) package/linux-s390x/$$(PACKAGE_NAME);\
	anaconda upload --user $(CONDA_USERNAME) package/osx-64/$$(PACKAGE_NAME);\
	anaconda upload --user $(CONDA_USERNAME) package/osx-arm64/$$(PACKAGE_NAME);

