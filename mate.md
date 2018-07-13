# `mate` File Specification

`mate` files describe the material and texture of the main field and add-on content field.

|   |   |
|:--|--:|
| File Locations | vol/content/Terrain/A/MainField/ |
| Extension | `.mate` |
| Parent Archive | `.mate.sstera` |
| Endianness | Little Endian |

## `mate` File Layout

Each file contains a 256&times;256 grid. For each vertex there is 4 bytes of data that describe the material of the heightmap mesh.

## Material Map Data

Each entry in the material data table is 4 bytes long.

```c
struct waterData {
    unsigned char material0;
    unsigned char material1;
    unsigned char blendWeight;
    unsigned char unknown;
};
```

| Offset | Length | Type | Description |
|--:|:-:|---|---|
| `0x00` | 1 | Unsigned Byte | `material0` |
| `0x01` | 1 | Unsigned Byte | `material1` |
| `0x02` | 1 | Unsigned Byte | `blendWeight` |
| `0x03` | 1 | Unsigned Byte | `unknown` |

`material0` and `material1` is an index from the user table in `Terrain.Tex1.bfres` (the table is below).

`x` and `z` can be calculated, while iterating through the data table:

```c
for (int index = 0; index < 256 * 256; index++) {
    uint x = index % 256;
    uint z = index / 256;
}
```

Note that `z` is expected to be an integer quotient. The `floor` function can be used if integer division is not supported.

## Material Index

