# CLIProxyAPI for LazyCat

LazyCat LPK v2 packaging for [CLIProxyAPI](https://github.com/router-for-me/CLIProxyAPI), an OpenAI/Gemini/Claude/Codex-compatible API gateway for CLI model subscriptions.

## Runtime

- Runs the requested `eceasy/cli-proxy-api:v7.2.149` image through the `docker.1ms.run` mirror.
- The HTTP API and bundled management panel use the LazyCat application domain on port 8317.
- OAuth callback ports 8085, 1455, 54545, 51121, and 11451 are exposed as TCP ingress.
- The setup wizard generates separate client and management keys. These two values are authoritative and are synchronized into the persistent configuration on every restart; other settings and additional API keys are preserved.
- The unsupported `config.yaml` file bind is replaced by a packaged template and first-run `setup_script`; later management-panel edits persist under `/lzcapp/var`.
- OAuth credentials, logs, and plugins are persisted separately.
- The management panel's credential import/export flows use the LazyCat file-picker injection.

The package uses the upstream `router-for-me` organization avatar as its 512×512 PNG icon because the source repository does not provide a standalone CLIProxyAPI product icon.

The LazyCat store already contains `router-for-me.cli-proxy-api`. This repository intentionally uses the distinct package ID `community.lazycat.app.cli-proxy-api` as requested.

## Build

```sh
lzc-cli project release -o dist/application.lpk
```

## GitHub Actions

The scheduled workflow follows stable SemVer tags for `eceasy/cli-proxy-api`, creates a versioned GitHub Release asset, and publishes only to the MiaoMiao private store.

Required repository or organization Secrets:

- `APPSTORE_URL`
- `APPSTORE_TOKEN`

Optional Secrets:

- `APP_ID`
- `PRIVATE_STORE_GROUP_CODES`
