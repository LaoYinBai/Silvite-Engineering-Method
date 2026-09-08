# Silvite Architecture Evolution Skill Design

## Outcome

Add a complementary `silvite-architecture-evolution` Skill without expanding the existing `silvite-engineering-method` into a monolith. The new Skill governs large, staged architecture changes while the existing Skill remains the general engineering-governance layer.

The repository remains install-compatible for the existing root Skill. The new Skill is installed from its own top-level directory.

## Scope

In scope:

- Add `silvite-architecture-evolution/SKILL.md`.
- Add `silvite-architecture-evolution/agents/openai.yaml`.
- Add eight one-level reference files covering baselines, architecture audits, migration slices, compatibility/versioning, cross-platform and edition boundaries, release evidence, hermetic toolchains, and command security.
- Add repository-level architecture-evolution evaluation scenarios and results.
- Add a minimal routing note to the existing Skill.
- Update repository documentation, changelog, sources, and publication review.
- Normalize public repository references and the new commit author name to `LaoYinBai`.

Out of scope:

- No product source code changes.
- No rewrite of the three existing Git commits or their historical authors.
- No executable migration tooling or product-specific configuration.
- No project names, private endpoints, credentials, signing material, or internal implementation parameters.

## Skill Boundary

`silvite-engineering-method` remains the default for non-trivial engineering work: defining outcomes, controlling scope and permissions, locating failures, choosing a minimal loop, preserving reversibility, and reporting evidence accurately.

`silvite-architecture-evolution` is additionally loaded when work involves multi-stage architecture migration, underlying subsystem replacement, protocol evolution, cross-platform unification, multi-repository or multi-edition synchronization, compatibility windows, or release migration gates.

The new Skill must require the existing Skill as background rather than repeat its general rules.

## Runtime Structure

```text
silvite-architecture-evolution/
├── SKILL.md
├── agents/
│   └── openai.yaml
└── references/
    ├── baseline-and-invariants.md
    ├── architecture-audit.md
    ├── migration-slicing.md
    ├── compatibility-and-versioning.md
    ├── cross-platform-and-editions.md
    ├── release-evidence-gates.md
    ├── hermetic-toolchains.md
    └── command-security-gate.md
```

`SKILL.md` stays below 500 lines and contains only the trigger boundary, mandatory phase gates, reference routing, concise templates, red flags, and completion contract. Detailed matrices and checklists live in the eight direct references. The Skill folder contains no README or changelog.

## Architecture-Evolution Workflow

1. Classify the task and load the companion Skill only for architecture-evolution categories.
2. Freeze a recoverable Known-Good baseline before cross-module writes.
3. Map the current architecture, including ownership, lifecycle, state, dependencies, side effects, platform/edition/repository differences, and fallback paths.
4. Define behavior invariants and information-exposure boundaries before designing the target architecture.
5. Admit future extension points only for explicit capabilities with stable semantics, compatibility rules, fallback behavior, tests, and deletion conditions.
6. Create a migration ledger of end-to-end slices.
7. Migrate high-coupling paths serially in dependency order, allowing parallel work only for independent read-only audits or verification.
8. Verify every slice and advance its state only when evidence supports that state.
9. Pass compatibility, release-identity, artifact, installation, upgrade, and rollback gates before describing the migration as complete.
10. Preserve a resumable progress record whenever work stops.

## Required Gates

### Baseline and invariants

Cross-module writes cannot start without a recorded branch, HEAD, worktree state, version/build/commit/channel, Known-Good artifact and behavior, test evidence, user data/configuration identity, known defects, and verified rollback target.

Acceptance is based on preserved behavior and explicit intended changes, not architectural aesthetics.

### Migration slicing

Each ledger entry records the observable outcome, current and target entry points, invariants, touched modules, compatibility strategy, tests, rollback point, enablement gate, retirement gate, and one of `Planned`, `Implemented`, `Verified`, `Migrated`, or `Retired`.

The default dependency order is contracts/models, pure logic, platform adapters, state machines, callers, UI, build/package, then release.

### Compatibility and identity

The Skill distinguishes shared behavior and contracts from shared source or commit identity. Cross-repository synchronization uses a semantic matrix; mechanical cherry-pick success is not the goal.

Before a distributable build or release, independently verify ProductVersion, globally monotonic Build, source Commit, Channel, updater ordering behavior, pre-release ordering, package identity, signing/upgrade identity, Tag, manifest, assets, upgrade path, user-data preservation, and rollback.

### Information exposure

Define where ProductVersion, Build, Commit, Channel, tokens, error codes, and diagnostics may appear. UI receives only information it needs to display. Credentials never enter UI, logs, package metadata, or publication artifacts.

### Command behavior security

Read-only intent does not imply low behavioral risk. Before commands involving reflection, non-public APIs, credential recovery, authenticated binary download, execution, signing material, or security-product changes, stop and choose a normal product path, controlled test credential, signed manifest/hash verification, or explicitly authorized isolated environment. Never recommend disabling Defender or adding exclusions to make a suspicious chain run.

### Evidence states

Report these states separately and never promote one into the next without evidence:

```text
Code Complete
→ Tests Passed
→ Build Produced
→ Artifact Inspected
→ Remote Published
→ Remote Independently Verified
→ Installed
→ Upgrade Verified
→ User Accepted
```

## Evaluation Design

Repository-level evaluation material will cover these eight required scenarios:

1. Same ProductVersion with a higher Build is rejected by an updater requiring both fields to increase.
2. A shared change crosses repositories and incorrectly imports edition-only behavior.
3. Internal Build identity leaks into ordinary UI.
4. Discovery implicitly triggers Connecting.
5. System ADB contaminates a bundled hermetic toolchain.
6. Reflection restores a credential and downloads executables, triggering endpoint security.
7. Work resumes after interruption using an explicit progress record.
8. A refactor modifies an explicitly excluded Web repository.

RED runs receive only raw scenarios and the existing general Skill. GREEN runs receive the raw scenarios plus the new Skill. Expected answers are kept out of agent prompts. Results record observed decisions, evidence, failures, and residual gaps rather than marketing claims.

## Documentation and Ownership

Update the root README to describe the two-Skill model, triggers, installation, structure, evaluation approach, and experimental status. Replace the stale clone owner with `LaoYinBai` and ensure repository-visible owner references are consistent.

Set repository-local `user.name` to `LaoYinBai` for new commits. Preserve existing commit history and authors because rewriting published history would be destructive and is not required for repository-visible consistency going forward.

## Verification

- Run `quick_validate.py` against both Skill directories.
- Confirm frontmatter names, descriptions, directory names, and `agents/openai.yaml` constraints.
- Confirm the new `SKILL.md` is under 500 lines and all reference links resolve one level deep.
- Run RED and GREEN forward evaluations with minimal isolated context and manually review every result.
- Scan for private/project-specific identifiers, credentials, stale owner names, Windows-style internal reference paths, placeholders, and contradictory completion language.
- Verify Git diff scope, working-tree state, remote identity, commit identity, and push result.

## Stop Conditions

Stop before implementation if the written design is not approved. During implementation, stop and report if evaluation requires access to production systems, credentials, signing material, private repositories, or destructive history rewriting. Such access is not part of this change.
