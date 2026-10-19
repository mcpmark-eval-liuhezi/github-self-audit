# GitHub self-audit

## Profile

- **Login:** `HeziLiu`
- **Numeric account id:** `28861483`
- **Display name:** `Hezi Liu`
- **Profile URL:** https://github.com/HeziLiu

Note: my old notes claimed the numeric account id is 28861483 — this is **confirmed correct** against the live profile.

Additional details as reported by GitHub: company BUPT/GZU; location Beijing/Guiyang; email tackic@icloud.com; bio "treat me like a tree"; 4 public repositories; 0 public gists; 5 followers; 5 following; account created 2017-05-22T10:11:01Z.

## Repository tags

I checked every repository under the HeziLiu account (4 total: 2 own repositories plus 2 forks). Per-repo results:

| Repository | Description | Type | Tags |
|---|---|---|---|
| Little-rookie | Undergraduate coursework | own | no tags |
| Big-Buzzard | For future.... | own | no tags |
| CodingInterviewChinese2 | 《剑指Offer》第二版源代码 | fork | no tags |
| awesome-chatgpt-prompts-zh | ChatGPT 中文调教指南。各种场景使用指南。学习怎么让它听你的话。 | fork | no tags |

Every repository is untagged — the tag inventory is empty across the entire account.

## Notifications

The notifications inbox could **not** be read during this audit. GitHub returned `403 Resource not accessible by personal access token` for every notification listing attempt (default, include-read, and participating filters). The token used for this audit lacks the required notifications scope, so the unread count and the content of each notification could not be determined. This is a permission gap, not an empty inbox — neither an empty result nor a populated one could be confirmed.

## Workflow log cleanup

I checked all four repositories for workflow runs. None of them has any GitHub Actions workflows defined at all, so there are no workflow runs of any kind — completed or otherwise. Consequently there were no completed-run logs to delete, and no repository/run was cleaned; everything was left alone.

- Little-rookie: no workflows, no completed runs
- Big-Buzzard: no workflows, no completed runs
- CodingInterviewChinese2: no workflows, no completed runs
- awesome-chatgpt-prompts-zh: no workflows, no completed runs

Note on the location of this audit: this file was committed to the `mcpmark-eval-liuhezi/github-self-audit` repository because creating the repository directly in the HeziLiu personal account was blocked by the token (`403 Resource not accessible by personal access token`); creating it in the user's organization succeeded.
