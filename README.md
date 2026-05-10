# EFT FPS PLZ — Public Data

Runtime data fetched by the [EFT FPS PLZ](https://gepcperformance.com) app. Edit + push to update every client; no app rebuild required.

## Files

- **`links.json`** — site / Twitch / donation links shown in the app's footer + dialogs.
- **`streamer-presets.json`** — list of streamer-curated EFT settings presets, with optional Twitch profile picture displayed in the Presets section.
- **`presets/*.eftpreset`** — actual settings preset files referenced by `streamer-presets.json` entries via `PresetUrl`.

## Adding a streamer preset

1. Save a preset from inside the EFT FPS PLZ app (Presets section → Save Preset). This produces an `.eftpreset` file.
2. Upload the file to `presets/<streamer-handle>.eftpreset` in this repo.
3. Add an entry to `streamer-presets.json`:
   ```json
   {
     "Name": "streamer's preset",
     "Creator": "streamer_handle",
     "Twitch": "https://www.twitch.tv/streamer_handle",
     "Description": "Brief description shown under the name",
     "Game": "EscapeFromTarkov",
     "AvatarUrl": "https://static-cdn.jtvnw.net/jtv_user_pictures/<UUID>-profile_image-300x300.png",
     "PresetUrl": "https://raw.githubusercontent.com/gepcperformance/eft-fps-plz-public/master/presets/streamer_handle.eftpreset"
   }
   ```
4. Get the `AvatarUrl` from the streamer's Twitch page: right-click their profile picture → Inspect → copy the `<img>` `src`.
5. Commit + push to `master`. Clients fetch on next launch.

## Why a separate public repo?

The EFT FPS PLZ source is in a **private** repo. Clients fetch JSON + presets from `raw.githubusercontent.com`, which requires the source repo to be public for unauthenticated access. Splitting public data out of the source repo keeps the implementation private while letting clients pull updates without a new app release.
