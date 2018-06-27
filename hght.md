# Contents

# `hght` File Specification

`hght` files describe the heightmap of the main field and add-on content field.

|   |   |
|:--|--:|
| File Locations | vol/content/Terrain/A/MainField/ |
| Extension | `.hght` |
| Parent Archive | `.hght.sstera` |
| Endianness | Little Endian |

## `hght` File Layout

`hght` files only contain a table of height data. There are 65,536 (256 &times; 256) unsigned short entries in the table.

Each file describes a 256 &times; 256 mesh tile. Each tile has placement data found in `MainField.tscb`.

## Height Map Data

Each entry in the table maps to an `x`, `y` and `z` component. The height or `y` component of each vertex is the value read the from the file.

```c
struct hghtData {
    ushort height;
};
```

| Offset | Length | Type | Description |
|--:|:-:|---|---|
| `0x00` | 2 | Unsigned Short | Vertex `y` component |

`x` and `z` can be calculated, while iterating through the data table:

```c
for (int index = 0; index < 256 * 256; index++) {
    uint x = index % 256;
    uint z = index / 256;
}
```

Note that `z` is expected to be an integer quotient. The `floor` function can be used if integer division is not supported.