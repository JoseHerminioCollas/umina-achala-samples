# umina-achala-testnet

Everything for minting Umiña and Achala NFTs on Hedera **testnet**: the form posts, and the images and documents they name. They are not the real products for the site: real stones and jewelry are sourced under umina-achala/umina-achala-web#94. Plan and checklist: umina-achala/umina-achala-chain#22 ("Test images").

This is its own repo, beside the other Umiña Achala repos, so a client site can use the images later without the chain code.

## Use from umina-achala-chain

The chain repo reads `testnet/`, which is a symlink to this repo (git-ignored there):

```bash
cd ~/projects/umina-achala/umina-achala-chain
ln -s ../umina-achala-testnet testnet
node src/mint/mintNFT.js --form testnet/chrysocolla_a.json --dry-run
node src/mint/mintNFT.js --form testnet/achala_a.json --token achala --dry-run
```

A post names its files by bare name (`"file": "chrysocolla_a1.jpg"`), relative to the post, so posts sit beside their images here. A copy of a post written into the chain repo's `generated/` must point them at `../testnet/` instead (see `umina-achala-documents/scripts.md`).

## Naming

All files sit at the top level, no folders: `<stone_type>_<stone letter><photo number>.<ext>`. `stone_type` is the id from `umina-achala-chain/schema/stone-types.json`; the letter is the stone (a, b, c…); the number is the photo of that stone. A stone's form post is `<stone_type>_<letter>.json`; an Achala's is `achala_<letter>.json`. A source image not yet worked in GIMP has no number (`quartz_a.jpg`).

```
chrysocolla_a.json                 stone A's form post
achala_a.json                      Achala A's form post (a pendant with chrysocolla A)
chrysocolla_a1.jpg                 stone A, photo 1: main_image, on white
chrysocolla_a1.png                 stone A, photo 1: transparent (images[0])
chrysocolla_a2.png                 stone A, photo 2
chrysocolla_a3.png                 stone A, photo 3
chrysocolla_a_mining-permit.pdf    stone A's documents
chrysocolla_a_store-receipt.pdf
chrysocolla_a_group.jpg            group photo the stones were cut from
chrysocolla_master.xcf             GIMP working file, one per stone type
```

Photo descriptions in the form posts: "Front view", "Back view", "Side view" when the stone has a face; otherwise by rotation from photo 1, e.g. three photos turned 0°, 120° and 240°: "View 1 of 3", "View 2 of 3, turned 120°", "View 3 of 3, turned 240°".

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
| `chrysocolla_a_group.jpg` | | |
| `chrysocolla_a1`–`a3`, `chrysocolla_master.xcf` | cut from `chrysocolla_a_group.jpg` | |

The PDFs are made up for testing. Their permit, REINFO and RUC numbers are not real.

## Storage

Plain git while the repo is small (about 12 MB now). Move `.xcf` files and originals to Git LFS if they grow past a few hundred MB.
