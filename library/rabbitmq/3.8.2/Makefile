# This file is generated by the template.

REGISTRY?=cr.loongnix.cn
ORGANIZATION?=library
REPOSITORY?=rabbitmq
TAG?=3.8.2

IMAGE=$(REGISTRY)/$(ORGANIZATION)/$(REPOSITORY):$(TAG)


default: image

image:
	docker build \
		-t $(IMAGE) \
		.

push:
	docker push $(IMAGE)
