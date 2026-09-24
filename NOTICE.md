# Source notice

Orlan Editor is Collabora Online, built from its source code without changes to that code.
Only the product name, the link and the logo differ (see `build.sh`, `start-orlan-editor.sh`
and `branding/`).

- Collabora Online is licensed under the Mozilla Public License 2.0. The full licence text is in
  [LICENSE](LICENSE). Copyright the Collabora Online contributors.
- Source of the server (online): https://gerrit.collaboraoffice.com/online, branch `main`. The
  build log of each image prints the exact commit (`Online source commit:`).
- Source of the engine: the prebuilt engine that Collabora publishes at
  https://github.com/CollaboraOnline/online/releases/tag/for-code-assets
  (`engine-main-assets.tar.gz`), built from the `engine/` directory of the same repository.
- Build files: adapted from `docker/from-source-gh-action` in
  https://github.com/CollaboraOnline/online (MPL-2.0).
- This repository, with every change we made: https://github.com/AliProgrammin/orlan-editor.

"Collabora" and "Collabora Online" are trademarks of Collabora Productivity Limited. Orlan
Editor is not made, endorsed or supported by Collabora.

The image carries this notice and the licence at `/usr/share/doc/orlan-editor/`.
