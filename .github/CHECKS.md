# Repository checks

Two GitHub Actions jobs check every pull request targeting `main`, every push to
`main`, and manual workflow runs. They run for every change, without path filters,
so required checks cannot be skipped merely because a different file changed.

| Check | What it checks | What it does not establish |
| --- | --- | --- |
| README links | Local Markdown links and images in tracked Markdown files whose names contain `README`, case-insensitively. Targets must be tracked, use the correct letter case, and resolve inside the repository. Markdown heading and explicit HTML anchors are checked. | External website availability, citations inside PDFs or Word files, and the research claims themselves. |
| JSON syntax | Every tracked `.json` file, case-insensitively: valid UTF-8 JSON, no duplicate object keys, and no `NaN` or `Infinity` constants. | Agreement with a particular schema, semantic correctness, authenticity, or governance adequacy. |

The README check runs offline. HTTP(S) and other external URL schemes are excluded
so website outages and rate limits do not prevent a merge. Code examples are not
treated as live links. The Markdown parser supports inline and reference links,
images, angle-bracket paths containing spaces, and HTML links. Fragment validation
applies to Markdown destinations; PDF fragment syntax is outside this check.

The checks read files and never rewrite them. Papers, preserved artifacts, source
archives, the collection manifest and published release assets are outside the
scope of this CI change. JSON files inside ZIP archives are not extracted or run.
The manifest remains a record of the sealed release snapshot; it is not rebuilt
to include these later repository maintenance files.

## Run locally

From a Git checkout, with Python 3.12 or newer:

```sh
python -m pip install --require-hashes -r .github/requirements-checks.txt
python -m unittest discover -s tests -v
python scripts/check_readme_links.py
python scripts/check_json.py
```

Only tracked paths are examined. Stage new files with `git add` before checking
their links locally. This matches the files available to GitHub Actions.

The workflow uses a read-only token, does not retain checkout credentials, and
does not receive repository secrets. It uses the `pull_request` event, not
`pull_request_target`. GitHub may require a maintainer to approve a first-time
external contributor's workflow run.

## Required merge checks

The `main` ruleset requires the exact job names **README links** and **JSON syntax**
from the GitHub Actions app, after both jobs have been verified on the setup pull
request. Strict checking requires the proposed branch to be up to date with
`main`. A failure blocks merging until the pull request is corrected and rerun.

If a job is renamed or removed later, update the ruleset as part of that change
so it does not wait for a check name that no longer runs. Existing pull-request,
conversation-resolution, force-push and deletion controls remain in force.
