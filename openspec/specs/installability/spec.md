# installability Specification

## Purpose
TBD - created by archiving change add-cargo-install-support. Update Purpose after archive.
## Requirements
### Requirement: Binary Installation via cargo install

The package SHALL be installable using standard Cargo tooling with a predictable binary name.

#### Scenario: Install from source
- **GIVEN** a user has Rust and Cargo installed
- **WHEN** they run `cargo install --path .` from the project root
- **THEN** the `skills-ref` binary SHALL be installed to `~/.cargo/bin/`
- **AND** running `skills-ref --version` SHALL succeed

#### Scenario: Install from crates.io
- **GIVEN** the package is published to crates.io
- **WHEN** a user runs `cargo install skills-ref-rs`
- **THEN** the `skills-ref` binary SHALL be installed
- **AND** the binary SHALL be immediately available in the user's PATH

#### Scenario: Binary name matches user expectations
- **WHEN** the package is installed via any method
- **THEN** the installed command SHALL be named `skills-ref` (without `-rs` suffix)
- **AND** all existing subcommands (validate, read-properties, to-prompt) SHALL work with the new binary name

### Requirement: Package Metadata for Distribution

The Cargo.toml SHALL contain complete metadata required for crates.io publication.

#### Scenario: Required metadata fields present
- **WHEN** validating the Cargo.toml manifest
- **THEN** it SHALL include a `name` field set to "skills-ref-rs"
- **AND** it SHALL include a `version` field
- **AND** it SHALL include a `description` field
- **AND** it SHALL include a `license` field
- **AND** it SHALL include a `repository` field

#### Scenario: Binary configuration
- **WHEN** examining the `[[bin]]` section
- **THEN** the binary `name` SHALL be "skills-ref"
- **AND** the `path` SHALL point to "src/main.rs"

### Requirement: Documentation Reflects Installed Command Name

All user-facing documentation SHALL use the installed command name `skills-ref`.

#### Scenario: README usage examples
- **WHEN** reading the README.md
- **THEN** all CLI examples SHALL show `skills-ref` as the command
- **AND** no references to `skills-ref-rs` as a command SHALL remain (except in package installation commands)

#### Scenario: CLI spec consistency  
- **WHEN** reviewing the cli specification
- **THEN** all scenario descriptions SHALL use `skills-ref` as the command name
- **AND** examples like `skills-ref validate <path>` SHALL replace `skills-ref-rs validate <path>`

