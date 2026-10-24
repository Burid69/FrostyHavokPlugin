# Building HavokFb

`HavokFb.exe` is a command line around the FrostyHavokPlugin library: it reads and writes Frostbite Havok physics
resources (e.g. Star Wars Battlefront II / Battlefront 2015 group physics).

## Prebuilt

Download `HavokFb-net8.0-win-x64.zip` from the [Releases](../../releases) page, unzip and run it from a command prompt:

    HavokFb.exe --toObj <file>      (Havok physics resource -> OBJ)
    HavokFb.exe --toHavok <file>    (OBJ -> Havok, one convex shape)

Running it without arguments crashes (original behaviour, it reads the first argument without checking).
Needs the [.NET 8 runtime](https://dotnet.microsoft.com/download/dotnet/8.0).

## From source

1. Install the .NET 8 SDK.
2. Clone this repository and the Frosty v2 SDK side by side:

       git clone https://github.com/Burid69/FrostyHavokPlugin.git
       git clone https://github.com/wannkunstbeikor/FrostyToolsuite.git
       git -C FrostyToolsuite checkout 036d3b09d43371154d5ff26f664e661ea151ccc9

3. Build:

       dotnet build FrostyHavokPlugin/build/HavokFb.csproj -c Release

   Output: `FrostyHavokPlugin/build/bin/Release/net8.0/HavokFb.exe`.

The original `HavokFb/HavokFb.csproj` references a project path that is not in the repository, so use `build/HavokFb.csproj`.

## Known behaviour (tested)

- `--toObj` exports group physics (hk_2013.3.0-r1) to OBJ: tested on Battlefront 2015 Hoth, 396 convex shapes.
- `--toHavok` builds a single convex shape only (no compound / mesh shapes yet, per the source).
- Input convention: `<x>.obj.temp_havok` + `<x>.obj.temp_resmeta`.
