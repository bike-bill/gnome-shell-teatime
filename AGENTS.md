# AGENTS.md

## Build & Install

```bash
./autogen.sh
./configure --prefix=/usr && make
make local-install  # installs to ~/.local/share/gnome-shell/extensions
make zip            # creates distributable zip for extensions.gnome.org
```

Restart GNOME Shell (Alt+F2, r) after install if extension doesn't appear.

## Code Formatting

```bash
./beautify-code.sh  # requires: pip install jsbeautifier
```

Run before commits. Uses tabs, jslint-happy style.

## Architecture

- **extension.js**: Main extension class, panel button, timer logic
- **prefs.js**: GTK4/Adw preferences dialog
- **utils.js**: Shared helpers (time parsing, sound playback via GStreamer)
- **icon.js**: SVG icon rendering with Cairo
- **schemas/**: GSettings schema (org.gnome.shell.extensions.teatime)

Targets GNOME Shell 47-50. Uses ESM imports from `gi://` and `resource:///org/gnome/shell/`.

## i18n

Translation files in `po/`. Gettext domain: `TeaTime`. Run `po/update_strings.sh` to update .pot file.

## Testing

No automated tests. Test manually by installing locally and verifying in GNOME Shell. Check `journalctl -f` for extension errors.
