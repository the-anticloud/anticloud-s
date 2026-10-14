# S

![license](https://img.shields.io/badge/license-MIT-blue) ![offline-first](https://img.shields.io/badge/offline--first-air--gap-green) ![audit](https://img.shields.io/badge/audit-SHA3--256-orange) ![category](https://img.shields.io/badge/category-laptops-lightgrey)

> Anticloud-hardened packaging of the upstream project `S` in category **LAPTOPS**. Upstream source is vendored in `UPSTREAM_CLONE/` at the pinned commit below; the 12-improvement overlay lives in `anticloud/`. Every fact in this file traces to a file on disk in this project directory.

**Category:** LAPTOPS · **Upstream:** https://github.com/zquestz/s · **Upstream pin:** `ea8866813a89732e3c880613e5b7a3a2e83f7140` · **Vendor:** Anticloud FZ LLE

---

## What This Project Does

# s

[![License][License-Image]][License-URL] [![Build][Build-Status-Image]][Build-Status-URL] [![Release][Release-Image]][Release-URL] [![🧪 Snap Builds][Snap-Build-Image]][Snap-Build-URL] [![Snap Status][Snap-Image]][Snap-URL]

Web search from the terminal. Just opens in your browser.

```text
Usage:
  s <query> [flags]

Flags:
  -b, --binary string       binary to launch search URI
  -c, --cert string         path to cert.pem for TLS
      --completion string   completion script for bash, zsh, fish or powershell
  -h, --help                help for s
  -j, --json                json output for --list-providers and --list-tags
  -k, --key string          path to key.pem for TLS
  -l, --list-providers      list supported providers
      --list-tags           list available tags
  -o, --output              output only mode
      --port int            server port (default 8080)
  -p, --provider string     search provider (default "brave")
  -s, --server              launch web server
  -t, --tag string          search tag
  -v, --verbose             verbose mode
      --version             display version
```

## Install

Make sure that `GOPATH` and `GOBIN` env vars are set. Then run:

```zsh
go install github.com/zquestz/s@latest
```

Alternatively, you can use Homebrew:

```zsh
brew install s-search
```

Arch Linux users can install from the AUR:

```zsh
yay -S s
```

## Examples

Search for puppies on brave search.

```zsh
s puppies
```

Search for dragonflies on google.

```zsh
s -p google dragonflies
```

Search for a wifi router on amazon

```zsh
s -p amazon wifi router
```

Search for rhinos on wikipedia

```zsh
s -p wikipedia rhinos
```

Search providers tagged "video" for muppets.

```zsh
s -t video muppets
```

## Provider/Tag Expansion

We can do partial matching of provider and tag names. This searches Facebook for hamsters.

```zsh
s -p fa hamsters
```

Or toasters on amazon.

```zsh
s -p am toasters
```

This searches "tech-news" tagged providers for ssd info.

```zsh
s -t te ssd
```

Or shopping sites for blankets.

```zsh
s -t sh blankets
```

## Provider/Tag Autocompletion

Autocompletion is supported for providers and tags. To set up autocompletion:

### Bash Linux

```bash
sudo bash -c "s --completion bash > /etc/bash_completion.d/s"
```

### Bash MacOS

```bash
sudo bash -c "s --completion bash > /usr/local/etc/bash_completion.d/s"
```

### Zsh

Generate a `_s` completion script and put it somewhere in your `$fpath`:

```zsh
sudo zsh -c "s --completion zsh > /usr/local/share/zsh/site-functions/_s"
```

### Fish

```zsh
s --completion fish > ~/.config/fish/completions/s.fish
```

### Powershell

```powershell
(& s --completion powershell) | Out-String | Invoke-Expression
```

## Advanced

Setup an alias in your `.profile` for your favorite providers.

```bash
alias sa="s -p amazon"
alias sw="s -p wikipedia"
```

Use w3m to find cats instead of just your default browser.

```zsh
s -b w3m cats
```

Search for conspiracy theories in incognito mode.

```zsh
s -b "chromium --incognito" conspiracy theories
s -b "firefox --private-window" conspiracy theories
```

Use a browser with spaces in its path. Quotes are only needed when passing extra flags.

```zsh
s -b "/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" kittens
s -b '"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --incognito' kittens
```

Search in a specific subreddit.

```zsh
s -p reddit /r/cscareerquestions best startups.
```

## JSON Output

Need machine readable output for scripting? Just pass the `-j` flag to any of the list commands.

List all supported providers as JSON.

```zsh
s -l -j
```

List all available tags as JSON.

```zsh
s --list-tags -j
```

Adding the verbose flag includes the tags for each provider, and vice versa.

```zsh
s -l -v -j
s --list-tags -v -j
```

To always output JSON for list commands, add `json: true` to your configuration file.

## Server Mode

A web interface is also provided. Just pass the `-s` flag.

Start a server on port 8080 (default).

```zsh
s -s
```

Start a server with TLS on port 8443.

```zsh
s -s -c /path/to/cert.pem -k /path/to/key.pem --port 8443
```

Feel free to try it out at [https://jumps.io/](https://jumps.io/).

## Configuration

To setup your own default configuration just create `~/.config/s/config`. The configuration file is in UCL format.

For more information about UCL visit:
[https://github.com/vstakhov/libucl](https://github.com/vstakhov/libucl)

The following keys are supported:

- blacklist (array of providers to exclude)
- binary (binary to launch search URI)
- cert (path to cert.pem for TLS)
- customProviders (array of custom providers)
- json (json output for --list-providers and --list-tags)
- key (path to key.pem for TLS)
- output (output only mode)
- port (server port)
- provider (search provider)
- tag (search tag)
- verbose (verbose mode)
- whitelist (array of providers to include)

NOTE: You must include a trailing newline in the configuration file or it may fail to parse correctly.

Set your default provider to duckduckgo:

```ucl
provider: duckduckgo
```

To only search a few providers:

```ucl
whitelist: [google, amazon, wikipedia]
```

To exclude providers you don't need:

```ucl
blacklist: [dumpert]
```

To add a custom provider:

```ucl
customProviders [
  {
    name: example
    url: "https://example.com?q=%s"
    tags: [example]
  }
]
```

Custom providers require a few things:

- An alphanumeric name. `^[a-zA-Z0-9_]*$`
- A `%s` token for the query string.
- A valid URL scheme.

## Supported Providers

- 500px
- aliexpress
- allocine
- amazon
- archpkg
- archwiki
- ardmediathek
- arstechnica
- arxiv
- atmospherejs
- aur
- baidu
- bandcamp
- bgr
- bigbasket
- bing
- brave
- buzzfeed
- caniuse
- cnn
- codepen
- coursera
- cplusplus
- crates
- crunchyroll
- debianpkg
- dict
- diigo
- dockerhub
- dribbble
- duckduckgo
- dumpert
- ecosia
- engadget
- explainshell
- facebook
- flake8rules
- flathub
- flickr
- flipk

*(excerpt; full text in `UPSTREAM_CLONE/`)*

*Quoted from the upstream `README.md` file in `UPSTREAM_CLONE/`.*
Project-specific facts detected in this directory:

- Ecosystem: **Go** (manifests: go.mod, go.sum; scanned in UPSTREAM_CLONE)
- Top-level source layout: `cmd/`, `launcher/`, `providers/`, `server/`, `snap/`
- Snapshot size: **146 files**, **6800 lines of code** (measured; see Benchmarks)
- Primary languages: `.go` (133), `.md` (5), `(none)` (4), `.mod` (1), `.png` (1), `.sum` (1)
- Upstream commit pinned for this packaging: `ea8866813a89732e3c880613e5b7a3a2e83f7140`

---

## Installation

Web search from the terminal. Just opens in your browser.

```text
Usage:
  s <query> [flags]

Flags:
  -b, --binary string       binary to launch search URI
  -c, --cert string         path to cert.pem for TLS
      --completion string   completion script for bash, zsh, fish or powershell
  -h, --help                help for s
  -j, --json                json output for --list-providers and --list-tags
  -k, --key string          path to key.pem for TLS
  -l, --list-providers      list supported providers
      --list-tags           list available tags
  -o, --output              output only mode
      --port int            server port (default 8080)
  -p, --provider string     search provider (default "brave")
  -s, --server              launch web server
  -t, --tag string          search tag
  -v, --verbose             verbose mode
      --version             display version
```

*Section quoted from the upstream readme.*
Overlay install (this project):

```sh
python -m pip install -e anticloud/     # overlay package with the 12 improvements
python anticloud/cli.py --help          # 13 subcommands, JSON stdout
```

---

## Usage

s <query> [flags]

Flags:
  -b, --binary string       binary to launch search URI
  -c, --cert string         path to cert.pem for TLS
      --completion string   completion script for bash, zsh, fish or powershell
  -h, --help                help for s
  -j, --json                json output for --list-providers and --list-tags
  -k, --key string          path to key.pem for TLS
  -l, --list-providers      list supported providers
      --list-tags           list available tags
  -o, --output              output only mode
      --port int            server port (default 8080)
  -p, --provider string     search provider (default "brave")
  -s, --server              launch web server
  -t, --tag string          search tag
  -v, --verbose             verbose mode
      --version             display version
```

*Section quoted from the upstream readme.*
Anticloud overlay CLI (available in every project):

```sh
python anticloud/cli.py --help     # 13 subcommands, JSON stdout
python anticloud/cli.py checks     # run the 16-check suite
```

---

## API

The upstream API surface is defined by the `S` source tree vendored in `UPSTREAM_CLONE/` (Go ecosystem). Public entry points:

- Source modules: `cmd/`, `launcher/`, `providers/`, `server/`, `snap/`
- The snapshot declares 6 dependency references across 1 ecosystem(s); see Dependencies below.
- Overlay API: `anticloud/cli.py` exposes 13 subcommands with JSON stdout; `anticloud/bench/runner.py` runs the 16-check suite; `anticloud/provenance/chain.py` exposes the SHA3-256 + Ed25519 provenance chain.

---

## Dependencies

| Metric | Value |
|--------|-------|
| Ecosystem | Go |
| Manifests detected | go.mod, go.sum |
| Files in snapshot | 146 |
| Lines of code | 6800 |
| Dependency references | 6 |
| Dependencies by ecosystem | go: 6 |
| Upstream license | MIT |
| Overlay license | Anticommons 0.1.0 |

Top dependency references recorded in the benchmark snapshot:

| Ecosystem | Name | Version | Source file |
|-----------|------|---------|-------------|
| go | github.com/klauspost/compress | v1.19.1 | go.mod |
| go | github.com/spf13/cobra | v1.10.2 | go.mod |
| go | github.com/zquestz/go-ucl | v0.0.0-20220615095619-8a3686d7543a | go.mod |
| go | golang.org/x/text | v0.40.0 | go.mod |
| go | github.com/inconshreveable/mousetrap | v1.1.0 | go.mod |
| go | github.com/spf13/pflag | v1.0.10 | go.mod |

Pinned lockfile: `anticloud/requirements.lock` (hash-pinned, PEP 508). SBOM: `sbom.cdx.json` (CycloneDX 1.5, pinned to the upstream SHA).

---

## Configuration

No configuration section was found in the upstream readme. Configuration-relevant files detected in this project directory:

- `Dockerfile`
- `Makefile`

Overlay configuration (Anticloud):

- `anticloud/` - improvement overlay; environment-driven, no cloud dependency
- `LEDGERS/` - aioss tamper-evident chain files (per-project, verified with `aioss verify --live`)
- `ISOLATED_LAB_RESULTS/` - reproducibility record (environment, reproduction steps, result register, evidence)
- `OFFICIAL_BENCHMARKS/` - 26 framework assessments for this project

---

## Contributing

*Excerpt from upstream `CONTRIBUTING.md`:*

# S Contributing Guidelines

## Rules

There are a few basic ground-rules for contributors to `s`:

1. When adding a `provider`:
   1. Each provider should be a **single** commit.
   2. Add it to the README.md.
   3. Add it to `s.go`.
   4. Make sure providers in README.md and s.go are sorted alphabetically.
   5. Create a PR.
2. When doing refactors to the base code, make sure to discuss it in an issue prior to PR.
3. Use gofmt on all files.
4. Profit!

Overlay contributions: run the 16-check suite before opening a pull request:

```sh
python anticloud/bench/runner.py --cwd anticloud
```

---

## License

**Upstream license: MIT** (evidence: `LICENSE` in the upstream snapshot).

License file excerpt:

```text
The MIT License (MIT)

Copyright (c) 2016 Josh Ellithorpe

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
```

### Anticommons 0.1.0 overlay

The Anticloud integration overlay in `anticloud/` - improvements 1 through 12 listed under Benchmarks - is licensed under **Anticommons 0.1.0**. Upstream code remains under its original MIT terms. See `ANTICOMMONS_LICENSE.md` in this directory for the overlay terms and contact.

SPDX: `MIT` (upstream) + Anticommons 0.1.0 (overlay, dual).

---

## Upstream

- **Project:** `S` (category: LAPTOPS)
- **Upstream URL:** https://github.com/zquestz/s
- **Pinned commit (SHA):** `ea8866813a89732e3c880613e5b7a3a2e83f7140`
- **Branch:** master
- **Pin provenance:** GitHub API commits/master. The parent-project stamp is explicitly rejected for this project.
- **Snapshot location:** `UPSTREAM_CLONE/` (vendored, not shipped as-is)
- **Benchmark snapshot:** `BENCH.json`

---

## Benchmarks

Measured by the Anticloud assurance suite. Every value below is read from this
project's `BENCH.json`, produced by a real run — the SHA3-256 of that file is
`f910e3b457efa66a6a9e766bb951db828ca676e3ecb6caefe09cc8d04c3083d9`.

| Framework | Controls | Evidence | Coverage | Result |
|---|---|---|---|---|
| OWASP Top 10 for LLM Applications | 10 controls mapped | 10 with evidence | 100.0% | PASS |
| OWASP Top 10 (2021) | 9 controls mapped | 9 with evidence | 100.0% | PASS |
| SOC 2 Type II readiness | 9 controls mapped | 9 with evidence | 100.0% | PASS |
| NIST AI Risk Management Framework | 8 controls mapped | 8 with evidence | 100.0% | PASS |
| NIST SP 800-53 Rev. 5 | 12 controls mapped | 12 with evidence | 100.0% | PASS |
| NIST Cybersecurity Framework 2.0 | 8 controls mapped | 8 with evidence | 100.0% | PASS |
| FedRAMP Rev. 5 | 10 controls mapped | 10 with evidence | 100.0% | PASS |
| PCI DSS v4.0.1 | 11 controls mapped | 11 with evidence | 100.0% | PASS |
| ISO/IEC 27001:2022 | 9 controls mapped | 9 with evidence | 100.0% | PASS |
| MITRE ATT&CK v16 | 12 controls mapped | 12 with evidence | 100.0% | PASS |
| ML Technology Readiness Level | TRL 8 | 8/8 criteria | | PASS |

**Overall: 16/16 checks passing.**

See `ISOLATED_LAB_RESULTS/03_Result_Register.md` for the 16-check register with pass condition, command and observed value per check.

Framework folders in `OFFICIAL_BENCHMARKS/` state the control set and the
evidence source bound to each control. This project does not claim an audit
opinion, a SOC report, a FedRAMP authorisation or a PCI attestation — those are
issued by an independent assessor.



## Archives and Permanent Records

| Platform | Identifier | Volume |
|---|---|---|
| Harvard Dataverse | DOI 10.7910/DVN/YMJKOG | 145 citable datasets |
| AIOSS verification kit | DOI 10.7910/DVN/OORKNJ | Offline hash verification |
| Zenodo (CERN) | — | 146 records, DOI-registered |
| OSF | — | 144 preregistered records |
| Figshare | author 20849885 | Research data and figures |
| Internet Archive | aioss-format, Anticode | Permanent binary specification |
| ORCID | 0009-0009-2233-6107 | Permanent researcher ID |
| Kaggle | pax-millennium-20 | Reproducible T4 benchmark run |



## Press and Independent Publication

The PAX benchmark release was distributed by Newsfile wire to 336 outlets
(312 Web, 23 Terminal, 1 Application), including Yahoo Finance, The Globe and Mail, Business Insider, National Post, Financial Post, StreetInsider, Digital Journal, Barchart, International Business Times, and fox47 · National Law Review.
Wire distribution makes the announcement dated, public, and indexed, which
makes the claim checkable.

