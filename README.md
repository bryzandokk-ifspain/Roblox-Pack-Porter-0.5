# KodaMesh Porter v0.7 (Electron integration)

This desktop build connects the Electron UI to the existing `portpack.js` processing pipeline. It preserves the original texture processing, Blender mesh generation, Roblox asset upload, Zstandard JSON generation, sky processing, and crosshair processing logic.

## Requirements

- Windows 10/11 x64
- Node.js 22 LTS recommended for building
- Blender 5.2 installed at `C:\Program Files\Blender Foundation\Blender 5.2\blender.exe` (or set `PORTER_BLENDER_PATH`)
- Roblox Open Cloud API key with asset creation permissions
- Roblox creator user/group ID

## Run from source

1. Install Node.js 22 LTS.
2. Open a terminal in this folder.
3. Run `npm install`.
4. Run `npm start`.
5. Click **Settings** to open the app configuration folder. Edit `.env` there and enter:

```dotenv
ROBLOX_API_KEY="YOUR_ROBLOX_OPEN_CLOUD_API_KEY"
ROBLOX_CREATOR_ID="YOUR_USER_OR_GROUP_ID"
ROBLOX_IS_GROUP=false
PORTER_BLENDER_PATH="C:\\Program Files\\Blender Foundation\\Blender 5.2\\blender.exe"
```

Set `ROBLOX_IS_GROUP=true` if the creator ID belongs to a group. Restart the app after editing `.env`. Never share this file or place it in a public repository.

## Build Windows installer

```bash
npm install
npm run dist
```

The installer is generated in `release/`.

## Notes / known limitations

- The desktop build automatically chooses the first compatible sky when multiple skies are found and automatically crops incompatible square textures, because those interactions were originally Discord component prompts.
- Blender must be installed separately; it is not bundled in the installer.
- Roblox asset uploads require valid credentials and network access. Upload completion depends on Roblox API permissions, moderation, and availability.
- Creation Studio includes a transparent pixel canvas, 16x-512x resolution selection, HSV/hex color selection, recent colors, eraser, and a 3-second pixel eyedropper. Upload uses the same Blender mesh generation and Roblox Open Cloud asset upload helpers as the image-to-mesh pipeline. Roblox asset upload still requires valid credentials and permissions.
