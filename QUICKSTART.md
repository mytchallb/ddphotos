# Quick Start — Your Own Photos

You’ve added config in `config/` and photos in `photos/`. Use these steps to generate and view your site.

## Prerequisites (one-time)

```bash
brew install go vips pkg-config
go mod download

make web-nvm-install
make web-npm-install
```

## 1. Run photogen

Resize photos and generate JSON indexes. Use `-doit` (no hyphen) or nothing is written.

```bash
go run cmd/photogen/photogen.go -resize -index -doit
```

Output goes to `web/albums/{id}/` (your `settings.id` in `albums.yaml`).

## 2. Point the site at your albums

Create a symlink so the web app uses your generated data:

```bash
ln -sfn ../albums/mytch web/static/albums
```

Use your actual `settings.id` (e.g. `mytch`, `prod`) in place of `mytch`.

## 3. Run the dev server

```bash
make web-npm-run-dev
```

Open [localhost:5173](http://localhost:5173) in your browser.

---

## Optional

- **Add captions**: Put a `photogen.txt` file in each album folder (see `sample/source/antarctica/photogen.txt`).
- **Album descriptions**: Edit `config/descriptions.txt` — one line per album: `slug` then description.
- **Build for deployment**: `make web-npm-build` — output is in `web/build/`.
