# Combat Robot Calculator v1.7

Upload `index.html`, `motors.json`, and `weapons.json` together to the root of a GitHub Pages site.

## Blade data

`weapons.json` contains an array called `weapons`. No commercial blades are included until reference MOI measurements and fitment have been verified.

Example entry (illustrative numbers only; NOT a real product):

```json
{
  "id": "example-flat-blade",
  "vendor": "Example Manufacturer",
  "name": "Example Flat Blade",
  "diameterMm": 80,
  "image": "https://example.com/blade.png",
  "url": "https://example.com/blade",
  "compatibleHubs": ["hub2812"],
  "materials": {
    "steel": {
      "referenceThicknessMm": 6,
      "referenceMoiKgM2": 0.00012,
      "referenceMassG": 80
    },
    "titanium": {
      "referenceThicknessMm": 6,
      "referenceMoiKgM2": 0.000067,
      "referenceMassG": 45
    }
  }
}
```

- `id` must be unique. `compatibleHubs` lists exact motor IDs from `motors.json`; only listed IDs get green borders. Unlisted matches show red (not a confirmed direct fit), not proof that a custom adapter is impossible.
- `image` and `url` are optional. Missing/broken images use an SVG placeholder.
- Steel/titanium material reference records can be omitted independently. If a material is absent, its toggle is disabled.
- `referenceMassG` is optional. Without it, estimated mass and J/kg are not shown.
- MOI and mass thickness scaling assumes an unchanged, uniform-section homogeneous blade, excluding fixed hub hardware.
- Browser-saved custom blades persist locally; they are not uploaded to the JSON database. Custom blades can currently associate one directly compatible hub (or none).
- No geometry-based MOI estimation is used.

## Offline/demo fallback

If `motors.json` fails to fetch or has an invalid top-level database structure, the site shows a clearly labeled fictional sample motor. If `weapons.json` fails to fetch or has an invalid top-level database structure, it shows a clearly labeled fictional sample blade (with steel and titanium entries). Each fallback is independent: a successfully loaded database is used as-is, including an intentionally empty `weapons` array. Sample data is never appended to successful JSON results.
