# Seerr Bridge for Jellyfin
# Seerr Bridge for Jellyfin

A Jellyfin 12.2-compatible fork of [Jellyseerr Bridge](https://github.com/monjaka/jellyfin-plugin-seerr-bridge), originally developed by [monjaka](https://github.com/monjaka).

Seerr Bridge adds a Jellyseerr/Seerr-powered request page directly to Jellyfin without exposing the Seerr API key to browsers.

**Compatibility:** Jellyfin 12.2.x, .NET 10  
**Current release:** 0.1.0.7  
**Status:** Experimental — initial Jellyfin 12.2 compatibility release.

## Screenshots

<img width="1117" height="283" alt="Jellyfin request navigation" src="https://github.com/user-attachments/assets/2d508176-25dd-4d94-9e12-2fc7458b2387" />

<img width="1488" height="641" alt="Media request page" src="https://github.com/user-attachments/assets/7ff5b1f4-e7d5-47b2-804d-bf067ac31f5c" />

## Installation

### 1. Add the plugin repository

In Jellyfin, navigate to **Dashboard → Plugins → Repositories**.

Add the following repository:
## Installation

### 1. Add the plugin repository

In Jellyfin, navigate to **Dashboard → Plugins → Repositories**.

Add the following repository:

```text
Name: Seerr Bridge (JeffCox56)
URL: https://raw.githubusercontent.com/JeffCox56/jellyfin-seerr-bridge/main/manifest.json
```

### 2. Install the plugin

1. Navigate to **Dashboard → Plugins → Catalog**.
2. Find **Jellyseerr Bridge**.
3. Install version `0.1.0.7` or newer.
4. Restart Jellyfin.

### 3. Configure Seerr

Navigate to **Dashboard → Plugins → Jellyseerr Bridge**.

Configure:

- **Seerr Base URL:** The URL Jellyfin uses to reach your Seerr instance.
- **Seerr API Key:** Your Seerr API key.
- **Enable Request Submission:** Enable this to allow media requests.

<img width="904" height="649" alt="Plugin configuration" src="https://github.com/user-attachments/assets/da23e483-1528-4bf4-b687-522db8ae9114" />

### 4. Install the Jellyfin Web navigation button

The plugin uses a separate web-loader installation step to add the **Request** navigation button to Jellyfin Web.

On the Jellyfin server:
### 4. Install the Jellyfin Web navigation button

The plugin uses a separate web-loader installation step to add the **Request** navigation button to Jellyfin Web.

On the Jellyfin server:

```bash
curl -fsSLO https://raw.githubusercontent.com/JeffCox56/jellyfin-seerr-bridge/main/scripts/install-web-loader.sh

# Review the downloaded script before running it
less install-web-loader.sh

sudo bash install-web-loader.sh
sudo systemctl restart jellyfin
```
```bash
curl -fsSLO https://raw.githubusercontent.com/JeffCox56/jellyfin-seerr-bridge/main/scripts/install-web-loader.sh

# Review the downloaded script before running it
less install-web-loader.sh

sudo bash install-web-loader.sh
sudo systemctl restart jellyfin
```

These commands assume Jellyfin is installed as a systemd service and the installer supports your Jellyfin Web layout.

Hard-refresh Jellyfin in your browser afterward.
These commands assume Jellyfin is installed as a systemd service and the installer supports your Jellyfin Web layout.

Hard-refresh Jellyfin in your browser afterward.

The request page can also be accessed directly at:
The request page can also be accessed directly at:

```text
https://your-jellyfin-domain/JellyseerrBridge/Page
```

**Note:** The web-loader integration is still being validated against Jellyfin 12.2. Installing the plugin does not automatically guarantee the Request navigation button will appear.

## Updating After Jellyfin Updates

Jellyfin updates may replace or modify Jellyfin Web's `index.html`, removing the custom navigation entry.

If the Request button disappears, rerun:

```bash
curl -fsSLO https://raw.githubusercontent.com/JeffCox56/jellyfin-seerr-bridge/main/scripts/install-web-loader.sh

sudo bash install-web-loader.sh
sudo systemctl restart jellyfin
```

Then hard-refresh your browser.

## Uninstall

First, remove the Jellyfin Web navigation integration:

```bash
curl -fsSLO https://raw.githubusercontent.com/JeffCox56/jellyfin-seerr-bridge/main/scripts/uninstall-web-loader.sh

less uninstall-web-loader.sh

sudo bash uninstall-web-loader.sh
sudo systemctl restart jellyfin
```

Then uninstall **Jellyseerr Bridge** from **Dashboard → Plugins**.

## Features

- Jellyfin-hosted request page for searching, discovering, and requesting media.
- Movie and television series detail views, including per-season request buttons.
- Discovery filters for ratings, release dates, and major streaming providers.
- Sorting by release date, title, and rating.
- Seerr-provided availability and request status.
- Server-side API requests using a configured Seerr URL and API key.
- Validated request endpoints rather than an unrestricted API proxy.
- Jellyfin Web integration providing a Request tab and Requests side-menu entry.

## Security Model

The Seerr API key is stored in Jellyfin's plugin configuration and used exclusively by the plugin's server-side integration.

Browsers communicate with Jellyfin plugin endpoints rather than directly receiving the Seerr API key.

Request submission is disabled by default and must be explicitly
