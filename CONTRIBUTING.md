# Contributing to Access PoD v1.0

Access PoD v1.0 is a Public Review Draft for governance tech research, supporting
artifacts and Access-Mode. Contributions can improve clarity, navigation,
reproducibility and the interpretation of examples. Identify the component,
document or file, version and reason for each proposed change.

The working repository can develop after publication. The
[v1.0-consolidated release](https://github.com/Access-PoD/access-pod-v1.0/releases/tag/v1.0-consolidated)
remains the published edition. Merging into `main` does not rebuild, reseal or
publish a release.

## Normal change workflow

1. **Start from the latest `main` and create a branch.** Use a focused name such
   as `docs/clarify-id2-guide`. Contributors without repository write access can
   fork the repository and create the branch in their fork. Work in a repository
   checkout; keep the sealed package and its preparation folder separate.
2. **Make a focused change.** Keep original papers and artifacts intact. Explain
   corrections through errata, current guidance or clearly versioned additions.
   Preserve attribution and applicable licence notices. Commit and push the
   changes to your branch.
3. **Open a pull request targeting `main`.** Describe the problem, the resulting
   change, files affected and validation performed. State whether it is current
   repository guidance or material proposed for a future edition. Use a draft
   pull request while work is unfinished, then mark it ready for review.
4. **Wait for both required checks.** Read failures in the pull request's
   **Checks** tab, correct the problem and push another commit to the same branch.
   The pull request updates and the checks rerun automatically. A failed check
   must be addressed before merging.
5. **Review the complete diff.** Use **Files changed** to confirm the scope,
   accuracy, links, licence notices and preservation of original material.
   Address and resolve review conversations. If `main` has advanced, update the
   branch, resolve any conflicts and wait for the checks to pass again.
6. **Merge when ready.** A maintainer merges after the checks and review are
   complete. For a small, focused change, **Squash and merge** gives one commit
   describing the completed change. Delete the finished working branch if it is
   no longer needed, then update your local `main`. Checks also run on `main`
   after the merge.

## Required checks and merge rules

| Required check | Scope |
| --- | --- |
| **README links** | Checks local links and images in tracked Markdown files whose names contain `README`, ignoring letter case. Checks tracked destinations, filename case, repository boundaries and Markdown heading or explicit HTML anchors. |
| **JSON syntax** | Checks every tracked `.json` file, ignoring extension case, for valid UTF-8 JSON, unique object keys and the absence of non-JSON `NaN` or `Infinity` literals. UTF-8 byte-order marks are rejected. |

Both jobs run on every pull request to `main`, including documentation-only
changes. The active rules require passing results from GitHub Actions, an
up-to-date branch and resolved review conversations. There are no configured
bypass actors. A second-person approval is not currently required, so a
maintainer can merge their own pull request once the other conditions are met.
Direct changes to `main` must go through a pull request; force pushes and branch
deletion are blocked.

These checks read files without rewriting them or executing the artifact
workflows. The README check is offline: external website availability and links
in other documents, including this guide, need separate review. JSON checking
does not extract ZIP archives, validate schemas, verify provenance or establish
research validity, governance adequacy or production readiness. Passing CI does
not by itself prove that original papers or sealed material were preserved.

See the [repository checks documentation](.github/CHECKS.md) for local commands
and implementation details. Local checking is optional before pushing; GitHub's
required checks must still pass. Stage intended new files before local checks,
because only Git-tracked paths are examined. GitHub may require maintainer
approval before running checks for a first-time external contributor.

If changing a required job's name or removing it, coordinate the workflow and
ruleset changes so pull requests are not left waiting for a check that no longer
runs.

## Preserve the sealed release

- Keep the `v1.0-consolidated` tag at its published commit. Its current protection
  blocks movement and deletion. Keep the release published as a pre-release
  while it remains the Public Review Draft.
- Do not replace, delete or regenerate the existing `access-pod-v1.0.zip`,
  `SHA256SUMS.txt` or `SEAL_RECEIPT.json` assets. Keep their recorded hashes and
  the sealed preparation files unchanged. Tag protection does not make uploaded
  assets immutable; this release currently has GitHub release immutability off.
- Retain original papers, artifact records, source archives and provenance.
  Identify the source version and date when adding revised or supplementary
  material so readers can distinguish it from the published originals.
- Keep [collection-manifest.json](collection-manifest.json) as the record of
  the sealed snapshot. Do not refresh it to include later repository guidance,
  contribution instructions or CI files.
- The existing supplementary reader and reviewer PDF is outside the sealed ZIP.
  Keep that published asset unchanged too; propose future supplements separately
  and label their status and relationship to the sealed edition.
- Prepare a future consolidated edition through a separate review and release
  process, using a new tag, versioned package, checksums and seal receipt. Extend
  published-tag protection to cover each newly published tag. A routine merge
  into `main` is not authority to replace the existing release assets.

For each pull request, verify that its diff contains only the intended changes
and that it does not overwrite preserved material. For publication work, also
compare the existing release tag, asset identities and hashes before and after.

## Scope and licences

Follow the [licensing scope and source notices](LICENSING.md), retain attribution
and respect the terms of separately linked releases. This contribution guide
does not change any licence or bring related external releases into this
collection. The [main README](README.md) maps the papers, artifacts and related
releases.
