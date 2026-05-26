# Remote Windows build for `php_swoole.dll`

This is the final one-click remote build workflow for:

- PHP `8.5`
- `x64`
- `NTS`
- Swoole `win32-event`
- GitHub-hosted `windows-2022` runner

Workflow file:

- `.github/workflows/build-swoole-php85-nts.yml`

## What it does

1. Uses `php/php-windows-builder/extension@v1`
2. Fetches `https://github.com/swoole/swoole-src`
3. Builds ref `win32-event`
4. Builds `php_swoole.dll` for `PHP 8.5 / x64 / NTS`
5. Uploads the build artifact automatically
6. Optionally uploads assets to a GitHub release when triggered by a release event or matching tag

## How to use it

1. Create or open a GitHub repository.
2. Copy `.github/workflows/build-swoole-php85-nts.yml` into that repo.
3. Trigger it in one of these ways:

```text
- Actions tab -> Run workflow
- push to main
- push a tag like swoole-php85-nts-v1
- create a GitHub release
```

4. Download the workflow artifact from the Actions run page.

## Why this version is cleaner

- It uses the official `php/php-windows-builder` action instead of manually scripting the Windows toolchain.
- It is already pinned to `PHP 8.5 / NTS`, so you do not need to keep editing variables.
- It avoids `--enable-swoole-thread`, because that feature requires a ZTS build and does not belong in an NTS workflow.

## Important notes

- This workflow is for the Windows native Swoole branch, not the mainstream Linux-first build path.
- The build still depends on the current compatibility state of `swoole-src` branch `win32-event` with PHP `8.5`.
- If you later need a TS build, create a separate workflow instead of mixing NTS and TS flags in one file.
