# This file is generated by the template.

REGISTRY?=cr.loongnix.cn
ORGANIZATION?=jaegertracing
REPOSITORY?=jaeger-operator
TAG?=1.22

IMAGE=$(REGISTRY)/$(ORGANIZATION)/$(REPOSITORY):$(TAG)


default: image

image:
	docker build \
		--build-arg http_proxy=$(http_proxy) \
		--build-arg https_proxy=$(https_proxy) \
		-t $(IMAGE) \
		.

push:
	docker push $(IMAGE)
