# Copyright 2010-2020, Google Inc.
# All rights reserved.
#
# Redistribution and use in source and binary forms, with or without
# modification, are permitted provided that the following conditions are
# met:
#
#     * Redistributions of source code must retain the above copyright
# notice, this list of conditions and the following disclaimer.
#     * Redistributions in binary form must reproduce the above
# copyright notice, this list of conditions and the following disclaimer
# in the documentation and/or other materials provided with the
# distribution.
#     * Neither the name of Google Inc. nor the names of its
# contributors may be used to endorse or promote products derived from
# this software without specific prior written permission.
#
# THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS
# "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT
# LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR
# A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT
# OWNER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL,
# SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT
# LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE,
# DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY
# THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
# (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
# OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.

# This file is deprecated.
# See the following pages for the latest build instructions.
# - https://github.com/google/mozc/blob/master/docs/build_mozc_for_linux.md
# - https://github.com/google/mozc/blob/master/docs/build_mozc_for_android.md

FROM ubuntu:24.04

# Package installation
## https://docs.docker.com/develop/develop-images/instructions/#apt-get
RUN apt-get update && apt-get install -y \
    ## Common packages for linux build environment
    python3 pkg-config git curl unzip g++ gcc \
    ## Packages for linux desktop version
    libibus-1.0-dev libglib2.0-dev qt6-base-dev libgl-dev \
    ## Packages for misc tools
    nano \
  && rm -rf /var/lib/apt/lists/*

# Working environemnt
ENV HOME /home/mozc_builder
RUN useradd --create-home --shell /bin/bash --base-dir /home mozc_builder
USER mozc_builder
RUN mkdir -p /home/mozc_builder/bin
ENV PATH "${PATH}:/home/mozc_builder/bin"
RUN mkdir -p /home/mozc_builder/work
WORKDIR /home/mozc_builder/work

## Set up bazelisk as bazel
RUN curl -LO https://github.com/bazelbuild/bazelisk/releases/download/v1.25.0/bazelisk-linux-amd64 \
  && mv bazelisk-linux-amd64 /home/mozc_builder/bin/bazelisk \
  && chmod u+x /home/mozc_builder/bin/bazelisk

# check out Mozc source with submodules
RUN mkdir /home/mozc_builder/work/mozc
# COPY --chown=mozc_builder:mozc_builder src/ /home/mozc_builder/work/mozc/src/
RUN git clone https://github.com/google/mozc.git -b master --single-branch --recursive

WORKDIR /home/mozc_builder/work/mozc/src
ENTRYPOINT bash
