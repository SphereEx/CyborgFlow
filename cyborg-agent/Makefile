# Licensed to the Apache Software Foundation (ASF) under one
# or more contributor license agreements.  See the NOTICE file
# distributed with this work for additional information
# regarding copyright ownership.  The ASF licenses this file
# to you under the Apache License, Version 2.0 (the
# "License"); you may not use this file except in compliance
# with the License.  You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
# If the first argument is "run"...

SHELL := /bin/bash -o pipefail

CYBORG_AGENT_ROOT := $(shell dirname $(realpath $(lastword $(MAKEFILE_LIST))))
CYBORG_AGENT_TAR := cyborg-agent.tar.gz
CYBORG_UPSTREAM_REPO ?= https://github.com/apache/skywalking-java.git
CYBORG_UPSTREAM_HEAD ?= a7a4faabb158ea8322170e3c7cae0210a8c4e7b4

.PHONY: build
build:
	cd plugins && ./mvnw --batch-mode clean package -Dmaven.test.skip=true

.PHONY: replace
replace: build
	bash ./replace-plugins.sh $(path)

.PHONY: release
release:
	bash ./release.sh $(CYBORG_UPSTREAM_REPO) $(CYBORG_UPSTREAM_HEAD) $(CYBORG_AGENT_ROOT)/$(CYBORG_AGENT_TAR)