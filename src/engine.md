# Engine

## Sonic R Engine
Sonic R's `.TER` file format (used for collision) is a very early version of the format used in the `NUP` and `PS2-HD` titles, but everything else is unique.

- [Sonic R](https://en.wikipedia.org/wiki/Sonic_R) (Saturn, Windows)

## Nu2 Engine
Whilst all TT-produced mainline console and PC video games from [Crash Bandicoot: The Wrath of Cortex](https://en.wikipedia.org/wiki/Crash_Bandicoot:_The_Wrath_of_Cortex) to [The LEGO Movie 2 Videogame (TLMV2)](games/tlmv2.md) run on the same underlying engine, the engine itself has undergone several iterations over the years.
This page attempts to categorize the engine into several sub-engines and document which games use which versions of the engine.

- [Crash Bandicoot: The Wrath of Cortex](https://en.wikipedia.org/wiki/Crash_Bandicoot:_The_Wrath_of_Cortex)
- [Haven: Call of the King](https://en.wikipedia.org/wiki/Haven:_Call_of_the_King)
- [Finding Nemo](https://en.wikipedia.org/wiki/Finding_Nemo_(video_game))

### PlayStation 2 (PS2) sub-engine
The PS2 Engine was purpose-built for the PlayStation 2, and then ported and modified for use on other platforms.

#### NUP variant
The NUP variant is so named for its usage of `.NUP` files in Lego [LEGO Star Wars: The Video Game (LSW1)](games/lsw1.md) and [LEGO Star Wars II: The Original Trilogy (LSW2)](games/lsw2.md) instead of `.GSC` files like in later titles.
Although listed as the same variant, these games also have vast differences, with [LEGO Star Wars: The Video Game (LSW1)](games/lsw1.md) being much more hard-coded than [LEGO Star Wars II: The Original Trilogy (LSW2)](games/lsw2.md), and [Bionicle Heroes (BionicleHeroes)](games/bionicle_heroes.md) having a significantly different system for loading files and code.

- [LEGO Star Wars: The Video Game (LSW1)](games/lsw1.md) (PS2, Xbox, GameCube, Windows, Mac OS X)
- [The Chronicles of Narnia: The Lion, the Witch and the Wardrobe](https://en.wikipedia.org/wiki/The_Chronicles_of_Narnia:_The_Lion,_the_Witch_and_the_Wardrobe_(video_game)) (PS2, Xbox, GameCube, Windows)
- [LEGO Star Wars II: The Original Trilogy (LSW2)](games/lsw2.md) (Multiplatform)
- [Bionicle Heroes (BionicleHeroes)](games/bionicle_heroes.md) (PS2, Xbox 360, GameCube, Wii, Windows)

#### PS2-HD variant
The oxymoronically named PS2 HD variant is so named because it is technologically similar to the NUP variant of the PS2 sub-engine, but was designed for HD platforms instead (although all games had a Wii release, and [LEGO Indiana Jones: The Original Adventures (LIJ1)](games/lij1.md) and [LEGO Batman: The Videogame (LB1)](games/lb1.md) had PS2 releases). 
It introduced the Enhanced Graphics mode, which uses higher-polygon character models, as well as introduces depth of field in cutscenes and uses complex shadows for all Lego models (although blob shadows still occasionally appear). Complex shadows are filtered in [LEGO Star Wars: The Complete Saga (TCS)](games/tcs.md) and [LEGO Indiana Jones: The Original Adventures (LIJ1)](games/lij1.md), but are unfiltered in [LEGO Batman: The Videogame (LB1)](games/lb1.md), resulting in noticeable aliasing. [LEGO Batman: The Videogame (LB1)](games/lb1.md) also introduced a strong Ambient Occlusion shader, although it suffers from color banding and fringing, and does not take into account vertex normals.
Also referred to as the PC.GHG variant, although this stems from a file nomenclature difference that is only used by the Windows releases. The three Lego games on this sub-variant are commonly referred to by modders as the "holy trinity" of Lego game modding.

- [Transformers: The Game](https://en.wikipedia.org/wiki/Transformers:_The_Game) (PS2, PS3, PSP, Xbox 360, Wii, Windows)
- [LEGO Star Wars: The Complete Saga (TCS)](games/tcs.md) (PS3, Xbox 360, Wii, Windows, Mac OS X)
- [LEGO Indiana Jones: The Original Adventures (LIJ1)](games/lij1.md) (PS2, PS3, PSP, Xbox 360, Wii, Windows, Mac OS X)
- [The Chronicles of Narnia: Prince Caspian](https://en.wikipedia.org/wiki/The_Chronicles_of_Narnia:_Prince_Caspian_(video_game)) (PS2, PS3, Xbox 360, Wii, Windows)
- [LEGO Batman: The Videogame (LB1)](games/lb1.md) (PS2, PS3, PSP, Xbox 360, Wii, Windows, Mac OS X)

### Next-Gen (NXG) sub-engine
When developing [LEGO Indiana Jones 2: The Adventure Continues (LIJ2)](games/lij2.md), Traveler's Tales decided to drop support for the PlayStation 2, and instead focus on pushing the capabilities of seventh-generation hardware. This resulted in a major technological revamp.

#### Creator variant
The Creator variant is so named because both games have a level builder. It also introduced the concept of using a `.CD` file to point to a character's files and replaced the plaintext `CHARS.TXT` with a binary `.APJ` file, much to many modder's chagrin.

- [LEGO Indiana Jones 2: The Adventure Continues (LIJ2)](games/lij2.md) (PS3, Xbox 360, Wii, Windows, Mac OS X)
- [LEGO Harry Potter: Years 1-4 (HP1)](games/hp1.md) (PS3, Xbox 360, Wii, Windows, Mac OS X)

#### Builder variant
The Builder variant is so named because it introduced several folders named BUILDER. It is notable for the usage of a new graphics engine, which introduced more advanced shaders and necessitated capping the console releases' framerates at 30 FPS.

- [LEGO Star Wars III: The Clone Wars (LSW3)](games/lsw3.md) (PS3, Xbox 360, Wii, Windows, Mac OS X)
- [LEGO Pirates of the Caribbean: The Video Game (Pirates)](games/pirates.md) (PS3, Xbox 360, Wii, Windows, Mac OS X)
- [LEGO Harry Potter: Years 5-7 (HP2)](games/hp2.md) (PS3, Xbox 360, Wii, Windows, Mac OS X)

#### Gotham variant
The Gotham variant, named after the hub of [LEGO Batman 2: DC Super Heroes (LB2)](games/lb2.md), is most notable for adding full camera control to (most areas of) the hub world and introducing a separate audio track for voices during cutscenes.

- [LEGO Batman 2: DC Super Heroes (LB2)](games/lb2.md) (PS3, Xbox 360, Wii, Wii U, Windows, Mac OS X)
- [LEGO The Lord of the Rings (LOTR)](games/lotr.md) (PS3, Xbox 360, Wii, Windows, Mac OS X)
- [LEGO City Undercover (LCU)](games/lcu.md) (Wii U)

#### Cinema variant
The Cinema variant is so named because Tt Games decided to make the games more cinematic around this time period. Also referred to as the DX11 variant, due to the API used.

##### DirectX 9 (DX9) sub-variant
The DX9 sub-variant is so named because the Windows versions of the games run under DirectX 9.

- [LEGO Marvel Super Heroes (LMSH1)](games/lmsh1.md) (PS3, Xbox 360, Wii U, Windows, Mac OS X)
- [The LEGO Movie Videogame (TLMV)](games/tlmv.md) (PS3, Xbox 360, Wii U, Windows, Mac OS X)
- [LEGO The Hobbit (Hobbit)](games/hobbit.md) (PS3, Xbox 360, Wii U, Windows, Mac OS X)
- [LEGO Batman 3: Beyond Gotham (LB3)](games/lb3.md) (PS3, Xbox 360, Wii U, Windows, Mac OS X)
- [LEGO Jurassic World (Jurassic)](games/jurassic.md) (PS3, Xbox 360, Wii U, Windows, Mac OS X)
- [LEGO Dimensions (Dimensions)](games/dimensions.md) (PS3, Xbox 360, Wii U)
- [LEGO Worlds (Worlds)](games/worlds.md) (Windows; early betas only)

##### DirectX 11 (DX11) sub-variant
The DX11 sub-variant is so named because the Windows versions of the games run under DirectX 11.

- [LEGO Marvel Super Heroes (LMSH1)](games/lmsh1.md) (PS4, Xbox One)
- [The LEGO Movie Videogame (TLMV)](games/tlmv.md) (PS4, Xbox One)
- [LEGO The Hobbit (Hobbit)](games/hobbit.md) (PS4, Xbox One)
- [LEGO Batman 3: Beyond Gotham (LB3)](games/lb3.md) (PS4, Xbox One, Windows)
- [LEGO Jurassic World (Jurassic)](games/jurassic.md) (PS4, Xbox One, Windows)
- [LEGO Dimensions (Dimensions)](games/dimensions.md) (PS4, Xbox One)
- [LEGO Worlds (Worlds)](games/worlds.md) (Windows; early betas only)
- [LEGO City Undercover (LCU)](games/lcu.md) (PS4, Xbox One, Switch, Windows)

#### TFA variant
The main distinction between the Cinema and TFA variants is that [LEGO Star Wars: The Force Awakens (LSW-FA)](games/lsw_fa.md)-variant games require a patched executable to run with extracted .DAT files. Often lumped together with the Cinema variant in discussion.

##### DirectX 9 (DX9) sub-variant
- [LEGO Marvel's Avengers (LMSH2)](games/lmsh2.md) (PS3, Xbox 360, Wii U, Windows, Mac OS X)
- [LEGO Star Wars: The Force Awakens (LSW-FA)](games/lsw_fa.md) (PS3, Xbox 360, Wii U, Windows, Mac OS X)
- [LEGO Worlds (Worlds)](games/worlds.md) (Windows)

##### DirectX 11 (DX11) sub-variant
- [LEGO Marvel's Avengers (LMSH2)](games/lmsh2.md) (PS4, Xbox One, Windows)
- [LEGO Star Wars: The Force Awakens (LSW-FA)](games/lsw_fa.md) (PS4, Xbox One, Windows)
- [LEGO Harry Potter Collection](games/lhpc.md) (PS4, Xbox One, Switch)
- [LEGO Worlds (Worlds)](games/worlds.md) (PS4, Xbox One, Switch, Windows)
- [The LEGO Ninjago Movie Videogame (NinjagoMovie)](games/ninjago_movie.md)
- [LEGO Marvel Super Heroes 2 (LMSH3)](games/lmsh3.md) (PS4, Xbox One, Switch, Windows, Mac OS X)
- [LEGO The Incredibles (Incredibles)](games/incredibles.md) (PS4, Xbox One, Switch, Windows, Mac OS X)
- [LEGO DC Super-Villains (DCSV)](games/dcsv.md) (PS4, Xbox One, Switch, Windows, Mac OS X)
- [The LEGO Movie 2 Videogame (TLMV2)](games/tlmv2.md) (PS4, Xbox One, Switch, Windows, Mac OS X)

## NTT Engine
NTT (pronounced "entity") is a custom built engine, developed specifically for [LEGO Star Wars: The Skywalker Saga (LSW-SS)](games/lsw_ss.md). As TT Games has announced that future titles are being developed using Unreal Engine, it is unknown whether NTT will be used for any other titles. Additionally, due to The Skywalker Saga's pending (and postponed) release, any technical similarities between NTT and the late Nu2 are yet to be determined.

## Handheld engines
Not much is known about the handheld engines, as they do not have easily disassembled Windows ports. The DS versions of [LEGO Star Wars: The Complete Saga (TCS)](games/tcs.md), [LEGO Indiana Jones: The Original Adventures (LIJ1)](games/lij1.md), and [LEGO Batman: The Videogame (LB1)](games/lb1.md) share an engine, while the GBA versions of [LEGO Star Wars: The Video Game (LSW1)](games/lsw1.md) and [LEGO Star Wars II: The Original Trilogy (LSW2)](games/lsw2.md) uses the same isometric engine developed by Aspire which is different from there fully 3D engine of [LEGO Star Wars II: The Original Trilogy (LSW2)](games/lsw2.md) for DS which in itself is different from the standard TT Fusion engine that is used from [LEGO Star Wars: The Complete Saga (TCS)](games/tcs.md) onwards.

### GBA Engine
- [LEGO Star Wars: The Video Game (LSW1)](games/lsw1.md) (Game Boy Advance)
- [LEGO Star Wars II: The Original Trilogy (LSW2)](games/lsw2.md) (Game Boy Advance)

### Amaze-ing Engine
- [LEGO Star Wars II: The Original Trilogy (LSW2)](games/lsw2.md) (Nintendo DS)

### Fusion Engine
- [LEGO Star Wars: The Complete Saga (TCS)](games/tcs.md) (Nintendo DS)
- [LEGO Indiana Jones: The Original Adventures (LIJ1)](games/lij1.md) (Nintendo DS)
- [LEGO Batman: The Videogame (LB1)](games/lb1.md) (Nintendo DS)
- [LEGO Indiana Jones 2: The Adventure Continues (LIJ2)](games/lij2.md) (Nintendo DS/PSP)
