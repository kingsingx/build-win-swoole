# Remote Windows build for `php_swoole.dll`

This is the final one-click remote build workflow for:

- PHP `8.4`
- `x64`
- `NTS`
- Swoole `win32-event`
- GitHub-hosted `windows-2022` runner
- Hand-written Windows build steps using Swoole's own `winext` scripts

Workflow file:

- `.github/workflows/build-swoole-php85-nts.yml`

## What it does

1. Clones `swoole/swoole-src` branch `win32-event`
2. Sets up `PHP 8.4 / NTS`
3. Downloads Windows deps and PHP devel pack using Swoole's `winext` scripts
4. Runs the native Windows extension build script directly
5. Uploads `php_swoole.dll` as a workflow artifact
6. Optionally uploads assets to a GitHub release when triggered by a release event or matching tag

## How to use it

1. Create or open a GitHub repository.
2. Copy `.github/workflows/build-swoole-php85-nts.yml` into that repo.
3. Trigger it in one of these ways:

```text
- Actions tab -> Run workflow
- push to main
- push a tag like swoole-php84-nts-v1
- create a GitHub release
```

4. Download the workflow artifact from the Actions run page.

## Why this version is cleaner

- It is already pinned to `PHP 8.4 / NTS`, so you do not need to keep editing variables.
- It avoids `--enable-swoole-thread`, because that feature requires a ZTS build and does not belong in an NTS workflow.
- It bypasses the extension action's source auto-detection, which was the thing causing the earlier `config.w32` failures.

## Important notes

- This workflow is for the Windows native Swoole branch, not the mainstream Linux-first build path.
- The build still depends on the current compatibility state of `swoole-src` branch `win32-event` with PHP `8.4`.
- If you later need a TS build, create a separate workflow instead of mixing NTS and TS flags in one file.
