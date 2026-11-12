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

- The mint takes JPEG, PNG or WebP up to 25 MB, strips EXIF/GPS, and makes its own master and 1080 px display versions, so no thumbnails are needed here.
- New photos: at least 1000 px on the long side; JPEG quality 95, or PNG with a transparent background. Keep camera originals unedited and edit copies.
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
