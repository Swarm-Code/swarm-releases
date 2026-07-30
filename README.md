# SwarmOS stable releases

This repository is the public distribution surface for verified stable SwarmOS
TUI executables. Canonical source, review, tests, and release builds are managed
in the private `Swarm-Code/mono` repository.

## Latest release

Download the latest stable release from
[GitHub Releases](https://github.com/Swarm-Code/swarm-releases/releases/latest).

Published platforms:

| Operating system | Architecture | Executable |
| --- | --- | --- |
| Linux | amd64 | `swarmos-linux-amd64` |
| Linux | arm64 | `swarmos-linux-arm64` |
| macOS | amd64 | `swarmos-darwin-amd64` |
| macOS | arm64 | `swarmos-darwin-arm64` |
| Windows | amd64 | `swarmos-windows-amd64.exe` |

Every executable has an adjacent `.sha256` file. Download both files and verify
the checksum before installation.

Linux example:

```bash
sha256sum -c swarmos-linux-amd64.sha256
chmod +x swarmos-linux-amd64
./swarmos-linux-amd64 --version
```

On macOS, use `shasum -a 256 -c <checksum-file>` if `sha256sum` is not
installed.

Windows PowerShell example:

```powershell
$expected = (Get-Content .\swarmos-windows-amd64.exe.sha256).Split()[0]
$actual = (Get-FileHash .\swarmos-windows-amd64.exe -Algorithm SHA256).Hash.ToLower()
if ($actual -ne $expected) { throw "Checksum mismatch" }
.\swarmos-windows-amd64.exe --version
```

## Trust model

- Stable releases are immutable.
- Every target is built and executed on its native GitHub-hosted runner.
- Publication occurs only after all platform builds and checksums pass.
- The built-in updater uses this repository anonymously and fails closed when
  an expected executable or checksum is absent or invalid.

## License and security

Official binaries are proprietary software distributed under the
[SwarmCode Binary Distribution License](LICENSE). Third-party components remain
subject to their respective licenses; see
[THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md).

Report security issues through [SECURITY.md](SECURITY.md), not a public issue.
