# YADSF Specification

Inspired by [MessagePack](https://msgpack.org).

format name | first byte (in binary) | first byte (in hex) | first byte (in decimal)
:----------- | :---------------------- | :------------------- | :-
positive fixint | 00xx xxxx | 0x00–0x3f | 0–63
nil | 0100 0000 | 0x40 | 64
sequence end | 0100 0001 | 0x41 | 65
false | 0100 0010 | 0x42 | 66
true | 0100 0011 | 0x43 | 67
uint 8 | 0100 0100 | 0x44 | 68
uint 16 | 0100 0101 | 0x45 | 69
uint 32 | 0100 0110 | 0x46 | 70
uint 64 | 0100 0111 | 0x47 | 71
int 8 | 0100 1000 | 0x48 | 72
int 16 | 0100 1001 | 0x49 | 73
int 32 | 0100 1010 | 0x4a | 74
int 64 | 0100 1011 | 0x4b | 75
float 32 | 0100 1100 | 0x4c | 76
float 64 | 0100 1101 | 0x4d | 77
bin 8 | 0100 1110 | 0x4e | 78
bin 16 | 0100 1111 | 0x4f | 79
bin 32 | 0101 0000 | 0x50 | 80
string | 0101 0001 | 0x51 | 81
sequence | 0101 0010 | 0x52 | 82
associative sequence | 0101 0011 | 0x53 | 83
*unused* | 0101 0100–0101 1111 | 0x54–0x5f | 84–95
fixbin | 011x xxxx | 0x60–0x7f | 96–127
negative fixint | 1xxx xxxx | 0x80–0xff | 128–255 (−128–−1)

## Value Formats
### Primitives
#### Nil
This is a unit type. It is bottom for the specification.

#### Boolean
Binary value of true or false.

#### Numbers
##### Integers
Signed integers of up to 8 bytes.

##### Floating Points
Single and double precision.

### Bin
This represents raw binary data. Fixbin, bin 8, 16, and 32.

### String
This represents a UTF-8 string. Terminated by 0xc0.

### Sequence
Sequence of any values; numbers, booleans, nil, strings, binary data, sequences, and/or associative sequences. A sequence is terminated with a sequence end byte (see below).

### Associative Sequence
An associative sequence is a series Key/value pairs. Keys and values can be any value pack type: number, boolean, nil, string, binary data, sequence, or associative sequence. An associative sequence is terminated with a sequence end byte (see below).

### Sequence End
Marks the end of the current sequence, or associative sequence. Required. If a sequence end byte occurs after an associative sequence key without a corresponding value, a nil byte is implied for the entry value. Invalid outside of a sequence, or associative sequence.
