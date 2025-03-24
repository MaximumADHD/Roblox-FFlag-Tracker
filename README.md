# Roblox FFlag Tracker

This repository is an offshoot of the [Roblox Client Tracker](https://github.com/CloneTrooper1019/Roblox-Client-Tracker), with the specific goal of tracking Roblox's application settings roughly in real-time.

## Terminology

The `F` in `FFlag` stands for `Fast`, and `Flag` represents a boolean in Roblox's application settings.<br/>Fast Flags are the most common type of setting, and in-general most people refer to Roblox's settings as FFlags.

In addition to `Flags`, there are other variable types supported.<br/>
Here is a list of every type:

<table>
	<tr>
		<th>Label</th>
		<th>Type</th>
	</tr>
	<tr>
		<td>Flag</td>
		<td>bool</td>
	</tr>
	<tr>
		<td>Int</td>
		<td>int</td>
	</tr>
	<tr>
		<td>String</td>
		<td>string</td>
	</tr>
	<tr>
		<td>Log</td>
		<td>byte</td>
	</tr>
</table>

There are also behavioral classifications:

<table>
	<tr>
		<th>Prefix</th>
		<th>Label</th>
		<th>Description</th>
	</tr>
	<tr>
		<td>F</td>
		<td>Fast</td>
		<td>A regular fast-variable that is initialized once<br/>and does not change until a new session begins.</td>
	</tr>
	<tr>
		<td>DF</td>
		<td>Dynamic Fast</td>
		<td>A fast-variable that can change at run-time, and<br/>automatically updates every 5 minutes.</td>
	</tr>
	<tr>
		<td>SF</td>
		<td>Synchronized Fast</span></td>
		<td>A fast-variable that is loaded by the server and<br/>sent to the client.</td>
	</tr>
</table>

## Apps & Platforms

The files in this repository each represent individual products of Roblox's client.<br/>These files correspond to the following products:

<table>
	<tr>
		<th>App/Platform</th>
		<th>File</th>
	</tr>
	<tr>
		<td>Client (Windows)</td>
		<td>PCDesktopClient.json</td>
	</tr>
	<tr>
		<td>Client (Mac)</td>
		<td>MacDesktopClient.json</td>
	</tr>
	<tr>
		<td>Roblox Studio</td>
		<td>StudioApp.json</td>
	</tr>
	<tr>
		<td>iOS</td>
		<td>iOSApp.json</td>
	</tr>
	<tr>
		<td>Android</td>
		<td>AndroidApp.json</td>
	</tr>
	<tr>
		<td>Xbox One</td>
		<td>XboxClient.json</td>
	</tr>
	<tr>
		<td>Client Installer (Windows)</td>
		<td>PCClientBootstrapper.json</td>
	</tr>
	<tr>
		<td>Client Installer (Mac)</td>
		<td>MacClientBootstrapper.json</td>
	</tr>
	<tr>
		<td>Studio Installer (Windows)</td>
		<td>PCStudioBootstrapper.json</td>
	</tr>
	<tr>
		<td>Studio Installer (Mac)</td>
		<td>MacStudioBootstrapper.json</td>
	</tr>
</table>

**PC** is currently inferred as the baseline platform. As such, all `#####Bootstrapper.json` files derive against `PCClientBootstrapper.json`, and non-bootstrap related files derive against `PCDesktopClient.json`.

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
