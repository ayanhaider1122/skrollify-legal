# Skrollify — Design System

## 1. Color Palette (Strictly Enforced)

| Token Name | Hex Code | Purpose |
| :--- | :--- | :--- |
| `DarkBg` | `#0B0B09` | Deep near-black background |
| `SurfaceDark` | `#171714` | Main container cards and list rows |
| `SurfaceElevated` | `#22221D` | Selected items, segment tabs, inner wells |
| `BorderSubtle` | `#35352F` | 1.dp hairline borders for structure |
| `BorderHighlight` | `#4A4A42` | Highlighted borders on selected states |
| `TextIvory` | `#F4F0E6` | Primary high-contrast warm ivory text |
| `TextMuted` | `#A7A59A` | Secondary descriptions and metadata |
| `DisabledElement`| `#55554E` | Inactive icons, subtle hints |
| `AccentSage` | `#C7D9AC` | Muted sage green accent (health, progress) |
| `AccentSageDark` | `#A5B888` | Darker sage for strokes and shadows |
| `ButtonIvory` | `#EDE8DC` | Primary button fill |
| `ButtonDarkText` | `#0B0B09` | Primary button text label |

## 2. Typography System
* **Display / Hero**: 44.sp – 34.sp ExtraBold (titles like "TK Decay", "Today's Scrolling").
* **Headline**: 28.sp – 24.sp ExtraBold (question titles like "Which apps do you use?").
* **Body Large**: 16.sp SemiBold (options text, button text).
* **Body Regular**: 14.sp Regular (subtitles, explanations, descriptions).
* **Caption / Label**: 12.sp – 11.sp Medium (badges, platform pills, status tags).

## 3. Shapes & Radii
* **Pill Buttons**: `RoundedCornerShape(28.dp)`
* **Content Cards**: `RoundedCornerShape(22.dp)` or `(24.dp)`
* **Selection Rows**: `RoundedCornerShape(20.dp)`
* **App Badges / Small Pills**: `RoundedCornerShape(12.dp)` or `(14.dp)`
* **Circular Elements**: `CircleShape`

## 4. Component Standards
* **Primary Action Buttons**:
  - Full-width, height 56.dp, warm ivory fill (`#EDE8DC`), bold dark text (`#0B0B09`), corner radius 28.dp.
* **Selection Rows (Radio & Checkbox)**:
  - Height 58.dp–64.dp, padded 18.dp horizontal, 14.dp vertical.
  - Background `SurfaceDark` (`#171714`) with 1.dp `BorderSubtle` border.
  - Selected state: `SurfaceElevated` (`#22221D`), crisp white indicator on left (radio) or right (checkbox).
* **App Logos**:
  - Authentic, official multi-stop gradient / vector shapes for Instagram, TikTok, YouTube, Snapchat, WhatsApp, Other.
* **Mascot Presentation**:
  - High-resolution 3D rendered character sitting on a subtle glowing ground spotlight. Never stretched, clipped, or approximated with primitive shapes.
