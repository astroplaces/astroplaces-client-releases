# Astro Places Package Format (APPF)

Astro Places uses a unified, simple, and open package format for both Themes and Gestures. This allows community developers to easily create custom content, tools, and generators compatible with the Astro Places client.

## Archive Structure

All Astro Packages are standard **ZIP archives** containing assets and a JSON manifest. To distinguish them, they use custom file extensions:

- **Themes:** Use the `.athm` extension.
- **Gestures:** Use the `.agst` extension.

At the root of every archive, the client expects a single manifest file named `toc.json` (Table of Contents). This file defines the package's metadata and tells the client where to find the included assets.

---

## 1. Themes (`.athm`)

A Theme package dictates the visual color palette of the Astro Places client.

### `toc.json` Schema

The table of contents for a Theme must contain the following keys:

```json
{
  "id": "my_unique_theme_v1",
  "name": "My Cool Theme",
  "author": "YourUsername",
  "preview": "preview.png",
  "palette": "palette.json"
}
```

- **`id`** _(string)_: A unique identifier for the theme (no spaces, typically snake_case).
- **`name`** _(string)_: The human-readable display name.
- **`author`** _(string)_: The creator of the theme.
- **`preview`** _(string)_: The filename of the preview image located in the archive (e.g., `.png`, `.jpg`). This is used as a gallery thumbnail.
- **`palette`** _(string)_: The filename of the JSON file containing the actual color definitions.

### `palette.json` Full Example

The palette file must define the complete suite of UI color tokens expected by the client. Below is a full example containing all required keys. You may use any standard Hex color codes you like.

```json
{
  "White": "#FFFFFF",
  "Black": "#000000",
  "Zinc50": "#F8FAFC",
  "Zinc100": "#F1F5F9",
  "Zinc200": "#E2E8F0",
  "Zinc300": "#CBD5E1",
  "Zinc400": "#94A3B8",
  "Zinc500": "#64748B",
  "Zinc600": "#475569",
  "Zinc700": "#334155",
  "Zinc800": "#1E293B",
  "Zinc900": "#0F172A",
  "Zinc950": "#020617",
  "Primary50": "#FFF1F2",
  "Primary100": "#FFE4E6",
  "Primary200": "#FECDD3",
  "Primary300": "#FDA4AF",
  "Primary400": "#FB7185",
  "Primary500": "#F43F5E",
  "Primary600": "#E11D48",
  "Primary700": "#BE123C",
  "Primary800": "#9F1239",
  "Primary900": "#881337",
  "Primary950": "#4C0519",
  "Muted50": "#FAFAFA",
  "Muted100": "#F5F5F5",
  "Muted200": "#E5E5E5",
  "Muted300": "#D4D4D4",
  "Muted400": "#A3A3A3",
  "Muted500": "#737373",
  "Muted600": "#525252",
  "Muted700": "#404040",
  "Muted800": "#262626",
  "Muted900": "#171717",
  "Muted950": "#0A0A0A",
  "AlphaLight50": "#0DFFFFFF",
  "AlphaLight100": "#1AFFFFFF",
  "AlphaLight200": "#33FFFFFF",
  "AlphaLight300": "#4DFFFFFF",
  "AlphaLight400": "#66FFFFFF",
  "AlphaLight500": "#80FFFFFF",
  "AlphaLight600": "#99FFFFFF",
  "AlphaLight700": "#B3FFFFFF",
  "AlphaLight800": "#CCFFFFFF",
  "AlphaLight900": "#E6FFFFFF",
  "AlphaLight1000": "#FFFFFFFF",
  "AlphaLight00": "#00FFFFFF",
  "AlphaDark50": "#0D000000",
  "AlphaDark100": "#1A000000",
  "AlphaDark200": "#33000000",
  "AlphaDark300": "#4D000000",
  "AlphaDark400": "#66000000",
  "AlphaDark500": "#80000000",
  "AlphaDark600": "#99000000",
  "AlphaDark700": "#B3000000",
  "AlphaDark800": "#CC000000",
  "AlphaDark900": "#E6000000",
  "AlphaDark1000": "#FF000000",
  "AlphaDark00": "#00000000"
}
```

---

## 2. Gestures (`.agst`)

A Gesture package defines interactive animations and sounds that users can trigger in chatrooms.

### `toc.json` Schema

The table of contents for a Gesture must contain the following keys:

```json
{
  "id": "fun_wave_gesture",
  "name": "Friendly Wave",
  "author": "YourUsername",
  "text": "waves happily",
  "animation": "wave.gif",
  "audio": "wave_sound.mp3"
}
```

- **`id`** _(string)_: A unique identifier for the gesture.
- **`name`** _(string)_: The human-readable display name.
- **`author`** _(string)_: The creator of the gesture.
- **`text`** _(string)_: Action text that will always be displayed alongside the gesture in the chat feed. **This must be clean text without special characters or line breaks.**
- **`animation`** _(string)_: The filename of the image file in the archive.
- **`audio`** _(string)_: The filename of the accompanying audio file in the archive.

## Asset Guidelines

- **Root Placement:** All assets referenced in the `toc.json` (such as images, palettes, or audio) must be placed at the root of the ZIP archive.
- **Animations:** The highly recommended default format for gesture animations is `.gif`. Please keep animation file sizes between **10 KB** and **3 MB** to ensure the client stays fast and responsive.
- **Audio:** Audio files within gesture packages must be standard `.mp3` format. For a seamless user experience, gesture audio enforces a default **5 second** playback duration. Users are able to set their own playback duration, but it is important to keep this default in mind.
