# GPX Street View Flythrough — Website

Static landing page for the GPX Street View Flythrough Chrome extension,
live at [gpx-street-viewer.codemountain.be](https://gpx-street-viewer.codemountain.be/).

There is no build step: the files in this repository are served as-is.

## Deploy

The site is served by Caddy on the `vimexx` server, straight from a git
checkout of this repository at `/home/bruno/projects/gpx-street-view`.

1. Commit and push your changes to `master`:

   ```sh
   git push origin master
   ```

2. Pull them on the server:

   ```sh
   ssh vimexx 'cd /home/bruno/projects/gpx-street-view && git pull'
   ```

Changes are live immediately; Caddy does not need to be reloaded.

3. Check the site:

   ```sh
   curl -I https://gpx-street-viewer.codemountain.be/
   ```

## Server configuration

The site block in `/etc/caddy/Caddyfile`:

```
gpx-street-viewer.codemountain.be {
	root * /home/bruno/projects/gpx-street-view
	file_server {
		hide .git README.md
	}
}
```

`hide` keeps the `.git` folder and this README from being served publicly.
After editing the Caddyfile, reload Caddy with `sudo systemctl reload caddy`.

If you add a new page, also add it to `sitemap.xml`.
