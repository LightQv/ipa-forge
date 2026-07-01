# ipa-forge

Build unsigned iOS apps and package them as IPA files for sideloading.

`ipa-forge` is a small macOS CLI around `xcodebuild` that builds an unsigned iOS app, places it in a `Payload` folder, and zips it into an `.ipa`.

## Requirements

- macOS
- Xcode command line tools
- An iOS project with an `ios/` directory and an Xcode workspace

## Usage

Run from the target project root:

```bash
npx ipa-forge --name=Scenario
```

Or pass the project root explicitly:

```bash
npx ipa-forge --name=Scenario --input=/path/to/scenario_expo
```

Choose the output IPA path:

```bash
npx ipa-forge --name=Scenario --input=/path/to/scenario_expo --output=~/Downloads/Scenario.ipa
```

## Sideloading

`ipa-forge` creates an unsigned `.ipa` that can be used with sideloading tools such as [AltStore](https://github.com/altstoreio/AltStore).

This CLI does not install the app on your device. It only builds and packages the `.ipa`; use AltStore or another sideloading tool to install it.

## Flags

```text
--name=AppName              Required. App name. Also used as the default scheme and workspace name.
--input=/path/to/project    Project root to build from. Defaults to the current directory.
--output=/path/to/file.ipa  Final IPA path. Defaults to ~/Downloads/Payload.ipa.
--scheme=AppName            Xcode scheme. Defaults to --name.
--workspace=path            Xcode workspace. Defaults to ios/{name}.xcworkspace.
--configuration=Release     Xcode build configuration. Defaults to Release.
--derived-data=path         Derived data path. Defaults to {input}/ios/build.
--help                      Show help.
```

## Defaults

For this command:

```bash
npx ipa-forge --name=Scenario
```

`ipa-forge` assumes:

```text
input:        current directory
workspace:    ios/Scenario.xcworkspace
scheme:       Scenario
configuration: Release
derived data: {input}/ios/build
output:       ~/Downloads/Payload.ipa
```

## Publishing

```bash
npm login
npm publish
```

Before publishing, make sure `package.json` points to the correct GitHub repository.
