# KodaMesh Porter (Electron integration)

This desktop build connects the Electron UI to the existing `portpack.js` processing pipeline. It preserves the original texture processing, Blender mesh generation, Roblox asset upload, Zstandard JSON generation, sky processing, and crosshair processing logic.

## Requirements

* Windows 10/11 x64
* [Node.js 22 LTS](https://nodejs.org/dist/v22.11.0/node-v22.11.0-x64.msi) recommended for building
* [Blender 5.2](https://www.blender.org/download/release/Blender5.2/blender-5.2.3-windows-x64.msi/) installed at `C:\\\\\\\\\\\\\\\\Program Files\\\\\\\\\\\\\\\\Blender Foundation\\\\\\\\\\\\\\\\Blender 5.2\\\\\\\\\\\\\\\\blender.exe` (or set `PORTER\\\\\\\\\\\\\\\_BLENDER\\\\\\\\\\\\\\\_PATH`)
* Roblox Open Cloud API key with asset creation permissions
* Roblox creator user/group ID

## Run from source

1. Install [Node.js 22 LTS](https://nodejs.org/dist/v22.11.0/node-v22.11.0-x64.msi).
2. Open a terminal in this folder.
3. Run `npm install`.
4. Run `npm start`.
5. Click **Settings** to open the app configuration folder. Edit `.env` there and enter:

```dotenv
ROBLOX\\\\\\\\\\\\\\\_API\\\\\\\\\\\\\\\_KEY="YOUR\\\\\\\\\\\\\\\_ROBLOX\\\\\\\\\\\\\\\_OPEN\\\\\\\\\\\\\\\_CLOUD\\\\\\\\\\\\\\\_API\\\\\\\\\\\\\\\_KEY"
ROBLOX\\\\\\\\\\\\\\\_CREATOR\\\\\\\\\\\\\\\_ID="YOUR\\\\\\\\\\\\\\\_USER\\\\\\\\\\\\\\\_OR\\\\\\\\\\\\\\\_GROUP\\\\\\\\\\\\\\\_ID"
ROBLOX\\\\\\\\\\\\\\\_IS\\\\\\\\\\\\\\\_GROUP=false
PORTER\\\\\\\\\\\\\\\_BLENDER\\\\\\\\\\\\\\\_PATH="C:\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\Program Files\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\Blender Foundation\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\Blender 5.2\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\blender.exe"
```

Set `ROBLOX\\\\\\\\\\\\\\\_IS\\\\\\\\\\\\\\\_GROUP=true` if the creator ID belongs to a group. Restart the app after editing `.env`. Never share this file or place it in a public repository.

## Build Windows installer

```bash
npm install
npm run dist
```

The installer is generated in `release/`.

## Notes / known limitations

* The desktop build automatically chooses the first compatible sky when multiple skies are found and automatically crops incompatible square textures, because those interactions were originally Discord component prompts.
* Blender must be installed separately; it is not bundled in the installer.
* Roblox asset uploads require valid credentials and network access. Upload completion depends on Roblox API permissions, moderation, and availability.
* Creation Studio includes a transparent pixel canvas, 16x-512x resolution selection, HSV/hex color selection, recent colors, eraser, and a 3-second pixel eyedropper. Upload uses the same Blender mesh generation and Roblox Open Cloud asset upload helpers as the image-to-mesh pipeline. Roblox asset upload still requires valid credentials and permissions.

## How to create the API key:

First of all, go in here: [https://create.roblox.com/dashboard/credentials](https://create.roblox.com/dashboard/credentials)
Then press ''Create API key'', then give it any name you want in the box, then in ''Access permissions'' select:
assets-permisions \[write]
assets \[read] \[write]

luau-execution-sessions \[read] \[write]
And finally, when you've finished, press 'Save and generate key', copy the API key, and put it in the .env
**How to get your UserID:**
For the UserID, just log into Roblox from the browser, put your username in the search bar, and some numbers will appear at the top. That will be your ID, copy it and put it in the .env
You can also go to this page to see your Roblox ID:
[https://rblxdb.com/tools/user-lookup](https://rblxdb.com/tools/user-lookup)

