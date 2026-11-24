# Skrollify — Avatar Layered Art Specification (v2.0)

> **Document Type:** Production Art Specification & Technical Integration Guide  
> **Target Platform:** Native Android (Jetpack Compose / Android Bitmap Pipeline)  
> **Rendering Paradigm:** 2.5D Layered Pre-Shaded Modular Assets  
> **Target Quality Benchmark:** Bitmoji / Modern Casual Mobile Game Character Quality  

---

## 1. Technical Framework & Constraints

### 1.1 Canvas & Export Format
- **Canvas Dimensions:** `1024 × 1024 px`, square, 72/144 DPI.
- **Export Format:** 32-bit transparent PNG or lossless WebP with alpha channel.
- **Color Profile:** sRGB.
- **Target Background:** Must be drawn and tuned to sit on pure black (`#000000`).
- **Rim Lighting:** Subtle light rim contour (1–2px soft glow) along outer edges of hair, shoulders, and jaw to pop against black backgrounds.
- **Bottom Fade:** Outfits must terminate at `y = 1024` with a soft alpha gradient fade between `y = 920` and `y = 1024`, ensuring zero hard cutoff.

---

## 2. Standardized Anchor Grid & Registration

Every asset must be drawn on the identical **1024 × 1024 canvas** with registration aligned to these reference points:

```
(0, 0) ------------------------------------------------ (1024, 0)
|                                                              |
|                     [Head Top: y = 260]                      |
|                                                              |
|                  Left Brow         Right Brow                |
|                  (380, 420)        (644, 420)                |
|                                                              |
|                   Left Eye          Right Eye                |
|                  (400, 460)        (624, 460)                |
|                                                              |
|                    [Nose Center: (512, 510)]                 |
|                                                              |
|                    [Mouth Line: (512, 570)]                  |
|                                                              |
|                    [Chin Line:  (512, 660)]                  |
|                                                              |
|                    [Neck Center: (512, 700)]                 |
|                                                              |
|             Left Shoulder              Right Shoulder        |
|               (240, 780)                 (784, 780)          |
|                                                              |
|                                                              |
|                     [Torso Base: y = 1024]                   |
(0, 1024) -------------------------------------------- (1024, 1024)
```

| Landmark | Coordinate / Line | Notes |
| :--- | :--- | :--- |
| **Canvas Center (X)** | `x = 512 px` | Symmetrical center line for face & body |
| **Head Top (Crown)** | `y = 260 px` | Scalp line before hair volume |
| **Brow Line** | `y = 420 px` | Rest eyebrow baseline |
| **Eye Line** | `y = 460 px` | Pupil centers: Left `(400, 460)`, Right `(624, 460)` |
| **Nose Tip** | `(512, 510)` | Base of nose |
| **Mouth Center** | `(512, 570)` | Smile / resting mouth center |
| **Chin Line** | `y = 660 px` | Lowest chin point (soft variation per base) |
| **Neck Anchor** | `y = 700 px` | Connection between head and shoulders |
| **Shoulder Line** | `y = 780 px` | Collarbone / shoulder peak level |
| **Torso Fade** | `y = 920..1024 px`| Soft gradient fade into transparency |

---

## 3. Strict Layer Ordering (Z-Index Pipeline)

Layers are composed from back to front:

