aqmon
-----

DIY indoor air quality monitor

# Building

```
dnf install arm-none-eabi-gcc arm-none-eabi-newlib
ln -s ../libopencm3
```

# Flashing

```
sudo openocd -c "bindto 0.0.0.0" -f rpi1.cfg -c "transport select swd" -c "adapter speed 1000" -f target/stm32f1x.cfg
```

```
program firmware.elf verify reset
```

# Raspberry Pi configuration

Uncomment this line in `/boot/config.txt`:

```
dtparam=spi=on
```

Note: This will automatically expose `spi0.0` and `spi0.1` under `/sys/bus/spi/devices/`
and they will be bound by default to the `spidev` driver. No manual configuration is
needed. This is because the `spidev` driver is patched in the Raspberry Pi kernel to
accept a `compatible = "spidev"` Device Tree binding and suppress the notorious warning
about the binding. The devices are defined in `arch/arm/boot/dts/bcm2708-rpi-*`, for
example: `arch/arm/boot/dts/bcm2708-rpi-zero-w.dts`.
