# umina-achala-samples

Test images and documents for minting Umiña and Achala NFTs on Hedera **testnet**. They are not the real products for the site: real stones and jewelry are sourced under umina-achala/umina-achala-web#94. Plan and checklist: umina-achala/umina-achala-chain#22 ("Test images").

This is its own repo, beside the other Umiña Achala repos, so a client site can use the images later without the chain code.

## Use from umina-achala-chain

The chain repo reads `samples/`, which is a symlink to this repo (git-ignored there):

```bash
cd ~/projects/umina-achala/umina-achala-chain
ln -s ../umina-achala-samples samples
node src/mint/mintNFT.js --form json/sample-umina-form-post.json --dry-run
```

Form posts point at files with paths like `../samples/chrysocolla/cut/stone_1.jpg`, relative to the post in `json/` or `generated/`.

## Layout

One folder per stone type, named with its id from `umina-achala-chain/schema/stone-types.json`:

```
<stone_type>/
  uncut/stone_1.jpg, stone_2.jpg           rough stone
  cut/stone_1.jpg, stone_2.jpg             cut or polished stone
  mounted/uncut/stone_1.jpg, stone_2.jpg   rough stone set in a piece (Achala)
  mounted/cut/stone_1.jpg, stone_2.jpg     cut stone set in a piece (Achala)
```

Stone types: `amethyst`, `chrysocolla`, `jade`, `lapis_lazuli`, `malachite`, `obsidian`, `quartz`, `ruby`, `sapphire`, `tourmaline`.

Gaps: `chrysocolla/mounted/uncut` and `tourmaline/mounted/uncut` have only `stone_1.jpg`.

### Files at the top level

| File | What it is | Used by |
|---|---|---|
| `master.jpg` | Chrysocolla, 1080 × 1080, main photo of `UMINA-2026-CH-99` | `json/sample-umina-form-post.json`, `json/umina-example.json` |
| `thumb.jpg` | Chrysocolla, 300 × 300, second photo of the same stone | same |
| `mining-permit.pdf` | Fake mining concession permit, marked "SAMPLE - FAKE DOCUMENT FOR TESTING ONLY" | same |
| `store-receipt.pdf` | Fake store receipt for `UMINA-2026-CH-99`, marked the same way | same, and `__tests__/metadataValidator.test.js` |
| `s.png`, `s.xcf` | Tumbled chrysocolla cut out on a transparent background, with its GIMP file | not yet |

These are due to move into `chrysocolla/` (chain#22). When they move, update the chain's `json/` posts and `umina-achala-documents/scripts.md` in the same change.

## Images

- JPEG, 1080 px wide. Two are smaller: `malachite/mounted/cut/stone_1.jpg` (356 × 343) and `quartz/mounted/cut/stone_1.jpg` (517 × 497).
- The mint takes JPEG, PNG or WebP up to 25 MB, strips EXIF/GPS, and makes its own master and 1080 px display versions, so no thumbnails are needed here.
- New photos: at least 1000 px on the long side; JPEG quality 95, or PNG with a transparent background. Keep camera originals unedited and edit copies.
- A group photo: cut each stone out with the SAM 2 tool (`~/projects/sam2_goatstone`, `cut.py`), then clean the edge in GIMP (Layer → Transparency → Alpha to Selection, Select → Shrink/Grow) and export.

## Sources and rights

Every image must have a known source (own photo, stock with its licence, or AI-generated) before any use outside testnet. Fill this in as images are added:

| Path | Source | Licence / notes |
|---|---|---|
| `master.jpg`, `thumb.jpg` | | |
| `s.png`, `s.xcf` | | |
| `<stone_type>/…` | | |

The PDFs are made up for testing. Their permit, REINFO and RUC numbers are not real.

## Storage

Plain git while the repo is small (about 12 MB now). Move `.xcf` files and originals to Git LFS if they grow past a few hundred MB.
