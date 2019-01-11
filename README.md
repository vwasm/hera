# Hera

Hera is an [vWASM](https://github.com/vwasm/design) virtual machine implemented in C++ conforming to the [Vapory VM API](https://github.com/vaporyco/EIPs/issues/56).

It can be used with [cpp-vapory](https://github.com/vaporyco/cpp-vapory) and perhaps in the future with other implementations through appropriate bindings.

Currently it uses [Binaryen](https://github.com/webassembly/binaryen)'s interpreter for running WebAssembly bytecode and it should be improved to support the [WAVM](https://github.com/AndrewScheidecker/WAVM) as a backend.

## Build options

- `-DHERA_DEBUGGING=ON` will turn on debugging features and messages
- `-DHERA_METERING_CONTRACT=ON` will pass contract creation data through the metering contract residing at 0x00..0a

## Interfaces

Hera implements two interfaces: [EEI](https://github.com/vwasm/design/blob/master/vap_interface.md) and a debugging module.

### Debugging module

- `debug::print32(value: i32)` - print value
- `debug::print64(value: i64)` - print value
- `debug::printMem(offset: i32, len: i32)` - print memory segment as printable characters
- `debug::printMemHex(offset: i32, len: i32)` - print memory segment as hex
- `debug::printStorage(pathOffset: i32)` - print storage value as printable characters
- `debug::printStorageHex(pathOffset: i32)` - print storage value as hex

These are only enabled if Hera is compiled with debugging on.

## Caveats

Although Hera enables the execution of vWASM bytecode, there are more elements to vWASM an Vapory node must be aware of:

- [backwards compatibility](https://github.com/vwasm/design/blob/master/backwards_compatibility.md) provisions
- injecting metering code to vWASM contracts
- transcompiling VVM1 contracts to vWASM if desired

All of the above must be implemented outside of Hera.

## Author(s)

Alex Beregszaszi

## License

MIT
