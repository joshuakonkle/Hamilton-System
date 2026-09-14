# Kit covers (public URL for Gumroad)

Gumroad `POST /covers` only accepts a URL it can GET as an image. S3 presign URLs fail. Drive links fail unless they are world-readable.

**Lock:** kit banners live on this public repo and are served from source.

- Path: `docs/offers/covers/<sku>.jpg`
- Size: 1600 × 520 JPEG (height 420–600). Not a 16:9 hero.
- Public URL Gumroad should receive:
  - `https://source.digitalknowledge.net/docs/offers/covers/<sku>.jpg`
  - fallback `https://raw.githubusercontent.com/joshuakonkle/Hamilton-System/main/docs/offers/covers/<sku>.jpg`

Zip files stay off this repo. Covers are the exception because they must be fetchable.

`gumroad-ship` reads `cover_public_url` from SHIP.md, or builds the source URL from the SKU.
