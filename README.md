# AtomVM Playground

This repo shows some basic experiments with AtomVM and ESP-32 devkit-v1.


## Setup AtomVM

First of all, we need to install AtomVM with the command:

```bash
$ esptool.py --chip auto \
--port /dev/tty.usbserial-0001 --baud 115200 \
--before default_reset --after hard_reset write_flash -u \
--flash_mode dio --flash_freq 40m --flash_size detect 0x1000 \
/PATH_TO/AtomVM-esp32-elixir-v0.6.6.img
```

## Deploy

To test the board, we can clone the HelloWorld example with the command: 

```bash
$ git clone https://github.com/atomvm/atomvm_examples
...
$ cd atomvm_examples/elixir/HelloWorld
```

Get the dependencies and compile the project:

```bash
$ mix deps.get
... 
$ mix atomvm.packbeam
```

From there, we can upload the compiled code into the ESP-board by using esptool 

```bash
$ esptool.py --port /dev/tty.usbserial-0001 write_flash 0x250000 /PATH_TO/HelloWorld.avm
```

or ExAtom, in that case set in `mix.exs project` params `flash_offset: 0x250000`, then execute

```bash
$ mix atomvm.esp32.flash --port /dev/tty.usbserial-0001 --baud 115200
```

## References 

- [AtomVM Docs](https://doc.atomvm.org/)
- [AtomVM Examples](https://github.com/atomvm/atomvm_examples)
