default: help

help:
	@echo "To build a bootable container image you first need to create instructlab container images for a particular vendor "
	@echo
	@echo "  - make instruct-amd"
	@echo "  - make instruct-intel"
	@echo "  - make instruct-nvidia"
	@echo "  - make instruct-vllm"
	@echo
	@echo "Once instruct images are created, creat bootc container images"
	@echo
	@echo "  - make bootc-amd"
	@echo "  - make bootc-intel"
	@echo "  - make bootc-nvidia"
	@echo "  - make bootc-vllm"
	@echo
	@echo "If these images are going to be used on a cloud, you might want to add cloud-init."
	@echo
	@echo "  - make cloud-amd"
	@echo "  - make cloud-intel"
	@echo "  - make cloud-nvidia"
	@echo "  - make cloud-vllm"

#
# Create instructlab AI container images
#
.PHONY:
instruct-amd:
	make -C instructlab amd

.PHONY:
instruct-nvidia:
	make -C instructlab nvidia

.PHONY:
instruct: instruct-amd instruct-nvidia

#
# Create bootc container images prepared for AI
#
.PHONY: amd nvidia intel vllm
amd:
	make -C amd-bootc/ bootc
intel:
	make -C intel-bootc/ bootc
nvidia:
	make -C nvidia-bootc/ dtk bootc
vllm:
	make -C vllm/ image

#
# Make Bootc container images preinstalled with cloud-init
#
.PHONY:
cloud-amd:
	make VENDOR=amd -C cloud

.PHONY:
cloud-intel:
	make VENDOR=intel -C cloud

.PHONY:
cloud-nvidia:
	make VENDOR=nvidia -C cloud

.PHONY:
cloud: cloud-amd cloud-intel cloud

clean:
	rm -rf build
