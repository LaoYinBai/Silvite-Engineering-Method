# Silvite Architecture Evolution Skill Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Add and publish a validated `silvite-architecture-evolution` Skill that complements the existing general engineering method with staged architecture-migration gates.

**Architecture:** Keep the existing root Skill install-compatible and add a self-contained second Skill in `silvite-architecture-evolution/`. Put detailed operational guidance in eight one-level references, keep evaluations and publication records at repository level, and validate behavior through RED/GREEN isolated-agent scenarios before release.

**Tech Stack:** Markdown Agent Skills, YAML UI metadata, Python `skill-creator` validators, Git, isolated Codex subagents.

**Spec:** `docs/superpowers/specs/2026-09-08-architecture-evolution-skill-design.md`

## Global Constraints

- Keep the existing root `silvite-engineering-method` install layout compatible.
- Keep `silvite-architecture-evolution/SKILL.md` below 500 lines.
- Keep all new Skill references exactly one level below `SKILL.md`.
- Do not add README or CHANGELOG files inside `silvite-architecture-evolution/`.
- Do not modify any product source repository or access production systems, credentials, signing material, or private endpoints.
- Use only generalized, public-safe engineering rules; do not name private products, repository services, or private repositories in runtime Skill content or evaluations.
- Normalize repository-visible GitHub ownership to `LaoYinBai`; preserve existing published commit authors.
- Do not claim a later evidence state from an earlier one.

---

### Task 1: RED Evaluation Baseline

**Files:**

- Create: `evals/architecture-evolution-scenarios.md`
- Create: `evals/architecture-evolution-results-v0.2.md`
- Modify: `evals/README.md`

**Interfaces:**

- Consumes: the approved design spec and existing `silvite-engineering-method` only.
- Produces: eight raw prompts, a stable scoring rubric, and verbatim or faithful baseline observations that the new Skill must address.

- [ ] **Step 1: Write the eight pressure scenarios before writing the new Skill**

  Include one raw prompt for each behavior: same ProductVersion/higher Build update rejection; cross-repository edition leakage; Build exposed in ordinary UI; Discovery implicitly starts Connecting; system ADB contaminates a bundled toolchain; reflection restores credentials and downloads executable artifacts; interrupted work resumes without a trustworthy progress record; an explicitly excluded Web repository is modified.

  Each prompt combines at least three pressures from time, authority, sunk cost, economic impact, fatigue, and social pressure. Prompts force an actual decision and omit expected behavior.

- [ ] **Step 2: Run isolated RED agents without the new Skill**

  Give each agent only one raw prompt plus the existing general Skill path. Do not include the design spec, rubric, expected answer, suspected failure, or other agents' output. Use read-only hypothetical tasks so evaluation cannot affect external systems.

- [ ] **Step 3: Record observed baseline behavior**

  In `architecture-evolution-results-v0.2.md`, record for every scenario: decision, missing gate, rationalization, pass/fail, and which pressure exposed the gap. Preserve exact short phrases when useful; do not invent failures when the control already behaves correctly.

- [ ] **Step 4: Verify RED integrity**

  Manually read every result. Confirm at least one observed gap is relevant to each rule added to the new Skill. If a scenario does not expose a gap, label the existing model behavior as already safe and do not inflate the new guidance to claim improvement.

- [ ] **Step 5: Commit the RED artifacts**

  ```powershell
  git add -- evals/architecture-evolution-scenarios.md evals/architecture-evolution-results-v0.2.md evals/README.md
  git commit -m "test: add architecture evolution baselines"
  ```

### Task 2: Initialize the Companion Skill and Core Contract

**Files:**

- Create: `silvite-architecture-evolution/SKILL.md`
- Create: `silvite-architecture-evolution/agents/openai.yaml`
- Create: `silvite-architecture-evolution/references/`

**Interfaces:**

- Consumes: Task 1 baseline failures and the `skill-creator` initialization scripts.
- Produces: discoverable Skill metadata, a concise mandatory workflow, direct reference routing, evidence states, red flags, and a UI invocation prompt.

