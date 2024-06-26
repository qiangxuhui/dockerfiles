# Copyright 2016 The Kubernetes Authors.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

FROM cr.loongnix.cn/k8s-build-image/debian-base:latest as build

# Install iptables and ebtables packages from buster-backports
RUN apt-get update \
    && apt-get -y --no-install-recommends install \
        iptables \
    && rm -rf /var/lib/apt/lists

# Install other dependencies and then clean up apt caches
RUN clean-install \
    conntrack \
    ipset \
    kmod \
    netbase

# Install iptables wrapper scripts to detect the correct iptables mode
# the first time any of them is run
COPY iptables-wrapper /usr/sbin/iptables-wrapper

RUN update-alternatives \
	--install /usr/sbin/iptables iptables /usr/sbin/iptables-wrapper 100 \
	--slave /usr/sbin/iptables-restore iptables-restore /usr/sbin/iptables-wrapper \
	--slave /usr/sbin/iptables-save iptables-save /usr/sbin/iptables-wrapper
RUN update-alternatives \
	--install /usr/sbin/ip6tables ip6tables /usr/sbin/iptables-wrapper 100 \
	--slave /usr/sbin/ip6tables-restore ip6tables-restore /usr/sbin/iptables-wrapper \
	--slave /usr/sbin/ip6tables-save ip6tables-save /usr/sbin/iptables-wrapper

# we're going to borrow the /go-runner binary in the final image
# dedupe this binary by just copying it from the go-runner image
FROM cr.loongnix.cn/k8s-build-image/go-runner:latest as gorunner

FROM scratch
COPY --from=build / /
COPY --from=gorunner /go-runner /go-runner
