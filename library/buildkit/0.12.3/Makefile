# This file is generated by the template.

REGISTRY?=cr.loongnix.cn
ORGANIZATION?=library
REPOSITORY?=buildkit
TAG?=0.12.3
LATEST?=true

IMAGE=$(REGISTRY)/$(ORGANIZATION)/$(REPOSITORY):$(TAG)
LATEST_IMAGE=$(REGISTRY)/$(ORGANIZATION)/$(REPOSITORY):latest
SOURCE_URL=https://github.com/Loongson-Cloud-Community/buildkit.git
default: image

src:
	git clone -b loongarch64-$(TAG) --depth 1 $(SOURCE_URL) $@

image: src
	cd src/ && docker buildx build \
		--load \
		--build-arg http_proxy=$(http_proxy) \
		--build-arg https_proxy=$(https_proxy) \
		-t $(IMAGE) -f Dockerfile \
		.

push:
	docker push $(IMAGE)
	#latest image
	@if [ $(LATEST) = "true" ]; \
		then \
		docker tag $(IMAGE) $(LATEST_IMAGE); \
		docker push $(LATEST_IMAGE); \
	fi

clean:
	rm -rf src 