- [ ] **Step 1: Initialize the exact folder structure**

  Run `init_skill.py silvite-architecture-evolution --path . --resources references` with interface values:

  ```text
  display_name=Silvite Architecture Evolution
  short_description=Guide staged, compatible architecture migrations
  default_prompt=Use $silvite-architecture-evolution to plan and execute this staged architecture migration safely.
  ```

- [ ] **Step 2: Verify the generated skeleton fails completeness review**

  Confirm the generated `SKILL.md` still contains template markers and lacks the approved phase gates. This is the content-level failing state that Task 2 replaces; do not treat generated boilerplate as usable.

- [ ] **Step 3: Write the minimal core Skill**

  Use frontmatter name `silvite-architecture-evolution` and a third-person `Use when...` description containing concrete triggers: multi-stage cross-module migration, subsystem replacement, protocol evolution, cross-platform unification, multi-edition/multi-repository compatibility, and release migration.

  Require `silvite-engineering-method` as background. Add the phase sequence: classify, freeze baseline, audit current architecture, define invariants, design admitted boundaries, create migration ledger, migrate in dependency order, verify each slice, pass release gates, preserve resumable state.

  Add the nine evidence states exactly as specified and prohibit promotion without evidence. Link all eight references directly from `SKILL.md`. Include a quick-reference gate table, common mistakes, red flags, and a concise migration-ledger template.

- [ ] **Step 4: Validate the generated metadata shape**

  Confirm `agents/openai.yaml` contains only quoted interface values requested above and its default prompt explicitly mentions `$silvite-architecture-evolution`.

- [ ] **Step 5: Commit the core contract with its references directory placeholder removed**

  Do not commit empty directories or generated example files. Commit Task 2 together with Task 3 after the references exist and validation passes.

### Task 3: Implement Baseline, Audit, and Migration References

**Files:**

- Create: `silvite-architecture-evolution/references/baseline-and-invariants.md`
- Create: `silvite-architecture-evolution/references/architecture-audit.md`
- Create: `silvite-architecture-evolution/references/migration-slicing.md`

**Interfaces:**

- Consumes: core workflow and RED failures from Tasks 1–2.
- Produces: exact baseline, invariant, architecture-map, migration-ledger, concurrency, retirement, and resumable-progress contracts.

- [ ] **Step 1: Write baseline and invariant gates**

  Define required version/build/commit/channel, Git, artifact, Known-Good behavior, defect, test, data/configuration, upgrade identity, and rollback fields. Define an information-exposure matrix for ProductVersion, Build, Commit, Channel, tokens, error codes, and diagnostics across UI, logs, crash reports, package metadata, network requests, updater, and release manifests.

- [ ] **Step 2: Write the current-architecture audit**

  Cover UI, application, state machine, protocol, transport, platform adaptation, and external systems. Require dependency direction, state ownership, lifecycle, concurrency, persistence, permissions, errors, side effects, fallback, toolchain boundaries, platform duplication, edition differences, and repository differences.

  Treat Discovery and Connecting as distinct capabilities and state transitions; discovery cannot acquire connection authority implicitly.

- [ ] **Step 3: Write migration slicing and resumption rules**

  Define the complete ledger schema and state transitions. Require one writer per high-coupling behavior boundary, dependency-order migration, explicit enablement and retirement gates, and a resumable record containing current phase, completed/incomplete slices, Git state, tests, last Known-Good, next unique entry point, and unverified risks.

- [ ] **Step 4: Review against the three relevant RED outputs**

  Check that the rules directly address implicit Connecting, unsafe resumption, and excluded-scope writes without embedding those expected answers in future evaluation prompts.

### Task 4: Implement Compatibility and Release References

**Files:**

- Create: `silvite-architecture-evolution/references/compatibility-and-versioning.md`
- Create: `silvite-architecture-evolution/references/cross-platform-and-editions.md`
- Create: `silvite-architecture-evolution/references/release-evidence-gates.md`

