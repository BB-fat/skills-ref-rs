# Tasks: add-cargo-install-support

## Implementation Order

- [x] **Update binary name in Cargo.toml**
  - Change `[[bin]]` section's `name` field from "skills-ref-rs" to "skills-ref"
  - Keep package name as "skills-ref-rs"
  - **Validates**: Run `cargo build` to ensure configuration is valid
  - **Delivers**: Correct binary name in build output

- [x] **Update README.md CLI examples**
  - Replace all occurrences of `skills-ref-rs validate` with `skills-ref validate`
  - Replace all occurrences of `skills-ref-rs read-properties` with `skills-ref read-properties`
  - Replace all occurrences of `skills-ref-rs to-prompt` with `skills-ref to-prompt`
  - Replace `skills-ref-rs --help` and `skills-ref-rs --version` examples
  - Keep `cargo add skills-ref-rs` unchanged (package installation)
  - Added CLI installation section with `cargo install skills-ref-rs`
  - **Validates**: Review diff to ensure all command references updated but package name preserved
  - **Delivers**: User-facing documentation with correct command name

- [x] **Update CLI spec (openspec/specs/cli/spec.md)**
  - Replace `skills-ref-rs validate` with `skills-ref validate` in all scenarios
  - Replace `skills-ref-rs read-properties` with `skills-ref read-properties` in all scenarios
  - Replace `skills-ref-rs to-prompt` with `skills-ref to-prompt` in all scenarios
  - Replace `skills-ref-rs --version` and `skills-ref-rs --help` references
  - **Validates**: Run `openspec validate --strict` on the spec
  - **Delivers**: Specification that matches actual command behavior

- [x] **Test installation from source**
  - Run `cargo install --path .` to install locally
  - Verify `skills-ref` command is available in PATH
  - Test `skills-ref --version` succeeds
  - Test `skills-ref validate ./pdf` works correctly (validated with pdf skill)
  - **Validates**: Manual verification of installation and basic functionality
  - **Delivers**: Confidence that cargo install workflow works

- [x] **Run full test suite**
  - Execute `cargo test` to ensure no integration tests broke
  - Verify all tests pass (41 unit tests + 5 integration tests + 1 doc test = 47 total)
  - **Validates**: Automated test coverage
  - **Delivers**: Regression confidence

## Notes

- **No code changes required**: This is purely configuration and documentation
- **No breaking changes**: The library API (`skills_ref`) remains unchanged
- **Can be done in sequence**: Each task builds on the previous one
- **Fast implementation**: All tasks are mechanical edits with clear validation criteria
