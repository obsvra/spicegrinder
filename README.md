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

| Build | For |
| --- | --- |
| `-windows.zip` | Windows x64, self-contained |
| `-mac-arm64.zip` | macOS Apple Silicon, self-contained |
| `-mac-x64.zip` | macOS Intel, self-contained |
| `-linux.zip` | Linux x64 / ARM64, self-contained |
| `-jre.zip` | Any OS, if you manage your own Java 25+ runtime |

The self-contained builds bundle the runtime, so there is nothing else to
install. Pick the JRE-only build if your organization manages its own Java.

### Verify your download

Every release ships a `SHA256SUMS.txt`:

```bash
shasum -a 256 -c SHA256SUMS.txt --ignore-missing
```

## What Free includes

The full core engine — every distribution, every core filter, deterministic
output, the CLI tools, and the desktop GUI — for models using numeric data, up to
20 nodes. Generation is unlimited and does not expire.

Pro adds complex data types, the business-object library (phone, SSN, credit
card, address, email), external data sources, custom components, and removes the
node limit. See [pricing](https://obsvra.com/get-spicegrinder).

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
