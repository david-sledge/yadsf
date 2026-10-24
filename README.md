# YADSF
**Y**et **A**nother **D**ata **S**erialization **F**ormat (syllables of the acronym rhyme with "fraud" and "clef") is a compact serialization specification inspired by [MessagePack](https://github.com/msgpack/msgpack).

## Why?

Having fixed-length data does not lend well to streaming/incremental serialization and deserialization. With the MessagePack, the size of the data is in the beginning of the data structure, so it requires knowing the size before serializing and sending the data which requires holding the entire data in memory or a persistence layer. With the exception of the binary data type, data structures in YADSF have terminators instead of specifying the size up front.

## No, I mean why use this instead of a human-readable format like JSON or YAML?

See [msgpack.org](http://msgpack.org/) website for the answer to that particular question.
