# Muxer — releases

Download channel for **[Muxer](https://github.com/arealhobo/Muxer)**, a Windows/Linux
terminal multiplexer. This repository holds **only** published binaries and their signed
update manifests — the source lives in a separate private repository.

## Downloads

Grab the latest build from the [**Releases**](https://github.com/arealhobo/Muxer-releases/releases)
page. On Windows, run `Muxer.exe` once and choose **Install** when prompted to set up
automatic updates.

## Auto-update

Muxer checks this repo for newer builds and verifies every download before applying it:

- The app fetches `releases/latest/download/manifest.json` (no API, no rate limits).
- The manifest is signed with an **offline ECDSA P-256** key; the app verifies it against
  an embedded public key before trusting any field, then confirms the downloaded exe's
  SHA-256 matches the signed manifest.
- Updates are strictly forward-only (a signed manifest older than your build is refused).

A valid signature from a compromised account still can't forge an update, because the
signing key is never stored on GitHub or in CI.

## Verifying a download manually

Each release lists the exe's SHA-256 in its `manifest.json`. To check a download:

```powershell
(Get-FileHash Muxer.exe -Algorithm SHA256).Hash.ToLower()
```
