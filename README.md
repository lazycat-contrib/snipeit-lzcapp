# Snipe-IT (LazyCat LPK)

IT asset management for hardware, licenses and accessories.

- Upstream: https://github.com/grokability/snipe-it
- Image: `snipe/snipe-it:v8.8.3` (mirror mode, digest-matched)
- License: AGPL-3.0 (full text in `content/licenses/LICENSE`)
- Containers: app + MySQL 8.0

## Notes

- Clean first-run flow: `app/Http/Middleware/CheckForSetup.php` redirects every request to
  `/setup` while `Setting::setupCompleted()` is false, and bounces `/setup*` back to the app
  once setup is done. So the admin account is created by the user in the browser — no seeded
  credential, and the wizard closes itself.
- `APP_KEY` is required by `docker/startup.sh` (it exits if empty) and comes from a platform
  stable secret.
- The entrypoint runs `artisan migrate --force` automatically.
- Data on `/lzcapp/var/{mysql,storage}`.
- No mail service configured.
- Not yet verified on a real device.
