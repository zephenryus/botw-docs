# `grass.extm` File Specification

`grass.extm` files describe the height and color of the main field grass and add-on content field.

|   |   |
|:--|--:|
| File Locations | vol/content/Terrain/A/MainField/ |
| Extension | `.grass.extm` |
| Parent Archive | `.grass.extm.sstera` |
| Endianness | Little Endian |

## `grass.extm` File Layout

Each file contains a 64 \times 64 grid. For each vertex there is 4 bytes of data that describe the height of the grass and color.

## Grass Map Data

Each entry in the water data table is 4 bytes long.

```c
struct grassData {
    unsigned char height;
    unsigned char red;
    unsigned char green;
    unsigned char blue;
};
```

| Offset | Length | Type | Description |
|--:|:-:|---|---|
| `0x00` | 1 | Unsigned Byte | `height` |
| `0x01` | 1 | Unsigned Byte | `r`, red |
| `0x02` | 1 | Unsigned Byte | `g`, green |
| `0x03` | 1 | Unsigned Byte | `b`, blue |

`x` and `z` can be calculated, while iterating through the data table:

```c
for (int index = 0; index < 64 * 64; index++) {
    uint x = index % 64;
    uint z = index / 64;
}
```
