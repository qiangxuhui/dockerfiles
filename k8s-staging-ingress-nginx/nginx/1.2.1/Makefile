# This file is generated by the template.

REGISTRY?=cr.loongnix.cn
ORGANIZATION?=k8s-staging-ingress-nginx
REPOSITORY?=nginx
TAG?=1.2.1
LATEST?=true

IMAGE=$(REGISTRY)/$(ORGANIZATION)/$(REPOSITORY):$(TAG)
LATEST_IMAGE=$(REGISTRY)/$(ORGANIZATION)/$(REPOSITORY):latest

# SOURCE_URL is a url to download source, such as https://github.com/merore/merore.git.
# SOURCE is project sources, its located at src/$(SORUCE).
# PATCH is a patch that supports loong64 to $(SOURCE).
# Be sure to fill in the follows!!!
SOURCE_URL=https://github.com/kubernetes/ingress-nginx.git
SOURCE=$(shell echo $(SOURCE_URL) | awk -F '/' '{print $$NF}' | awk -F '.' '{print $$1}')
PATCH=0001-port-to-loong64.patch

default: image

image: src/$(SOURCE)
# Commands for building.
	TAG=$(TAG) \
	REGISTRY=$(REGISTRY)/$(ORGANIZATION) \
	$(MAKE) -C $</images/nginx build

src/$(SOURCE):
	git clone -b controller-v$(TAG) --depth=1 $(SOURCE_URL) $@
	cd $@ && \
		git apply ../../$(PATCH)

push:
	docker push $(IMAGE)
	@if [ $(LATEST) = "true" ]; \
		then\
		docker tag $(IMAGE) $(LATEST_IMAGE); \
		docker push $(LATEST_IMAGE); \
	fi

clean:
	rm -rf src
