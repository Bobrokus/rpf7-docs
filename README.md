# RPF7 Archive Documentation from my research 🔬
[What's an RPF archive? 🤔](https://gtamods.com/wiki/RPF_archive)

## Why did I create this?
I'm working on my FiveM Mod Manager so I need to figure out how to read RPF files. GTA5 uses RPF7. After getting through multiple rabbit holes, I deduced there is little to none documentation about RPF7. Fortunately, I found out Codewalker has [`RpfFile` class](https://github.com/dexyfex/CodeWalker/blob/f9a3559263f6b87a9ae53b2035e62294ac576f46/CodeWalker.Core/GameFiles/RpfFile.cs#L134) (which was very well documented, thanks). This helped me a lot and it's what I started working off of. I want to dig through the hard part, so other modders/devs don't have to. My goal is to make the documentation as accessible and helpful as possible, so the modding community grows.

### Contribution is highly appreciated! 🙌

## Credits ⭐

- dexyfex for [Codewalker](https://github.com/dexyfex/CodeWalker) - RPF decoder source code 😉
- OpenIV Team for [OpenIV](https://openiv.com/) - Helped me while creating and modifying RPFs 🔧
- WerWolv for [ImHex](https://github.com/WerWolv/ImHex) - Helped me as an amazing tool for reverse engineering 🔎
- [GTAMods Wiki](https://gtamods.com/wiki/RPF_archive) - Great documentation of older RPF versions
---
## Legend ❓

- ❔Uncomfirmed
-  **u8 - u64**: Unsigned integer
-  **i8 - i64**: Signed integer
-  **string**: Array of `char`

## Header

| label           | type         | size |
| :-------------- | :----------- | :--- |
| RPF Version     | u32 / string | 4B   |
| Entry Count     | u32          | 4B   |
| Names Data Size | u32          | 4B   |
| Encryption Type | u32          | 4B   |

**RPF Version** should be "RPF7" (0x52504637)

### Encryption Type

| type |    hex     |  decimal   | string |
| ---- | :--------: | :--------: | :----: |
| None |     0      |     0      |        |
| Open | 0x4E45504F | 1313165391 | "OPEN" |
| AES  | 0x0FFFFFF9 | 268435449  |        |
| NG   | 0x0FEFFFFF | 267386879  |        |

## Entries Data

### Directory Entry

| label             | type | size |
| ----------------- | ---- | ---- |
| Name Offset       | u16  | 2B   |
| Flags❔            | u32❔ | 4B❔  |
| First Entry Index | u32  | 4B   |
| Entry Count       | u32  | 4B   |

### File Entry

| label                  | type | size |
| ---------------------- | ---- | ---- |
| Name Offset            | u16  | 2B   |
| Flags❔                 | u24❔ | 3B❔  |
| Offset (in 512B units) | u24  | 3B   |
| Size                   | u32  | 4B   |

If file is compressed:
- **Flags**: size of the compressed file
- **Size**: size of the original file
