# Security Policy

## Reporting a vulnerability

Report security issues privately through GitHub: open the [Security tab](https://github.com/nebinfra/nebguard-dist/security) of this repository and choose **Report a vulnerability**, or email <security@nebinfra.com>.

Please do not open public issues or pull requests for security reports.

We aim to acknowledge new reports within 3 business days and to keep you informed while we investigate. We follow coordinated disclosure: we ask that you give us a reasonable window to ship a fix before publishing details. There is no paid bounty program at this time; we are happy to credit reporters in the release notes on request.

NebGuard is a policy enforcement layer for AI coding assistants and autonomous agents, so bypasses are security bugs: a way to make a guarded action execute without its policy verdict (hook evasion, rule-matching gaps, TOCTOU between verdict and execution) is in scope and treated with the same severity as a conventional vulnerability.

## Scope

This repository is the public release home for NebGuard. In scope here:

- Vulnerabilities in the NebGuard binaries published on the [releases page](https://github.com/nebinfra/nebguard-dist/releases), including policy-bypass techniques as described above.
- Integrity or authenticity problems with any release asset: archives, `SHA256SUMS`, `.bundle` signature files, or SBOMs.
- Anything in this repository's install or verification instructions that could lead users into an unsafe state.

Issues in the Homebrew formula or Scoop manifest belong in [nebinfra/homebrew-tap](https://github.com/nebinfra/homebrew-tap) or [nebinfra/scoop-bucket](https://github.com/nebinfra/scoop-bucket). Issues with the published verification keys belong in [nebinfra/trust](https://github.com/nebinfra/trust).

## Verifying release artifacts

Every artifact ships with a sibling `.bundle` file containing the cosign signature and the Rekor transparency-log inclusion proof; the full walkthrough lives in this repository's [README](README.md#verify-a-release). Public keys live in [nebinfra/trust](https://github.com/nebinfra/trust); keys rotate quarterly and archived keys remain available for older releases.

```bash
cosign verify-blob \
  --key https://raw.githubusercontent.com/nebinfra/trust/main/cosign-keys/nebguard-prod.pub \
  --bundle nebguard_<version>_<os>_<arch>.tar.gz.bundle \
  nebguard_<version>_<os>_<arch>.tar.gz
```

An artifact that fails verification is itself a security report: please tell us immediately through the channels above and do not run the artifact.

## Supported versions

Security fixes ship forward in the newest release; only the latest release of NebGuard is supported. Older releases stay downloadable and remain signature-verifiable (archived keys in [nebinfra/trust](https://github.com/nebinfra/trust)), but they do not receive fixes.
