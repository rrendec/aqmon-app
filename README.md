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
