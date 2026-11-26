---
name: release-notes
description: Writes release notes from the merged Pull Requests
---

# Release notes

You write the release notes for one version. A release tells people what changed, so write for the reader, not for the author of the code.

## Input

For every PR merged since the last release:

1. **Title**
2. **Description**
3. **Diff**: lines starting with `-` were removed, lines starting with `+` were added.

You also get the **version** (for example `v1.0`).

Only merged PRs count. Ignore PRs that were closed or are still open.

## Who reads the notes

**Users of the project**, not the programmers who wrote it. They want to know what is different when they use it now. They do not care how it was built.

- Write in plain words. No file names, function internals, or branch names.
- Describe the behavior, not the code. Write "Passwords shorter than 10 characters are now rejected", not "changed `len(pw) > 10` to `len(pw) >= 10`".

## Sections

Use only these three sections, in this order:

1. **Added**: new things users can do.
2. **Fixed**: something was wrong and now works correctly.
3. **Changed**: something works differently on purpose.

Rules:

- Leave out a section that has no entries. Never write "Nothing" or an empty heading.
- Put each PR in exactly one section.
- If a PR does two things, write two lines.

## What one line looks like

```
- <Verb> <what is different for the user> (#<PR number>)
```

- One line per change, at most about 15 words.
- Start with a verb: "Rejects", "Counts", "Adds", "Fixes".
- Say what the behavior is now, not what the code did.
- End with the PR number.

Good: `- Counts uppercase vowels as well as lowercase (#3)`
Bad: `- Fixed bug in vowels.py` (no file names, and it does not say what changed for the user)
Bad: `- Updated check_password function` (says nothing about the behavior)

**Trust the diff over the description.** If the PR description says one thing and the diff does something else, write what the diff does.

## What is left out

Do not mention:

- changes to tests only
- refactors, renames, and formatting with no change in behavior
- debug prints, comments, and typo fixes in docs
- merge commits and "update README" PRs
- anything secret: tokens, passwords, keys (if a PR touched one, leave it out of the notes completely)
- PRs whose diff has no effect the user can see

If every PR is left out, write the title line and `No user-facing changes.`

## Output format

Output only the notes, in Markdown, ready to paste into `CHANGELOG.md`. No greeting, no explanation.

```
## <version>

### Added
- ...

### Fixed
- ...

### Changed
- ...
```

### Example

Version: `v1.0`

Merged PRs:
- #1 "Fix password length": diff changes `len(pw) > 10` to `len(pw) >= 10`
- #2 "Add email check": new function `is_valid_email`, requires `@` and `.`
- #3 "Add tests for vowels": only `test_vowels.py` changed

Output:

```
## v1.0

### Added
- Adds email validation that requires an @ and a dot (#2)

### Fixed
- Accepts passwords of exactly 10 characters (#1)
```

(PR #3 is left out because it only changed tests.)
