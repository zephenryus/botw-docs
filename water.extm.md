# `water.extm` File Specification

`water.extm` files describe the water heightmap and the texture of the main field and add-on content field.

|   |   |
|:--|--:|
| File Locations | vol/content/Terrain/A/MainField/ |
| Extension | `.water.extm` |
| Parent Archive | `.water.extm.sstera` |
| Endianness | Little Endian |

## `water.extm` File Layout

Each file contains a 64 \times 64 grid. For each vertex there is 8 bytes of data that describe the height of the mesh, the material type, the surf opacity and flow speed.

## Water Map Data

Each entry in the water data table is 8 bytes long.

```c
struct waterData {
    unsigned short height;
    unsigned short xAxisFlowRate;
    unsigned short zAxisFlowRate;
    unsigned char unk00;
    unsigned char materialIndex;
};
```

| Offset | Length | Type | Description |
|--:|:-:|---|---|
| `0x00` | 2 | Unsigned Short | `height` (Vertex `y` component |
| `0x02` | 2 | Unsigned Short | `xAxisFlowRate`. |
| `0x04` | 2 | Unsigned Short | `zAxisFlowRate`. |
| `0x05` | 1 | Unsigned Byte | `materialIndex + 3`. This may act as a checksum? |
| `0x06` | 1 | Unsigned Byte | `materialIndex` |


`height`, `surf` and `flowSpeed` are stored as unsigned shorts, but seem to map to float values. These can be calculated by dividing by the max size of an unsigned short:

```
32767 / 0xffff = 0.5
```

`height` is furthur multiplied by another constant to get the final height (the constant is unknown at this time).

`x` and `z` can be calculated, while iterating through the data table:

```c
for (int index = 0; index < 64 * 64; index++) {
    uint x = index % 64;
    uint z = index / 64;
}
```

Note that `z` is expected to be an integer quotient. The `floor` function can be used if integer division is not supported.

Flow Rates are calculated as `(flowRate * 2) - 1` and ranges from `-1` to `1`. On the x-axis this changes flow direction from East (`-1`) to West (`+1`) and on the z-axis from North (`-1`) to South (`+1`).

## Material Index

| id | file | name | attribute | attribute_sub | flag | Google Translated |
|--:|:--|:--|:--|:--|:--|:--|
| 0 | Water | 水 | Water | Water | 0 | Water |
| 1 | HotWater | 熱湯 | Water | Water_Hot | 0 | Hot water |
| 2 | Poison | 毒水 | Water | Water_Poison | 0 | Poison water |
| 3 | Lava | 溶岩 | Lava | Lava | 0 | Lava |
| 4 | IceWater | 冷たい水 | Water | Water_Ice | 0 | Cold water |
| 5 | Mud | 泥沼 | Bog | Bog | 0 | Bog |
| 6 | Clear01 | 透明水01 | Water | Water | 0 | Clear water 01 |
| 7 | Sea | 海 | Water | Water | 0 | Ocean |

This data is stored in Terrain.Tex1.bfres