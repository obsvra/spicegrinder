# SpiceGrinder

Deterministic synthetic data, generated from a model of your own domain.

SpiceGrinder lets you describe the shape of your data — entities, relationships,
and distributions — and generate datasets at any scale from that description.
Nothing is copied from production, so there is no PII or PHI to protect and no
compliance review to wait on. The same model plus the same seed produces the same
data every time, on any machine.

**This repository hosts the public downloads for SpiceGrinder Free.**
Full documentation, pricing, and benchmarks are at **https://obsvra.com**.

## Download

Get the latest build from [Releases](https://github.com/obsvra/spicegrinder/releases/latest).

You need one file. Each has its own Java runtime, so there is no Java to install.

| Platform | Desktop installer (the whole product) | CLI zip (no desktop app) |
| --- | --- | --- |
| Windows x64 | `-Desktop-windows-setup.exe` (no admin needed) or `-Desktop-windows.msi` (all users) | `-windows.zip` |
| macOS Apple Silicon | `-Desktop-mac-arm64.dmg` | `-mac-arm64.zip` |
| macOS Intel | `-Desktop-mac-x64.dmg` | `-mac-x64.zip` |
| Linux x64 | `-Desktop-linux.AppImage` or `-Desktop-linux.deb` | `-linux.zip` |
| Linux ARM64 | `-Desktop-linux-arm64.AppImage` or `-Desktop-linux-arm64.deb` | `-linux-arm64.zip` |

**Desktop installer:** the whole product. It has the desktop app (the model editor), all
the command-line tools, including `grind` and `experiment`, the MCP server, docs, the User
Manual, sample models and agent skills. Most people want this one. The Windows setup `.exe`
and Linux `.deb` add the tools to your PATH; the `.dmg`, `.msi` and `.AppImage` don't yet,
and the User Manual shows how. On Windows, run the format tool as `format-model`, because
`format` alone runs the Windows disk format command.

**CLI zip:** the same tools, MCP server, docs, samples and skills, with no desktop app.
Choose it for servers, CI and anywhere you don't want the desktop app. You set up your
PATH yourself; the User Manual shows how.

### Other downloads

- `-jre.zip`: any OS, only if you manage your own Java 25+ runtime. It has `grind`,
  `experiment`, `analyze`, `validate`, `compare` and `format`, plus docs and samples, but
  no `list`, no MCP server and no skills. Most people should pick the desktop installer or
  the CLI zip for their platform.
- `SpiceGrinder-Skills-1.0.0.zip`: the agent skills on their own, with no engine.

### Verify your download

Every release ships a `SHA256SUMS.txt`:

```bash
shasum -a 256 -c SHA256SUMS.txt --ignore-missing
```

## What Free includes

The full core engine, with every distribution, every core filter and deterministic
output, for models using numeric data, up to 20 nodes. Generation is unlimited and does
not expire. The desktop installer has the desktop app, the command-line tools, the MCP
server, docs, samples and skills; the CLI zip has all of that except the desktop app.

Pro adds complex data types, the business-object library (phone, SSN, credit card,
address, email), external data sources, custom components, and removes the node limit.
See [pricing](https://obsvra.com/get-spicegrinder).

## Source

SpiceGrinder itself is closed-source; this repository distributes the Free
builds rather than the engine. What *is* open lives in
**[spicegrinder-cookbook](https://github.com/obsvra/spicegrinder-cookbook)** —
agent skills, worked examples, and community models.

## Links

- [Documentation](https://obsvra.com/docs)
- [Learn](https://obsvra.com/learn) — modeling, ops, and agent tracks
- [Benchmarks](https://obsvra.com/benchmarks) — verified throughput, with the model file to reproduce it
- [Security & trust](https://obsvra.com/security)

Questions: sales@obsvra.com

## License

SpiceGrinder Free is proprietary software, not open source. See
[LICENSE-FREE.txt](LICENSE-FREE.txt) and the terms included with each download.
