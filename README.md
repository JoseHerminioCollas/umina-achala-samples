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

Form posts point at files with paths like `../samples/master.jpg`, relative to the post in `json/` or `generated/`.

## Images

Each stone's main photo goes in as two files of the same shot:

- **`main_image`:** JPEG, quality 95, on a white background (black or grey for a white stone). Wallets show this one.
- **`images[0]`:** the same photo as a PNG with a transparent background. The website shows this one.
- **`images[1…]`:** other angles, also PNG with a transparent background. `images` holds at most 5, so this leaves room for 4.
- **Size:** 2000–3000 px on the long side; at least 1000 px.
- **Not accepted by the mint:** HEIC, GIF, TIFF. Convert phone HEIC photos to JPEG first. WebP is accepted but gains little.
- Keep camera originals unedited and edit copies.

What the mint does with a photo (up to 25 MB): it strips EXIF/GPS and keeps a **master** at the original size and format (JPEG and WebP saved again at quality 95, PNG lossless). For the main photo only, it also makes a **display** version, a JPEG of 1080 px on the long side at quality 82, which wallets and marketplaces show. No thumbnails are needed here.

For each stone: cut it out once and export the transparent PNG (`images[0]`). Then flatten a copy onto the background colour in GIMP and export it as the JPEG for `main_image`. The main photo must have no transparency: the mint does not set a background for the display version, so transparent areas would come out black.
- A group photo: cut each stone out with the SAM 2 tool (`~/projects/sam2_goatstone`, `cut.py`), then clean the edge in GIMP (Layer → Transparency → Alpha to Selection, Select → Shrink/Grow) and export.

## Sources and rights

Every image must have a known source (own photo, stock with its licence, or AI-generated) before any use outside testnet. Fill this in as images are added:

| Path | Source | Licence / notes |
|---|---|---|
| `master.jpg`, `thumb.jpg` | | |
| `s.png`, `s.xcf` | | |

The PDFs are made up for testing. Their permit, REINFO and RUC numbers are not real.

## Storage

Plain git while the repo is small (about 12 MB now). Move `.xcf` files and originals to Git LFS if they grow past a few hundred MB.
