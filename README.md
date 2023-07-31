
# GitHub Activity in Readme


Updates `README.md` with the recent GitHub activity of a user.

<img width="735" alt="profile-repo" src="https://user-images.githubusercontent.com/25279263/87703301-3aa4a500-c7b8-11ea-8eb6-245121997a7b.png">

---

## Instructions

<!--START_SECTION:activity-->
1. 🚀 Published release [v0.4.1](https://github.com/jamesgeorge007/github-activity-readme/releases/tag/v0.4.1) in [jamesgeorge007/github-activity-readme](https://github.com/jamesgeorge007/github-activity-readme)
2. 🎉 Merged PR [#104](https://github.com/jamesgeorge007/github-activity-readme/pull/104) in [jamesgeorge007/github-activity-readme](https://github.com/jamesgeorge007/github-activity-readme)
3. 🔒 Closed issue [#99](https://github.com/jamesgeorge007/github-activity-readme/issues/99) in [jamesgeorge007/github-activity-readme](https://github.com/jamesgeorge007/github-activity-readme)
4. 🗣 Commented on [#102](https://github.com/jamesgeorge007/github-activity-readme/pull/102#issuecomment-1627773520) in [jamesgeorge007/github-activity-readme](https://github.com/jamesgeorge007/github-activity-readme)
5. 🔒 Closed issue [#96](https://github.com/jamesgeorge007/github-activity-readme/issues/96) in [jamesgeorge007/github-activity-readme](https://github.com/jamesgeorge007/github-activity-readme)
<!--END_SECTION:activity-->

- Add the comment `<!--START_SECTION:activity-->` (entry point) within `README.md`. You can find an example [here](https://github.com/jamesgeorge007/jamesgeorge007/blob/master/README.md).

- It's the time to create a workflow file.

`.github/workflows/update-readme.yml`

```yml
name: Update README
on:
  schedule:
    - cron: "*/30 * * * *"
  workflow_dispatch:
jobs:
  build:
    name: Update this repo's README with recent activity
    runs-on: ubuntu-latest
    permissions:
      contents: write

    steps:
      - uses: actions/checkout@v3
      - uses: jamesgeorge007/github-activity-readme@master
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

The above job runs every half an hour, you can change it as you wish based on the [cron syntax](https://jasonet.co/posts/scheduled-actions/#the-cron-syntax).

Please note that only those public events that belong to the following list show up:-

- `IssueEvent`
- `ReleaseEvent`
- `IssueCommentEvent`
- `PullRequestEvent`

You can find an example [here](https://github.com/jamesgeorge007/jamesgeorge007/blob/master/.github/workflows/update-readme.yml).

### Override defaults

Use the following `input params` to customize it for your use case:-

| Input Param    | Default Value                                         | Description                                               |
| -------------- | ----------------------------------------------------- | --------------------------------------------------------- |
| `COMMIT_NAME`  | github-actions[bot]                                   | Name of the committer                                     |
| `COMMIT_EMAIL` | 41898282+github-actions[bot]@users.noreply.github.com | Email of the committer                                    |
| `COMMIT_MSG`   | :zap: Update README with the recent activity          | Commit message used while committing to the repo          |
| `MAX_LINES`    | 5                                                     | The maximum number of lines populated in your readme file |
| `TARGET_FILE`  | README.md                                             | The file to insert recent activity into                   |

```yml
name: Update README
on:
  schedule:
    - cron: "*/30 * * * *"
  workflow_dispatch:
jobs:
  build:
    name: Update this repo's README with recent activity
    runs-on: ubuntu-latest
    permissions:
      contents: write

    steps:
      - uses: actions/checkout@v3
      - uses: jamesgeorge007/github-activity-readme@master
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        with:
          COMMIT_MSG: "Specify a custom commit message"
          MAX_LINES: 10
          COMMIT_NAME: GitHub Activity Readme
```

_Inspired by [JasonEtco/activity-box](https://github.com/JasonEtco/activity-box)_
