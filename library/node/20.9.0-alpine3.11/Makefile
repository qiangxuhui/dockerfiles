# This file is generated by the template.

REGISTRY?=cr.loongnix.cn
ORGANIZATION?=library
REPOSITORY?=node
TAG?=20.9.0-alpine3.11
LATEST?=true

IMAGE=$(REGISTRY)/$(ORGANIZATION)/$(REPOSITORY):$(TAG)
LATEST_IMAGE=$(REGISTRY)/$(ORGANIZATION)/$(REPOSITORY):latest

default: image

image:
	docker build \
		--build-arg http_proxy=$(http_proxy) \
		--build-arg https_proxy=$(https_proxy) \
		--build-arg no_proxy='alpine.loongnix.cn,pkg.loongnix.cn,cloud.loongnix.cn,goproxy.cn,cloud.loongnix.xa' \
		-t $(IMAGE) \
		.

push:
	docker push $(IMAGE)
	#latest image
	@if [ $(LATEST) = "true" ]; \
		then \
		docker tag $(IMAGE) $(LATEST_IMAGE); \
		docker push $(LATEST_IMAGE); \
	fi
