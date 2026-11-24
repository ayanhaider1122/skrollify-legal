# Skrollify — Implementation Plan

## 1. Asset Pipeline
1. **Source Design Assets**:
   - Location: `assets/design/`
   - Manifest: `assets/design/manifest.json`
   - Assets needed:
     - `sproutling_thriving.png`
     - `sproutling_healthy.png`
     - `sproutling_tired.png`
     - `sproutling_wilted.png`
     - `sproutling_recovering.png`
     - `sproutling_growing.png`
     - `sproutling_sleeping.png`
     - `sproutling_variant_sage.png`
     - `sproutling_variant_blossom.png`
     - `sproutling_variant_golden.png`
     - `ic_launcher_sproutling.png`
2. **Android Resource Integration**:
   - High-density assets placed in `app/src/main/res/drawable/` as webp/png/jpg.
   - Vector logos in `AppLogos.kt`.

## 2. Phased Execution Order
1. **Phase 1 — Asset Generation & Manifest**:
   - Generate high-resolution mascot renders for all conditions and variants using `generate_image`.
   - Copy to `assets/design/` and `app/src/main/res/drawable/`.
2. **Phase 2 — Design System Tokens & Components**:
   - Refactor `theme/Color.kt`, `theme/Theme.kt`, `theme/Type.kt`.
   - Build standardized `ScrollDecayButton`, `ScrollDecaySelectionRow`, `ScrollDecayCard`.
3. **Phase 3 — Onboarding Refinement (Screens 1–6)**:
   - Ensure pixel-level fidelity matching the approved reference strip.
   - Compile and verify.
4. **Phase 4 — Home Dashboard Refinement**:
   - Integrate high-res mascot asset with real usage tracking and dynamic state transitions.
   - Compile and verify.
5. **Phase 5 — Quality Verification & Testing**:
   - Unit tests execution.
   - Full APK assembly verification.

## 3. UI Verification Loop
* **Local Compilation**: `./gradlew.bat testDebugUnitTest assembleDebug` ensures all layouts, resources, and viewmodels compile cleanly.
* **Asset Integrity**: Inspect generated and packaged images to prevent distortion, stretching, or downsampling.
* **Device Testing**: ADB connection ready for real phone installation and screenshot validation.
