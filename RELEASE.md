# Release Guide

## Prepare

Update the version in:

- `Directory.Build.props`
- `manifest.template.json`
- release notes

Build:

```bash
dotnet restore
dotnet build -c Release
```

Package the build output:

```bash
mkdir -p dist/JellyseerrBridge_0.1.0.6
cp src/Jellyfin.Plugin.JellyseerrBridge/bin/Release/net10.0/* dist/JellyseerrBridge_0.1.0.6/
cd dist
zip -r JellyseerrBridge_0.1.0.6.zip JellyseerrBridge_0.1.0.6
md5sum JellyseerrBridge_0.1.0.6.zip
```

## GitHub Release

Create a GitHub release such as:

```text
v0.1.6
```

Attach:

```text
JellyseerrBridge_0.1.0.6.zip
```

## Manifest

The checked-in `manifest.json` and `manifest.example.json` describe the published 0.1.0.5 build. Keep that entry unchanged until the new archive is uploaded. Generate the new 0.1.0.6 entry with ABI `12.2.0.0` and its actual archive checksum; retain the old entry for Jellyfin 10.11 users.

Generate `manifest.json` after the release zip exists:

```bash
./scripts/generate-manifest.sh monjaka jellyfin-plugin-jellyseerr-bridge 0.1.0.6 v0.1.6 dist/JellyseerrBridge_0.1.0.6.zip > manifest.json
```

PowerShell:

```powershell
.\scripts\generate-manifest.ps1 -Owner monjaka -ZipPath dist\JellyseerrBridge_0.1.0.6.zip > manifest.json
```

Commit `manifest.json` so Jellyfin can read it from:

```text
https://raw.githubusercontent.com/monjaka/jellyfin-plugin-jellyseerr-bridge/main/manifest.json
```

Users can add that URL under Jellyfin Dashboard -> Plugins -> Repositories.

Important: Jellyfin downloads the plugin package from the version's `sourceUrl`. That field must point to `JellyseerrBridge_0.1.0.6.zip`, not the GitHub repository page.
