# NOTES: GitHub profile hygiene

This is the record of the profile clean-up: what changed on the GitHub account, how it was checked, and what is still open.
Private repositories are redacted to a count.

## 2026-10-29

### Added

- `README.md`: profile README with a one-line role, three bullets, the public portfolio repos with their CI badges, and contact links (958129e).
- `README_TEMPLATE.md`: the shared README shape for the portfolio repos, with a pre-publication checklist in a comment at the top (c5ffa37).
- `NOTES.md`: this file.

### Changed

- This repo's description is now "Profile README and the shared README template for my robotics portfolio repos.".
- This repo's topics: added `portfolio` and `robotics`, removed `config` and `github-config`.
- `README.md` replaces GitHub's 2022 default profile README.
- `Home-servie-robot` (Udacity Robotics Software Engineer Nanodegree, project 5) got a one-line banner commit, then was archived:
  - Banner commit 64494e2: "Archived Udacity Robotics Software Engineer Nanodegree coursework (project 5); kept for the record."
  - The repo stays public and read-only. It was not renamed, hidden or deleted.

### Not changed

- `ur5e-teaching-controllers`, `pointcloud-constrained-planning` and `a private repo`:
  - Each already had a description and six topics from the vocabulary, so none of them was edited here.
  - Each will adopt `README_TEMPLATE.md` at its own final checkpoint.
- 3 private repos, unchanged.
- Nothing else changed:
  - No repo deleted, no visibility change, and no forks exist.
  - Nothing starred, followed or watched.
  - Pinned repos and profile fields were not changed.
  - No GitHub Action was added.

## Inventory (2026-10-29)

Command: `gh repo list giridhar-shenoy --limit 200 --json name,description,isArchived,isPrivate,isFork,pushedAt,stargazerCount,repositoryTopics,url`.

| Repo | Visibility | Before | Action | After |
|---|---|---|---|---|
| giridhar-shenoy | public | default README, GitHub's default description, topics `config`, `github-config` | KEEP + DESCRIBE | new README and template, description set, topics `portfolio`, `robotics` |
| Home-servie-robot | public | coursework, last push 2022-02-10, no topics | ARCHIVE | banner commit, archived |
| ur5e-teaching-controllers | public | description, 6 vocabulary topics | KEEP | unchanged |
| pointcloud-constrained-planning | public | description, 6 vocabulary topics | KEEP | unchanged |
| a private repo | public | description, 6 vocabulary topics | KEEP | unchanged |
| sim-demo-to-policy | public | created 2026-10-28 21:10 UTC by its own build session; empty (no commits), description set, no topics | none here: its topics are chosen in that repo's own setup step | unchanged, not listed in the README while it is empty |
| 3 private repos | private | — | none | unchanged |

There are no forks, so there were no DELETE-FORK rows.

## Verification (2026-10-29, after the push)

| Check | Result | Command |
|---|---|---|
| Home-servie-robot is archived | `isArchived: true`, still public | `gh repo view giridhar-shenoy/Home-servie-robot --json isArchived,visibility` |
| Every public, non-archived repo has a description and at least 2 vocabulary topics | yes for 4 of 5. `sim-demo-to-policy` has no topics yet (open question 6) | `gh repo list giridhar-shenoy --json name,visibility,isArchived,description,repositoryTopics` |
| Profile README renders | the profile page shows the new role line | `curl -s https://github.com/giridhar-shenoy \| grep -c 'moving into learning-based manipulation'` |
| Rendered README has 8 links, 3 CI badges | 3 repos, 3 CI workflow pages, mailto, LinkedIn | `gh api markdown -f mode=gfm -F text=@README.md` |
| Every link resolves | 9 GitHub URLs return 200. LinkedIn returns 999, its bot block, so it can only be checked in a browser | `curl -s -o /dev/null -L -w '%{http_code}' <url>` |
| No force-pushes | 0 on both touched repos | `gh api "repos/giridhar-shenoy/<repo>/activity?activity_type=force_push" --jq length` |
| New commits are dated today, conventional, and use the right author | 3 `docs:` commits, 2026-10-29 IST (2026-10-28 ~21:10 UTC), giridharjshenoy@gmail.com; no amended or rebased commits | `gh api "repos/giridhar-shenoy/<repo>/commits" --jq '.[] \| [.sha[0:7], .commit.author.date, .commit.author.email, .commit.message]'` |

## Open questions

1. **Pins.** The planned six pins are R1–R5 plus an upstream-PR fork or this repo. R4, R5 and the fork don't exist yet, so only four pins are possible now: the three portfolio repos and this repo. Pins are set by hand on the profile page.
2. **Profile fields.** The account's name, bio and location are empty, so the profile shows only the handle. The proposed text is kept off this public repo. Apply it by hand, or refresh the gh token with the `user` scope.
3. **Weekly list refresh.** The portfolio list is hand-written until the site and its `data/repos.json` exist. When they do, should the refresh Action commit directly as `github-actions[bot]` or open a PR?
4. **`portfolio` topic.** Add it to each portfolio repo at that repo's final checkpoint, together with the template?
5. **LinkedIn link.** Check it once in a browser; automated checks can't reach it.
6. **`sim-demo-to-policy`.** It went public while empty. Its topics come from that repo's setup step: proposed `robotics`, `manipulation`, `mujoco`, `lerobot`, `imitation-learning`. Its line in the README is added once it has a README and a green CI run.
