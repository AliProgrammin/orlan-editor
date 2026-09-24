# Orlan Editor

The office editing server of [Orlan](https://orlan.app): people edit PowerPoint, Word and Excel
files in the browser. It is Collabora Online, built from its MPL-2.0 source with the Orlan name
and logo. See [NOTICE.md](NOTICE.md) for the source and the licence.

## Image

`ghcr.io/aliprogrammin/orlan-editor:latest`, and one tag per commit of this repository.
GitHub Actions builds it (`.github/workflows/build.yml`) on each push to `main` and on a manual
run (`gh workflow run build.yml`). A build takes about 20 minutes.

## How it is built

- The engine is not compiled here. `build.sh` downloads the prebuilt engine that Collabora
  publishes for GitHub Actions (`ENGINE_ASSETS` in the `Dockerfile`).
- The server (online) is cloned from Collabora's Gerrit and compiled against that engine.
- `configure` gets `--with-app-name="Orlan Editor"`, `--with-vendor`, `--with-info-url`, and
  `--with-max-connections=100000 --with-max-documents=100000`.
- `branding/` goes into `/usr/share/coolwsd/browser/dist/`. The server links `branding.css` and
  `branding.js` into each editor page.

## Connection and document limits

online's `configure.ac` sets `MAX_CONNECTIONS=9999` and `MAX_DOCUMENTS=9999` unless
`--with-max-connections` or `--with-max-documents` gives another number. The limit of 20
connections and 10 documents applies only in "home mode", which exists only in a build with
`--with-welcome-url`. This build has no welcome url and sets both limits to 100000, so server
memory is the only limit. The build log prints the values the compiler sees (`#define
MAX_CONNECTIONS`).

## Run

```
docker run -p 9980:9980 \
  -e aliasgroup1=https://orlan.example \
  -e extra_params="--o:ssl.enable=false --o:ssl.termination=true" \
  -e DONT_GEN_SSL_CERT=1 \
  ghcr.io/aliprogrammin/orlan-editor:latest
```

`aliasgroup1` is the WOPI host that may open files. Put TLS in front of it (for example Traefik).
