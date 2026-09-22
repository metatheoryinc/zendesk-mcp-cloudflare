# Vendored MCP worker

`levibe-mcp-worker-0.3.0.tgz` is built from the unchanged public source of
[`levibe/mcp-worker` v0.3.0](https://github.com/levibe/mcp-worker/tree/7cf54a7aec761488e5082d36bc80ae2cfa25cf82).

- Commit: `7cf54a7aec761488e5082d36bc80ae2cfa25cf82`
- License: MIT (included in the archive)
- SHA-256: `2daa400e60a7369f52c41c5b767db1e32521a04112c828871fdfa5d379b3b019`
- Built with Node 24.19.0 and upstream-pinned pnpm 10.32.1.
- Upstream build and all 220 tests passed before packaging.

The upstream GitHub Packages distribution returned `403 read_package` for the
configured account. This archive removes that registry permission requirement
while retaining the project's existing dependency version. It is a source build,
not a byte-for-byte copy of the inaccessible registry archive.

To rebuild from the repository root (use a fresh checkout directory):

```bash
git clone --branch v0.3.0 --depth 1 https://github.com/levibe/mcp-worker.git .wrangler/setup/mcp-worker
git -C .wrangler/setup/mcp-worker rev-parse HEAD
pnpm --dir .wrangler/setup/mcp-worker install --frozen-lockfile --ignore-scripts
pnpm --dir .wrangler/setup/mcp-worker run build
pnpm --dir .wrangler/setup/mcp-worker run test
pnpm --dir .wrangler/setup/mcp-worker --config.ignore-scripts=true pack --out "$PWD/vendor/levibe-mcp-worker-0.3.0.tgz"
pnpm install --lockfile-only
pnpm install --frozen-lockfile
pnpm run validate
```

Verify the commit before building. Packaging skips lifecycle scripts because the
build has already run and upstream's `prepare` also installs Git hooks. Record a
new checksum and regenerate the lockfile if the archive changes.
