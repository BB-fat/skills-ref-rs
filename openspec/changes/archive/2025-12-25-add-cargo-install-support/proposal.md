# Proposal: Add cargo install Support

**Change ID**: `add-cargo-install-support`  
**Status**: Draft  
**Created**: 2025-12-25

## Problem

Currently, the project has a binary named `skills-ref-rs` defined in Cargo.toml (line 10), but users expect to install and use the tool with the simpler command `skills-ref` after running `cargo install`. This naming inconsistency creates friction for users who want to install from crates.io or from source.

The current configuration:
- Package name: `skills-ref-rs` 
- Binary name: `skills-ref-rs`
- Desired command: `skills-ref`

## Proposed Solution

Rename the binary from `skills-ref-rs` to `skills-ref` in Cargo.toml while keeping the package name as `skills-ref-rs`. This is a minimal, non-breaking change that:

1. Allows users to run `cargo install skills-ref-rs` 
2. Installs the binary as `skills-ref` (without the `-rs` suffix)
3. Maintains the package name for crates.io consistency
4. Preserves the library crate name `skills_ref` unchanged

This approach follows Rust ecosystem conventions where the binary name can differ from the package name (e.g., `ripgrep` package installs `rg` binary).

## Scope

This change is **tightly scoped** to:
- Modifying the `[[bin]]` section in Cargo.toml
- Updating documentation (README.md, CLI spec) to reflect the new command name
- No code changes required
- No architectural changes

## User Impact

**Before**: Documentation shows `skills-ref-rs` but users want `skills-ref`  
**After**: Users can install with `cargo install skills-ref-rs` and run `skills-ref`

This aligns with user expectations stated in the request: "安装后的命令是 skills-ref" (installed command is skills-ref).

## Spec Deltas

- **installability**: New capability spec documenting package installation requirements

## Dependencies

None - this is a standalone change with no dependencies on other changes.

## Risks

**Low risk**: 
- Binary rename is straightforward
- Only affects new installations (existing local builds can rebuild)
- No API or library changes
- Documentation updates are mechanical

## Alternatives Considered

1. **Rename package to `skills-ref`**: Would lose the `-rs` suffix convention that signals Rust implementation
2. **Keep `skills-ref-rs` command**: Doesn't meet user requirements
3. **Create both binaries**: Unnecessary complexity

## Open Questions

None - the approach is straightforward and well-understood.