**Interfaces:**

- Consumes: Task 3 invariants and migration states.
- Produces: semantic synchronization matrices, capability/version compatibility rules, release identity checks, and staged evidence contracts.

- [ ] **Step 1: Define compatibility and extension-point admission**

  Require explicit future capability, known variation axis, stable boundary semantics, a real consumer or negligible reservation cost, capability negotiation, fallback, tests, and deletion conditions. Reject universal interfaces, unused plugin points, boolean-controlled false unification, and speculative whole-system rewrites.

  Include updater ordering analysis where ProductVersion and Build may form a lexicographic, conjunctive, or channel-specific predicate; require testing the actual installed client's comparison rule.

- [ ] **Step 2: Define cross-platform, edition, and repository synchronization**

  Provide a matrix distinguishing shared contract/behavior, platform-only implementation, edition-only capability, repository-only release logic, and forbidden code/credential transfer. State that behavioral equivalence may legitimately produce different directories and commits.

- [ ] **Step 3: Define release and evidence gates**

  Check version, globally monotonic Build, source Commit, Channel, prerelease ordering, package ID, signing identity, UpgradeCode or platform equivalent, user-data preservation, manifest, asset, Tag, hashes, old-to-new upgrade, excluded repositories, and rollback.

  Define evidence required for each of the nine states and require remote verification through an independent supported path.

- [ ] **Step 4: Review against the three relevant RED outputs**

  Confirm the rules address version/build rejection, edition leakage, and Build/UI leakage at the correct architectural boundaries.

### Task 5: Implement Hermetic Toolchain and Command-Security References

**Files:**

- Create: `silvite-architecture-evolution/references/hermetic-toolchains.md`
- Create: `silvite-architecture-evolution/references/command-security-gate.md`

**Interfaces:**

- Consumes: architecture ownership and release evidence contracts.
- Produces: tool-resolution isolation rules and a behavior-chain risk gate for commands that may be nominally read-only.

- [ ] **Step 1: Define hermetic toolchain boundaries**

  Require explicit executable resolution, version capture, environment-variable isolation, child-process inheritance review, cache/state separation, deterministic invocation, and evidence that bundled ADB/Git/runtime tools did not silently fall back to system installations.

- [ ] **Step 2: Define the command behavior gate**

  Before execution, require classification of credential access/recovery, reflection or private APIs, binary download/generation/execution, signing material, security-product interaction, and combined endpoint-security resemblance. Prefer supported client paths, controlled test credentials, signed manifests, hashes, or authorized isolated environments.

  Explicitly prohibit disabling endpoint security or adding exclusions merely to run the validation chain.

- [ ] **Step 3: Review against the two relevant RED outputs**

  Confirm the rules address system/bundled tool contamination and credential-plus-binary command chains. Ensure “read-only” is never used as a risk classification by itself.

- [ ] **Step 4: Run structural validation and commit the new Skill**

  ```powershell
  python C:/Users/wxb27/.codex/skills/.system/skill-creator/scripts/quick_validate.py silvite-architecture-evolution
  git add -- silvite-architecture-evolution
  git commit -m "feat: add architecture evolution skill"
  ```

### Task 6: Route the Existing Skill and Update Repository Documentation

**Files:**

- Modify: `SKILL.md`
- Modify: `README.md`
- Modify: `CHANGELOG.md`
- Modify: `SOURCES.md`
- Modify: `PUBLICATION_CHECKLIST.md`

**Interfaces:**

- Consumes: the validated new Skill and evaluation design.
- Produces: an explicit two-Skill public contract, corrected owner identity, installation instructions, release notes, and public-safety review.

- [ ] **Step 1: Add a minimal companion-Skill route**

  Add one concise section to the existing `SKILL.md`: for multi-stage underlying architecture evolution, additionally load `silvite-architecture-evolution`; keep general engineering governance in the root Skill.