| Slot Order | Slot Name | Asset Layer | Description |
| :---: | :--- | :--- | :--- |
| **10** | `BACK_HAIR` | `hair_<id>_back.png` | Hair volume behind head, neck, and shoulders. |
| **20** | `BODY_TORSO` | `base_<type>_body.png` | Shoulders, neck base, collarbones. |
| **30** | `OUTFIT_BASE` | `outfit_<id>_base.png` | Main clothing fabric (recolorable). |
| **35** | `OUTFIT_DETAILS` | `outfit_<id>_details.png` | Seams, collars, zippers, drawstrings, buttons. |
| **40** | `NECK_HEAD` | `base_<type>_head.png` | Head shape, ears, and neck skin. |
| **42** | `JAW_SHADOW` | `base_<type>_shadow.png` | Soft drop shadow cast by jaw onto neck. |
| **45** | `FRINGE_SHADOW` | `hair_<id>_shadow.png` | Soft shadow cast by bangs onto forehead. |
| **50** | `FACE_DETAILS` | `face_<id>.png` | Freckles, beauty marks, blush, dimples, stubble. |
| **60** | `EYES` | `eyes_<id>_<state>.png` | Open, sleepy, or closed blinking eyes. |
| **70** | `EYEBROWS` | `brows_<id>_<state>.png` | Neutral, joyful, sleepy, or concerned. |
| **80** | `NOSE` | `nose_<id>.png` | Soft contoured nose shading. |
| **90** | `MOUTH` | `mouth_<id>_<state>.png` | Smile, calm, yawn, open, laughing. |
| **100** | `FRONT_HAIR` | `hair_<id>_front.png` | Fringe, bangs, side tendrils, layered locks. |
| **105** | `HAIR_HIGHLIGHTS`| `hair_<id>_sheen.png` | Translucent specular sheen and light bounce. |
| **110** | `ACCESSORIES` | `acc_<id>.png` | Glasses, earrings, hats, headphones. |

---

## 4. Color Slots & Tinting Rules

To allow infinite personalization from a lightweight asset set:
1. **Recolorable Base Layer:**
   - Saved as neutral grayscale (`#808080` base tone) with pre-baked volumetric shading.
   - Tinted at runtime using `ColorFilter.tint(chosenColor, BlendMode.Modulate)`.
2. **Fixed Highlight/Detail Layer:**
   - Drawn with pure white/warm highlights and alpha gradients.
   - Drawn directly over the tinted base layer without color multiplication to preserve sparkling catchlights and fabric stitch details.

---

## 5. File Naming Conventions & Directory Layout

Assets are placed in `app/src/main/assets/avatar/`:

```
assets/avatar/
├── bases/
│   ├── base_fem_head.png
│   ├── base_fem_body.png
│   ├── base_fem_shadow.png
│   ├── base_masc_head.png
│   ├── base_masc_body.png
│   ├── base_masc_shadow.png
│   ├── base_andro_head.png
│   ├── base_andro_body.png
│   └── base_andro_shadow.png
├── hair/
│   ├── hair_sidepart_back.png
│   ├── hair_sidepart_front.png
│   ├── hair_sidepart_sheen.png
│   ├── hair_sidepart_shadow.png
│   ├── hair_bob_back.png
│   ├── hair_bob_front.png
│   ├── hair_bob_sheen.png
│   ├── hair_bob_shadow.png
│   ├── hair_undercut_back.png
│   ├── hair_undercut_front.png
│   └── hair_undercut_sheen.png
├── eyes/
│   ├── eyes_default_open.png
│   ├── eyes_default_blink.png
│   ├── eyes_default_sleepy.png
│   └── eyes_default_wink.png
├── brows/
│   ├── brows_default_neutral.png
│   ├── brows_default_joyful.png
│   └── brows_default_sleepy.png
├── mouths/
│   ├── mouth_default_smile.png
│   ├── mouth_default_calm.png
│   └── mouth_default_sleepy.png
├── noses/
│   └── nose_default.png
├── outfits/
│   ├── outfit_hoodie_base.png
│   ├── outfit_hoodie_details.png
│   ├── outfit_knit_base.png
│   ├── outfit_knit_details.png
│   ├── outfit_jacket_base.png
│   └── outfit_jacket_details.png
└── accessories/
    └── acc_glasses_gold.png
```

---

## 6. Illustrator / Asset Pack Checklist

When commissioning an artist on Fiverr, Upwork, or Behance:
- [ ] 3 Genuinely different bases:
  - **Feminine:** Softer jawline, smaller chin, slender neck, narrower shoulders, softer eyebrows.
  - **Masculine:** Defined angular jaw, broader chin, thicker neck, wider athletic shoulders, stronger brow line.
  - **Androgynous:** Balanced contemporary oval, neutral neck width.
- [ ] Soft shading with highlights, ambient occlusion, and rim light (feels "almost 3D" like Bitmoji).
- [ ] Large expressive glossy eyes with double catchlights.
- [ ] Separated front and back hair layers for each hairstyle.
- [ ] Eyelid / closed eye frame for procedural blinking.
- [ ] Compatible collar line across all 3 bases.
- [ ] Full commercial usage rights transferred to app owner.
