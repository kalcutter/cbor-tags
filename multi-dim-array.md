# Additional CBOR Tags for Multi-dimensional Arrays

## Summary

CBOR tags for multi-dimensional arrays defined in [RFC 8746] only accept element arrays which are either a CBOR array of major type 4, a Typed Array, or a Homogeneous Array. A CBOR protocol, however, may require an array encoding not compatible with these data items. This document registers additional tags for multi-dimensional arrays that accept any semantic array of elements.

### Multi-dimensional Array, Row-Major Order

* Tag: 48
* Data Item: Array (major type 4) of two arrays: one array (major type 4) of dimensions, which are unsigned integers distinct from zero; and one array (either a CBOR array of major type 4, or any tag representing an array) of elements.
* Semantics: Multi-dimensional Array, row-major order (identical to tag 40)

### Multi-dimensional Array, Column-Major Order

* Tag: 1048
* Data Item: Array (major type 4) of two arrays: one array (major type 4) of dimensions, which are unsigned integers distinct from zero; and one array (either a CBOR array of major type 4, or any tag representing an array) of elements.
* Semantics: Multi-dimensional Array, column-major order (identical to tag 1040)

## Motivation

* There are important binary representations not covered by [RFC 8746]. For example, `bfloat16` is widely used and supported by different mainstream processors. However, `bfloat16` cannot be directly represented as a Typed Array.
* Array elements may be encoded in compressed form. This is essential for large arrays where network bandwidth may be a limiting factor.
* It may be useful for a generic decoder to present a multi-dimensional array to the user, regardless whether the decoder is able to decode the array elements. In any case, it may be presented as a multi-dimensional array with known dimensions.

## Alternatives

Instead of defining new tags for multi-dimensional arrays, tags 40 and 1040 could be relaxed to the definitions above. This alternative, if acceptable would be preferred.

[RFC 8746]: https://www.rfc-editor.org/info/rfc8746