- [ ] **Step 2: Rewrite README sections for the two-Skill model**

  Explain responsibilities, trigger examples, combined workflow, new folder structure, separate installation of each Skill, architecture-evolution evaluation coverage, and experimental limitations. Replace the clone URL with `https://github.com/LaoYinBai/Silvite-Engineering-Method.git`.

- [ ] **Step 3: Update release records**

  Add a `0.2.0` changelog entry describing the companion Skill, evaluation evidence, routing change, ownership normalization, and limitations. Update `SOURCES.md` to classify the supplied experience as generalized, declassified project feedback without retaining product-specific facts. Update `PUBLICATION_CHECKLIST.md` with every new directory and explicit SAFE/REVIEW NEEDED status.

- [ ] **Step 4: Scan repository-visible identity and private terms**

  Run searches for stale owner names, named private products/services, credential-like strings, private endpoints, and Windows-only paths inside runtime Skill Markdown. Resolve all public-content findings or record an explicit publication blocker.

- [ ] **Step 5: Validate and commit documentation**

  ```powershell
  python C:/Users/wxb27/.codex/skills/.system/skill-creator/scripts/quick_validate.py .
  git diff --check
  git add -- SKILL.md README.md CHANGELOG.md SOURCES.md PUBLICATION_CHECKLIST.md
  git commit -m "docs: publish two-skill engineering method"
  ```

### Task 7: GREEN Forward Evaluation and Refactoring

**Files:**

- Modify: `evals/architecture-evolution-results-v0.2.md`
- Modify if evidence requires: `silvite-architecture-evolution/SKILL.md`
- Modify if evidence requires: `silvite-architecture-evolution/references/*.md`

**Interfaces:**

- Consumes: exactly the Task 1 raw prompts and the new Skill artifact, without design conclusions or expected answers.
- Produces: independently observed GREEN behavior, residual gaps, and narrowly justified refinements.

- [ ] **Step 1: Run isolated GREEN agents**

  Give each agent one raw scenario and direct it to use `$silvite-architecture-evolution` at the repository path. Do not provide the evaluation rubric, expected response, design spec, baseline findings, or suspected loopholes.

- [ ] **Step 2: Manually score all outputs**

  Record decision, gates applied, evidence state, unsafe actions refused, remaining ambiguity, and pass/fail. Compare behavior rather than wording.

- [ ] **Step 3: Refactor only observed loopholes**

  If a GREEN agent finds a new rationalization, add the narrowest explicit counter in the correct core/reference file, then rerun that scenario. Do not add hypothetical rules unsupported by the supplied experience or evaluation.

- [ ] **Step 4: Commit verified evaluation results and refinements**

  ```powershell
  git add -- evals silvite-architecture-evolution SKILL.md
  git commit -m "test: validate architecture evolution behavior"
  ```

### Task 8: Final Validation and Push

**Files:**

- Verify: all tracked files and Git metadata.

**Interfaces:**

- Consumes: all prior commits.
- Produces: a clean, validated `main` pushed to `origin/main` with an exact evidence report.

- [ ] **Step 1: Run complete validation**

  Run both `quick_validate.py` checks, `git diff --check`, broken-relative-link inspection, `SKILL.md` line-count checks, placeholder scan, owner/private-term scan, YAML inspection, and `git fsck --full`.

- [ ] **Step 2: Review commit and diff scope**

  Inspect `git status`, commits since original HEAD `3856e104a010a9dfc46ab543d83d3546a6eb1725`, and the cumulative diff. Confirm no product code, credentials, generated caches, or unrelated files were added.

- [ ] **Step 3: Push and verify remote state**

  ```powershell
  git push origin main
  git ls-remote origin refs/heads/main
  git rev-parse HEAD
  ```

  Require the remote and local hashes to match before reporting `Remote Published` and `Remote Independently Verified` for the repository update.

- [ ] **Step 4: Report exact completion state**

  Report files and commits, RED/GREEN results, validation commands, remote hash, untested models/environments, residual method limitations, and the fact that published Git history before this work retains its original authors.
