# Roblox FFlag Tracker

This repository is an offshoot of the [Roblox Client Tracker](https://github.com/CloneTrooper1019/Roblox-Client-Tracker), with the specific goal of tracking Roblox's application settings in approximate real-time.

## Terminology

The `F` in `FFlag` stands for `Fast`, and `Flag` represents a boolean in Roblox's application settings.<br/>Fast Flags are the most common type of setting, and in-general most people refer to Roblox's settings as FFlags.

In addition to `Flags`, there are other variable types supported.<br/>
Here is a list of every type:

| Label | Type |
|-|-|
| Flag | `bool` |
| Int | `i64` |
| String | `string` |
| Log | `u8` |

There are also behavioral classifications:

| Prefix | Meaning | Description |
|-|-|-|
| `F` | Fast | An immutable fast variable that is loaded upon starting a session. |
| `DF` | Dynamic Fast | A mutable fast variable that is able to change to different values at runtime. |
| `SF` | Synchronized Fast | An immutable fast variable that is stored on the server and forces all connected clients to use its value. |

## Apps & Platforms

The files in this repository each represent individual products of Roblox's client.<br/>These files correspond to the following products:

| App/Platform | Identifier |
|-|-|
| Client (Windows) | PCDesktopClient |
| Client (Mac) | MacDesktopClient |
| Studio (Windows) | PCStudioApp |
| Studio (Mac) | MacStudioApp |
| iOS | iOSApp |
| Android | AndroidApp |
| Xbox | XboxClient |
| Playstation | PlayStationClient |
| Client Installer (Windows) | PCClientBootstrapper |
| Client Installer (Mac) | MacClientBootstrapper |
| Studio Installer (Windows) | PCStudioBootstrapper |
| Studio Installer (Mac) | MacStudioBootstrapper |

You can fetch the live JSON file from Roblox at these urls:
* `https://clientsettingscdn.roblox.com/v2/settings/application/{Identifier}`
* `https://clientsettingscdn.roblox.com/v2/settings/application/{Identifier}/bucket/{Bucket}`
  * (Bucket can be `zcanary`, `zintegration`, `zlive`, `zbeta`, or any other known internal Roblox channel)

**PC** is currently inferred to be the baseline platform. As such, all `{OS}Bootstrapper.json` files derive against `PCClientBootstrapper.json`, and non-bootstrap related files derive against `PCDesktopClient.json`.

## Metadata

Metadata about each individual FVariable can be accessed through the following route:<br/>
```
FVariables/{FVariableType}/{A-Z}/{FVariable}.json
```

The metadata can be described with the following Luau types:
```luau
type IMetadata<TypeName, Data> = {
    Type: TypeName,
    Value: Data
}

type PlatformData<T> = {
    AndroidApp: T?,
    iOSApp: T?,
    MacClientBootstrapper: T?,
    MacDesktopClient: T?,
    MacStudioApp: T?,
    MacStudioBootstrapper: T?,
    PCClientBootstrapper: T?,
    PCDesktopClient: T?,
    PCStudioApp: T?,
    PCStudioBootstrapper: T?,
    PlayStationClient: T?,
    UWPApp: T?,
    XboxClient: T?,
}

type ChannelData<T> = {
    LIVE: T?,
    zcanary: T?,
    zintegration: T?,
}

type Unified<T> = IMetadata<"Unified", T>
type Channels<T> = IMetadata<"Channels", ChannelData<T>>
type Platforms<T> = IMetadata<"Platforms", PlatformData<T>>
type ChannelsAndPlatforms<T> = IMetadata<"ChannelsAndPlatforms", ChannelData<PlatformData<T>>>

export type Metadata<T = (string | number)> =
    | Unified<T>
    | Channels<T>
    | Platforms<T>
    | ChannelsAndPlatforms<T>
```

## Source

This repo is automatically maintained by [RCT-Source](https://github.com/MaximumADHD/RCT-Source).
