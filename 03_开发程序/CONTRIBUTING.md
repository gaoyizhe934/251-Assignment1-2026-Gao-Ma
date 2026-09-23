# GitHub Collaboration and Code Commenting Rules

This policy applies only to this repository. GitHub evidence must reflect real work. Do not create empty commits, meaningless formatting changes, or fabricated Issues, reviews, and test results merely to increase visible activity.

## 1. Repository language policy

All human-readable repository content and GitHub collaboration text must be written in English. This includes source-code comments, Javadoc, README files, documentation, configuration descriptions, Issue and pull-request titles and bodies, review comments, test names, UI messages, and workflow descriptions. Use clear New Zealand English where a regional spelling choice is needed.

## 2. Commit rules

1. Create a GitHub Issue before beginning a feature, defect fix, quality task, or build task. The Issue must state the context, acceptance criteria, owner, and affected module. Apply an appropriate `feature`, `bug`, `test`, `quality`, `ci`, or `docs` label.
2. Create a short-lived branch from `main` for each task. Branch names use `type/Chinese-summary`; for example, `feat/<feature-summary>`, `fix/<bug-summary>`, or `test/<test-summary>`.
3. Each commit must contain one small, complete, reviewable task. Do not combine features, refactoring, dependency changes, and unrelated formatting changes in one commit.
4. Commit subjects must use a Chinese summary and one of these prefixes only:

   - `feat:` for a new user-visible feature
   - `fix:` for a defect or error-handling fix
   - `docs:` for README, usage, or design documentation
   - `test:` for test additions or changes
   - `refactor:` for behaviour-preserving restructuring
   - `chore:` for build, CI, dependency, tool, or configuration work

   Format examples: `feat: <feature-summary>`, `test: <test-summary>`, and `fix: <bug-summary>`.

5. When needed, the commit body records the linked Issue, scope, validation command, and result. For example:

   ```text
   feat: <feature-summary>

   Linked issue: #12
   Validation: mvn test -Dtest=SearchServiceTest
   ```

6. Each member pushes soon after completing genuine work and maintains near-daily Git activity during development. Run the relevant tests before committing; run `mvn test` or the relevant Maven goal when changing build, dependency, or quality tooling.

## 3. Branch, Issue, and pull-request workflow

1. `main` contains only verified, buildable code. Do not develop directly on `main`.
2. Create a pull request when a branch is ready. Use the same prefix style as the commits and link its Issue, for example `Closes #12`.
3. The PR description must include a change summary, acceptance method, and result. GUI work needs a screenshot or reproducible interaction notes; build and quality work needs the relevant report, command output, or CI link.
4. The other member reviews every PR and leaves a genuine approval or actionable change request. Address feedback before merging.
5. Before merging, confirm that relevant tests and CI pass, no review comments remain unresolved, and the Issue acceptance criteria are met. Close the Issue after the PR is merged.
6. Use a normal merge commit or squash merge and retain the PR-to-Issue relationship. Do not rewrite shared, pushed branch history.

## 4. Required GitHub evidence

Maintain these records throughout development:

| Record | Minimum requirement | Evidence to retain |
| --- | --- | --- |
| Private repository | Keep the repository private from the start until marking is complete | Correct repository name, both members as collaborators, and marker access when requested |
| Commit history | Both members make genuine, traceable commits | Prefix, description, author, timestamp, and focused module scope |
| Branches and merges | Complete features on branches before merging | Branch name, PR, merge commit, and conflict-resolution record when applicable |
| GitHub Issues | Track every feature, defect, quality, and CI task | Description, owner, label, acceptance criteria, closed state, and linked PR |
| Pull requests and reviews | Create a PR for every merged feature branch | Change summary, validation evidence, peer review, and merge record |
| GitHub Actions | Run Maven validation on pushes and PRs | Workflow YAML, run history, and any necessary fix commit |
| Quality reports | Generate reviewable reports at each milestone | Files in `reports/metrics`, `reports/spotbugs`, and `reports/pmd`, plus their generation commits |
| README | Complete it before final submission | Both members' names and IDs, run instructions, directory explanation, Docker instructions, private repository link, and representative commit SHAs for both members |

The evidence must form a real lifecycle: `Issue -> branch -> commit -> PR/review -> CI -> merge -> close Issue`.

## 5. Java code-commenting rules

1. Add concise Javadoc to every public class, interface, enum, and public method. Describe responsibility, inputs and outputs, state changes, and meaningful exceptions.
2. Comment on *why* a non-obvious decision exists, such as the UTF-8 save policy, ODT-read fallback, search-offset calculation, or multi-window close order. Do not restate what clear code already says.
3. Explain failure handling for file I/O, PDF export, printing, YAML parsing, and external libraries. A caught exception must be recovered from, reported, or rethrown; never swallow it silently.
4. Keep a short explanation beside complex regular expressions, syntax-highlighting rules, pagination calculations, and cross-window state synchronisation. Extract reusable logic into clearly named methods or constants.
5. Every `TODO` includes the next action and its Issue, for example: `// TODO(#18): Show a recoverable error message when ODT parsing fails.` Remove it when complete and update or close the Issue.
6. Do not leave stale, vague, or line-by-line translation comments. Update Javadoc, README files, and configuration documentation when behaviour changes.

## 6. Pre-commit checklist

- The related Issue exists or is linked, and the change contains only files required for the task.
- The code follows the Java 17, Maven, and YAML conventions. Do not commit local JAR files, `target/`, or IDE files.
- New behaviour has focused JUnit coverage, with test names that describe scenario and expected outcome.
- Relevant Maven commands have been run and recorded. UI, format-reading, PDF, and print work has reproducible manual verification notes.
- Comments and Javadoc explain responsibilities, boundaries, and error handling; no obsolete TODO remains.
- The branch is pushed, its PR links the Issue, and peer review is requested or complete.
