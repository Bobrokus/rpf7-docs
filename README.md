# RPF7 Archive Documentation from my research 🚀
[What's an RPF archive?](https://gtamods.com/wiki/RPF_archive)

## Credits ⭐

- dexyfex for [Codewalker](https://github.com/dexyfex/CodeWalker) (mainly its source code 😉)
- OpenIV Team for [OpenIV](https://openiv.com/)
---
## Legend

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

---

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

If the file is compressed (only tested with .txt files):
- **Flags**: size of the compressed file
- **Size**: size of the original file
