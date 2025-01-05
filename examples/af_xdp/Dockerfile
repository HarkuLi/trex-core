ARG UBUNTU_VERSION="22.04"

FROM alpine/git:2.45.2 AS git

RUN git clone -b v3.06 --depth 1 \
        https://github.com/HarkuLi/trex-core.git /trex

FROM ubuntu:${UBUNTU_VERSION} AS builder

RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends \
        build-essential \
        libbpf-dev \
        libmnl-dev \
        libnuma-dev \
        pkg-config \
        python3 \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /trex

COPY --from=git /trex .

RUN cd linux_dpdk \
    && ./b configure \
    && ./b build

FROM ubuntu:${UBUNTU_VERSION} AS app

RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends \
        iproute2 \
        netbase \
        pciutils \
        python3 \
        python3-distutils \
    && rm -rf /var/lib/apt/lists/*

COPY --from=builder /trex/scripts /trex/scripts
COPY --from=builder /trex/linux_dpdk/build_dpdk/linux_dpdk /trex/linux_dpdk/build_dpdk/linux_dpdk

WORKDIR /trex/scripts

ENTRYPOINT [ "./t-rex-64" ]
