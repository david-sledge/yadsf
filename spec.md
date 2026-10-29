# YADSF Specification

Inspired by [MessagePack](https://msgpack.org).

format name | first byte (in binary) | first byte (in hex) | first byte (in decimal)
:----------- | :---------------------- | :------------------- | :-
positive fixint | 0xxx xxxx | 0x00–0x7f | 0–127
nil | 1000 0000 | 0x80 | 128
sequence end | 1000 0001 | 0x81 | 129
false | 1000 0010 | 0x82 | 130
true | 1000 0011 | 0x83 | 131
uint 8 | 1000 0100 | 0x84 | 132
uint 16 | 1000 0101 | 0x85 | 133
uint 32 | 1000 0110 | 0x86 | 134
uint 64 | 1000 0111 | 0x87 | 135
int 8 | 1000 1000 | 0x88 | 136
int 16 | 1000 1001 | 0x89 | 137
int 32 | 1000 1010 | 0x8a | 138
int 64 | 1000 1011 | 0x8b | 139
float 32 | 1000 1100 | 0x8c | 140
float 64 | 1000 1101 | 0x8d | 141
bin 8 | 1000 1110 | 0x8e | 142
bin 16 | 1000 1111 | 0x8f | 143
bin 32 | 1001 0000 | 0x90 | 144
utf-8 | 1001 0001 | 0x91 | 145
utf-16 be | 1001 0010 | 0x92 | 146
utf-16 le | 1001 0011 | 0x93 | 147
utf-32 be | 1001 0100 | 0x92 | 148
utf-32 le | 1001 0101 | 0x93 | 149
sequence | 1001 0110 | 0x92 | 150
associative sequence | 1001 0111 | 0x93 | 151
*unused* | 1001 1000–1001 1111 | 0x94–0x9f | 152–159
fixbin | 101x xxxx | 0xa0–0xbf | 160–191
negative fixint | 11xx xxxx | 0xc0–0xff | 192–255 (−64–−1)

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

### Strings
The uft formats represent strings encoded in UTF-8, UTF-16 (big endian and little endian), and UTF-32 (big endian and little endian). UTF-8 strings are terminated by 0xc0. UTF-16 strings are terminated by 0xd800 (0x00d8 little endian). UTF-32 strings are terminated by 0x0000d800 (0x00d80000 little endian).

### Sequence
Sequence of any values; numbers, booleans, nil, strings, binary data, sequences, and/or associative sequences. A sequence is terminated with a sequence end byte (see below).

### Associative Sequence
An associative sequence is a series Key/value pairs. Keys and values can be any value pack type: number, boolean, nil, string, binary data, sequence, or associative sequence. An associative sequence is terminated with a sequence end byte (see below).

### Sequence End
Marks the end of the current sequence, or associative sequence. Required. If a sequence end byte occurs after an associative sequence key without a corresponding value, a nil byte is implied for the entry value. Invalid outside of a sequence, or associative sequence.
