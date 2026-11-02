![spicegrinder-icon](assets/spicegrinder-icon.png)
# Verifying a SpiceGrinder download

> © 2026 Obsvra. This document describes SpiceGrinder and is provided to help you evaluate and use it. It is not a license to reproduce, adapt, or use this material to build a competing product or service. Full terms: the SpiceGrinder EULA.

**Where things stand (1.0.0).** The Mac and Windows downloads are signed, every release jar is signed with SpiceGrinder's own code-signing certificate, and every release comes with a checksum file.

## What you can check today

- **Any download, any platform: the checksum.** Each release includes `SHA256SUMS.txt`. Put it next to the files you downloaded and run `shasum -a 256 -c SHA256SUMS.txt --ignore-missing` (on Windows, `Get-FileHash -Algorithm SHA256 <file>` and compare by eye). A match means the file is exactly what was published.
- **Mac apps and installers.** They are signed with an Apple Developer ID and notarized by Apple. In Terminal: `codesign --verify --deep --strict --verbose=2 "SpiceGrinder Free.app"` and `spctl --assess --type exec --verbose=2 "SpiceGrinder Free.app"` (it should say `accepted` and `source=Notarized Developer ID`).
- **Windows installers and programs.** They are signed by Obsvra. In File Explorer, open a file's **Properties > Digital Signatures**, or in PowerShell run `Get-AuthenticodeSignature <file>`; the status should be `Valid`.
- **The jars, any platform.** `jarsigner -verify spicegrinder-1.0.0-pro.jar` should say `jar verified`; see "The jar signature" below.
- **Linux.** The `.deb` and `.AppImage` are covered by the checksum only for now.

**If macOS stops a SpiceGrinder app or tool.** The first time you open a downloaded app, macOS asks whether you want to open something downloaded from the internet; click **Open**. That question is normal. A warning that Apple "could not verify" the app, or a command-line tool that stops with `Killed: 9` the first time you run it from Terminal, means that copy is not a notarized one. Run the `spctl` check above on it (for the command-line package, on the `SpiceGrinder-Free.app` or `SpiceGrinder-Pro.app` you unzipped), and download it again from the official release page.

## The jar signature

Every SpiceGrinder release jar (`spicegrinder-<version>-free.jar` / `spicegrinder-<version>-pro.jar`, whether you got it as a standalone jar or unzipped it from inside a jpackage app-image) is signed with SpiceGrinder's own code-signing certificate. This is a self-signed certificate, not one issued by a public certificate authority; see "What this does and doesn't prove" below for exactly what that means. The short version: it lets you confirm a jar you have is byte-for-byte what was actually signed and shipped, not a copy someone modified afterward.

## The certificate

The public certificate is [`spicegrinder-codesign.pem`](spicegrinder-codesign.pem), shipped alongside this doc in every release. Its fingerprints, so you can confirm you have the right one without even importing it:

```
SHA256: C2:17:40:BB:24:7B:8E:EF:8E:0A:A1:0D:0B:C9:B3:00:38:97:FD:38:DE:5C:89:86:E6:78:E4:25:E2:22:77:BC
SHA1:   D3:AC:4F:D2:09:3E:64:CD:CB:1B:70:B3:81:F9:01:0A:85:BA:B1:7E
```

Owner: `CN=SpiceGrinder Code Signing, O=Obsvra, C=US`. Valid 2026-10-23 through 2036-10-20.

## Quick check

Two commands, both part of every JDK, neither needs the certificate file:

```bash
jarsigner -verify -verbose -certs spicegrinder-1.0.0-pro.jar
```

Confirms the jar hasn't been altered since signing. Look for `jar verified` and a line naming `CN=SpiceGrinder Code Signing, O=Obsvra, C=US`. If any entry had been tampered with, this fails outright instead.

```bash
keytool -printcert -jarfile spicegrinder-1.0.0-pro.jar
```

Prints the signing certificate's actual fingerprints. Compare the `SHA256`/`SHA1` lines it prints against the ones published above — if they match, the jar was signed with SpiceGrinder's real certificate, not a substitute.

If any class in the jar had been altered after signing, `jarsigner -verify` fails outright, and the JVM itself refuses to load the tampered class at runtime with a `SecurityException` — this isn't just a check you can run manually, it's enforced automatically every time the jar runs.

## What this does and doesn't prove

**Does prove:** the jar you have matches exactly what was signed under this certificate. Tampering after signing — a modified `.class` file, a swapped-in malicious component, anything — breaks the signature and both `jarsigner -verify` and the JVM's own class loading will say so.

**Does not prove, on its own:** that this certificate itself was issued by an independently-verified "SpiceGrinder" identity the way a certificate from a public CA (DigiCert, Sectigo, etc.) would be. This is a self-signed certificate — nobody but SpiceGrinder vetted it. The trust anchor is this page: you're trusting that the fingerprint published here, on SpiceGrinder's own site/repo, is the real one. If you obtained a jar from somewhere other than an official SpiceGrinder source and want independent identity assurance (not just tamper-detection), that's a real limitation of a self-signed certificate — cross-check the fingerprint against multiple official channels rather than relying on this page alone.
