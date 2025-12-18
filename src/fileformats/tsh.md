# TSH Files

**TSH** files are a proprietary texture set format used in TTGames LEGO video games to store collections of texture images (DDS) along with crop informations.

Each TSH file usually comes with a `_CONTENTS.TXT` file that contains a hash of each character name.

This format is not officially documented by TTGames. The current understanding comes from community research.

## 📦 Overview

- **File extension:** `.tsh`
- **Category:** Texture set / image container 
- **Used for:** Grouping multiple textures into one file 
- **Official name:** NuTextureSheet

## 🎮 Usage in games

The file format was introduced in [LEGO Batman 3: Beyond Gotham](games/lb3.md) with the initial file version 4. 

Version 5 seems to be indistinguishable from version 4 except the `VTOR` FourCC is missing. 

Version 11 was introduced in [LEGO Star Wars: The Skywalker Saga](games/lsw_ss.md). This format changes slightly, mostly with the lack of Trim information headers and the name is stored as a 16 bit sized string, it's upper case hash and it's regular hash. The texture is also moved into a seperate `.TEXTURE` file pointed to at the end of the file.

## 🛠️ Working with TSH files

To work with TSH files, modders usually extract them into separated image format such as DDS.

### Common workflow:
1. Extract TSH files from the game archives
2. Unpack TSH file to DDS using a dedicated tool
3. Analyze, or edit the resulting image
4. Repack or replace TSH file for modding purposes

## 🔧 Known tools

The following tools are commonly used with TSH files:
- [TTGames Explorer Rebirth](tools/ttgamesexplorerrebirth.md)

## ⚠️ Notes & limitations

- TSH is a proprietary format
- The internal structure is not fully documented
- Some variations may exist between different games or engine versions
- Repack TSH files is not possible

## 🧩 Structure

Texture sheets are loaded through the `Collectibles.txt` file with the function `LoadIconTPage`. `PermLoadCollectionIcons` was also added along with it.
In Version 11, the FourCC is `4CC.RESHTXSH` instead of `4CC.TXSHTXSH`, using the ResourceHeader FourCC.
Each character is loaded by hashing their internal name. The hash is calculated using the 32bit Folwer Noll Vo hash in upper case which looks like this.

```c
uint FNV1UPPER(string text)
{
  uint Hash = 0x811C9DC5;

  foreach (char c in text)
  {
    Hash = Hash * 0x01000193;
    Hash = Hash ^ c.ToUpper();
  }

  return Hash;
}
```

### File Format

The file starts with a ResourceHeader.

| Type | Data |
| -------- | ------- |
| u32 | Blocksize |
| u64 | `4CC.TXSH` |
| u32 | `TXSH` |
| u32 | Version |
| u32 | VTOR (sometimes zeroes) |
| u32 | Number of entries |

Each image header contains cropping information in order to extract icons from the embeded DDS image.

### Version 4 & Version 5

| Type | Data | Description |
| -------- | ------- | ------- |
| Float | MinU | |
| Float | MinV | |	 
| Float | MaxU | |
| Float | MaxV | | 
| u32 | MinX | |
| u32 | MinY | |
| u32 | Width | | 
| u32 | Height | |
| char[4] | FourCC | DXT compression type |
| u32 | TrimTop | |
| u32 | TrimBottom | |
| s32 | TrimRight | Signed integer |
| s32 | TrimLeft | Signed integer |
| u32 | FNVHash | |

At the end of the headers, the DDS image starts.

### Version 11


| Type | Data | Description |
| -------- | ------- | ------- |
| Float | MinU | |
| Float | MinV | |
| Float | MaxU | |
| Float | MaxV | | 
| u32 | MinX | |
| u32 | MinY |  |
| u32 | Width | |
| u32 | Height | |
| String16 | Filename |	|
| u32 | Hash(Upper) | FNV1 (Uppercase) |
| u32 | Hash | FNV1 |

At the end of the headers, there is a String16 with the file path of the `.TEXTURE` file.
