FROM ubuntu:26.04

ENV ZEPHYR_SDK_INSTALL_DIR=/toolchain/zephyr-sdk-0.17.0
ENV ZEPHYR_TOOLCHAIN_VARIANT=zephyr
ENV HOME=/tmp

RUN apt-get update && apt-get install -y build-essential cmake file git ninja-build python3-dev wget
RUN wget -qO- https://astral.sh/uv/install.sh | UV_INSTALL_DIR=/usr/local/bin sh \
    && uv tool install west \
    && git clone https://github.com/zmkfirmware/zmk.git /toolchain/zmk
WORKDIR /toolchain/zmk
RUN uv init --bare \
    && uv add west pip \
    && uv run west init -l app/ \
    && uv run west update \
    && uv run west zephyr-export \
    && uv run west packages pip --install
RUN uv run west sdk install -t arm-zephyr-eabi --install-base /toolchain
RUN git config --system --add safe.directory /toolchain/zmk/zephyr