| id | file | name | attribute | attribute_sub | flag | Google Translated |
|--:|:--|:--|:--|:--|:--|:--|
| 0 | Plant_GreenGrassField_A | 芝生（基本） | Grass | Grass | 0 | Grass (basic) |
| 1 | Rock_NoisyRock_A | ざらざら岩A | Stone | Stone_Light | 0 | Rough rock A |
| 2 | Rock_RedCubeRock_A | ※上書き禁止※ | Stone | Stone | 0 | ※ Overwrite prohibition ※ |
| 3 | Rock_RoughRock_A | 荒れた岩 | Stone | Stone | 0 | Rough rock |
| 4 | Rock_WhiteRock_A | 岩（白）A | Stone | Stone | 0 | Rock (white) A |
| 5 | Sand_BrownSoilAndGrass_A | 土（固め緑色） | Soil | Soil_Hard | 0 | Soil (consolidated green) |
| 6 | Sand_SandBeige_A | 砂（基本） | HeavySand | HeavySand | 0 | Sand (basic) |
| 7 | Sand_SandBeach_A | 砂浜（海岸用）A | Sand | Sand | 0 | Sandy beach (for coast) A |
| 8 | Snow_SnowPowder_A | 雪（平ら） | HeavySnow | HeavySnow | 0 | Snow (flat) |
| 9 | Rock_GravelStone_A | 砂利A | Stone | Stone_Light | 1 | Gravel A |
| 10 | Sand_HardMad_A | 土砂＆岩 | Soil | Soil_Hard | 0 | Earth and rock |
| 11 | Plant_GreenGrassAndMad_A | 芝生＆土 | Grass | Grass_WithMud | 1 | Lawn & earth |
| 12 | Rock_FutagoRock_A | 岩（フタゴ）A | Stone | Stone | 0 | Rock (Futago) A |
| 13 | Floor_StoneTilesAndMoss_A | 石畳＆芝生 | Stone | Stone | 1 | Cobblestones & lawn |
| 14 | Plant_FallenLeafAndGrass_A | 落ち葉A | Grass | Grass_Leaf | 0 | Fallen leaves A |
| 15 | Rock_RockAndGrass_A | 薄い岩＆草 | Stone | Stone | 0 | Thin rock & grass |
| 16 | Rock_LargeCliffAndGrass_A | 崖（白）A＆草 | Grass | Grass_Moss | 0 | Cliff (white) A & grass |
| 17 | Rock_LargeCliff_A | 崖（白）A | Stone | Stone | 0 | Cliff (white) A |
| 18 | Rock_LargeCliff_B | 崖（白）B | Stone | Stone | 0 | Cliff (white) B |
| 19 | Rock_RedRockSoft_A | 岩（赤）A | Stone | Stone | 0 | Rock (red) A |
| 20 | Rock_RoundRockAndSand_A | 丸岩＆砂 | Stone | Stone_Light | 0 | Maruwa & Sand |
| 21 | Rock_OrangeCubeCliff_A | 矩形岩（オレンジ） | Stone | Stone | 0 | Rectangular rock (Orange) |
| 22 | Rock_NoisyRock_B | ざらざら岩B | Stone | Stone_Light | 0 | Rough rock B |
| 23 | Sand_HardSoilRed_A | 土（固め赤色） | Soil | Soil_Hard | 1 | Soil (hardened red) |
| 24 | Sand_FarmMad_A | 土（畑用） | Soil | Soil_Soft | 0 | Sat (for fields) |
| 25 | Sand_HardMadAndStone_A | 土（固め小石混じり） | Soil | Soil | 1 | Soil (compacted pebble) |
| 26 | Plant_GreenGrassAndStone_A | 芝生＆岩 | Grass | Grass | 1 | Lawn & rock |
| 27 | Rock_RoughRock_B | 荒れた赤岩 | Stone | Stone | 0 | Stormy rocks |
| 28 | Sand_LandSlide_A | 土砂A | Soil | Soil_Hard | 0 | Earth and sand A |
| 17 | Rock_LargeCliff_A | ※上書き禁止※ | Stone | Stone | 0 | ※ Overwrite prohibition ※ |
| 18 | Rock_LargeCliff_B | ※上書き禁止※ | Stone | Stone | 0 | ※ Overwrite prohibition ※ |
| 0 | Plant_GreenGrassField_A | 未使用 | Grass | Grass | 0 | unused |
| 29 | Plant_DriedGrassField_A | 芝生（枯れ） | Grass | Grass | 0 | Grass (dead) |
| 30 | Rock_WorldEnd_A | 世界のおわり | Stone | Stone | 1 | The end of the world |
| 31 | Rock_DeathMountain_B | 岩(火山)B | Stone | Stone | 1 | Rock (volcano) B |
| 32 | Rock_DeathMountain_C | 土(固まり・火山) | Soil | Soil | 1 | Sat (mass / volcano) |
| 33 | Snow_SnowBumpy_A | 雪（でこぼこ） | HeavySnow | HeavySnow | 0 | Snow (bumpy) |
| 34 | Sand_BrownSoil_A | 土（茶色） | Soil | Soil_Hard | 1 | Sat (brown) |
| 35 | Sand_SolidSoil_A | 土（固まり） | Soil | Soil_Hard | 1 | Earth (mass) |
| 36 | Plant_FallenLeafAndGrass_B | 落ち葉B | Grass | Grass_Leaf | 0 | Fallen leaves B |
| 37 | Plant_FallenLeafAndGrass_C | 落ち葉C | Grass | Grass_Leaf | 0 | Fallen leaves C |
| 38 | Plant_MossField_A | 苔A | Grass | Grass_Moss | 0 | Moss A |
| 39 | Plant_MossField_B | 苔B | Grass | Grass_Moss | 0 | Moss B |
| 40 | Sand_CrackSoil_A | ひび割れた土 | Soil | Soil_Hard | 0 | Cracked soil |
| 41 | Wall_TerraZoraBridge_A | ゾーラの橋 | Stone | Stone | 0 | Bridge of Solar |
| 42 | Sand_BrownSoilAndStone_A | 小石混じりの土 | Soil | Soil | 0 | Pebbles mixed with pebbles |
| 43 | Rock_GravelStone_B | 砂利B | Stone | Stone_Light | 1 | Gravel B |
| 44 | Sand_GraySoilAndGrass_A | 雑草混じりの砂利 | Stone | Stone_Light | 0 | Gravel mixed with weeds |
| 45 | Rock_HorizontallyCliff_A | 崖（横割れ）A | Stone | Stone | 0 | Cliff (transverse crack) A |
| 46 | Rock_LargeCliffSnow_A | 雪まじりの岩（黒） | Snow | Snow_Shallow | 0 | Snow-rocky rock (black) |
| 47 | Rock_RedRockDark_A | 岩（固まった溶岩） | Stone | Stone | 0 | Rock (hardened lava) |
| 48 | Rock_RockZora_A | ゾーラ岩（青）A | Stone | Stone | 0 | Solar rock (blue) A |
| 49 | Sand_PebblySoil_A | 小石混じり砂（黄）A | Sand | Sand | 0 | Pebble mixed sand (yellow) A |
| 50 | Rock_RockSnow_A | 雪まじりの岩A | Snow | Snow_Shallow | 0 | Snow-rocky rock A |
| 51 | Rock_RockSnow_B | 雪まじりの岩B | Snow | Snow_Shallow | 0 | Snow-rocky rock B |
| 52 | Rock_LargeCliff_C | 雪場用の(黒) | Stone | Stone | 0 | For snow fields (black) |
| 53 | Rock_BeigeRock_A | 岩（ベージュ）A | Stone | Stone | 0 | Rock (beige) A |
| 54 | Sand_RedPebbly_A | 小石混じり砂（赤）A | Sand | Sand | 0 | Pebble mixed sand (red) A |
| 55 | Plant_GreenGrassField_B | 芝生B | Grass | Grass_Moss | 0 | Lawn B |
| 56 | Sand_SandWindPattern_A | 砂紋A | HeavySand | HeavySand | 0 | Sandpaper A |
| 57 | Rock_CliffCheese_A | チーズ岩A | Stone | Stone | 0 | Cheese rock A |
| 58 | Rock_ColorfulRock_A | カラフル岩A | Stone | Stone_Light | 0 | Colorful rock A |
| 59 | Rock_HardBrownStone_A | 固い岩盤A | Stone | Stone_Heavy | 0 | Hard bedrock A |
| 7 | Sand_SandBeach_A | 砂（川岸用）A | Sand | Sand | 0 | Sand (for riverside) A |
| 60 | Wall_TerraZoraWall_A | ゾーラの壁 | Stone | Stone | 0 | Solar Wall |
| 61 | Snow_SnowAndStone_A | 雪＆石肌 | Snow | Snow_Shallow | 0 | Snow & stone skin |
| 62 | Rock_MountainSheiker_A | シーカー岩A | Stone | Stone | 0 | Seeker rock A |
| 63 | Plant_MountainSheiker_A | シーカー苔A | Grass | Grass_Moss | 0 | Seeker Moss A |
| 64 | Rock_TropicalCliff_A | 崖（熱帯）A | Stone | Stone | 0 | Cliff (tropical) A |
| 65 | Plant_TropicalGrass_A | 苔（熱帯）A | Grass | Grass_Moss | 0 | Moss (tropical) A |
| 66 | Rock_RedCubeCliff_A | 矩形岩（赤） | Stone | Stone | 0 | Rectangular rock (red) |
| 67 | Sand_PebblySoil_B | 小石混じり砂（黄）B | Sand | Sand | 0 | Pebble mixed sand (yellow) B |
| 68 | Rock_SeasideRock_A | 崖（海岸）A | Stone | Stone | 0 | Cliff (coast) A |
| 69 | Rock_GravelStone_C | 砂利C | Stone | Stone_Light | 1 | Gravel C |
| 70 | Rock_TropicalLumpRock_A | 岩（熱帯）A | Stone | Stone | 0 | Rock (Tropical) A |
| 71 | Wall_HyliaStoneRoad_A | ハイリア建築石畳 | Stone | Stone_Marble | 0 | Hiria architectural stone pavement |
| 0 | Plant_GreenGrassField_A | 未使用 | Grass | Grass | 0 | unused |
| 72 | Plant_LakeHylia_A | 芝生(ハイリア湖) | Grass | Grass_Moss | 0 | Lawn (Lake Hiriah) |
| 73 | Sand_CrackSoil_B | ひび割れた土B | Stone | Stone_Heavy | 0 | Cracked soil B |
| 74 | Sand_SandBeachAndGrass_A | 砂浜（海岸用・芝）A | Sand | Sand | 0 | Sandy beach (for shore / turf) A |
| 75 | Plant_BlackGrassField_A | 芝（汚染） | Grass | Grass | 0 | Turf (pollution) |
| 76 | Sand_WhiteSoilAndStone_A | 小石混じり砂（白）A | Sand | Sand | 0 | Pebble mixed sand (white) A |
| 77 | Sand_DebriWood_A | 木のガレキ | Wood | Wood | 0 | Wooden garetchi |
| 78 | Sand_DebriStone_A | 石のガレキ土 | Stone | Stone_Heavy | 0 | Rock of stone |
| 79 | Rock_RoughRockMoss_A | 崖（苔)A | Stone | Stone | 0 | Cliff (moss) A |
| 80 | Plant_FallenLeafAndGrass_D | 落ち葉D | Grass | Grass_Leaf | 0 | Fallen leaves D |
| 81 | Plant_FallenLeafCherry_A | 桜落ち葉 | Grass | Grass_Leaf | 0 | Cherry blossoms fallen leaves |
| 82 | Rock_RockBeachCoral_A | 岩（磯)A | Stone | Stone | 0 | Rock (Aso) A |

This data is stored in Terrain.Tex1.bfres