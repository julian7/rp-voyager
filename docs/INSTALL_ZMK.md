# ZMK firmware for RP-Voyager

## Install native ZMK toolchain

```shell
brew install uv cmake ninja gperf python3 python-tk ccache qemu dtc libmagic wget openocd
uv tool install west
git clone https://github.com/zmkfirmware/zmk.git ~/src/zmk
cd zmk
uv init --bare
uv add west pip
uv run west init -l app/
uv run west update
uv run west zephyr-export
uv run west packages pip --install
uv run west sdk install -t arm-zephyr-eabi
```

## Specifics

The previous snippet assumes MacOS with Homebrew. Follow [Native local toolchain setup](https://zmk.dev/docs/development/local-toolchain/setup/native) guide for your operating system.

It also depends on `uv` so that the environment can be localized into `~/src/zmk`. You'll have to initiate builds from that directory.

## Run in docker

Build the image (eg. `docker build -t zmk firmware`). It will take some time.

## Compile the firmware

- run the build, like: `docker run --rm -ti -v $PWD:/repo zmk uv run west build --source app --board rp_voyager_left/rp2350a/m33 --build-dir /repo/build2/left --pristine -- -DZEPHYR_TOOLCHAIN_VARIANT=zephyr -DZMK_EXTRA_MODULES=/repo -DZMK_CONFIG=/repo/config -DKEYMAP_FILE=/repo/config/rp_voyager.keymap`
