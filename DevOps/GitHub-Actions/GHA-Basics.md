# GitHub Actions (GHA)

GitHub Actions is a CI/CD and automation platform provided by GitHub to automate workflows like building, testing, linting, and deploying code.

## Components of GHA

### Workflow

A workflow is a YAML file stored in `.github/workflows/` that defines automation.

It contains:

- Triggers (events)
- Jobs
- Steps

> **Note**: `workflow_dispatch` allows us to manually trigger a workflow from GitHub UI or API. For example: `on: workflow_dispatch`.

### Events/Triggers

Events define when a workflow runs.

Common events:

- `push`
- `pull_request`
- `issue`
- `workflow_dispatch`
- `schedule` (cron)
- `release`

Example:

```yaml
on:
  push:
    branches: [ main ]
```

### Runners

A runner is the machine that executes the workflow.

GitHub provides hosted runners or we can define our own custom runners. 

There are two types of runners:

#### GitHub-hosted

- Managed by GitHub
- Fresh VM for every job
- Examples:
  - `ubuntu-latest`
  - `windows-latest`
  - `macos-latest`

#### Self-hosted

- Own server/VM
- Useful for:
  - Custom software
  - Private network
  - Heavy workloads

Example:

```yaml
runs-on: ubuntu-latest
```

### Jobs

A job is a group of steps that run on the same runner.

- Jobs run in parallel by default.
- Can be sequenced using `needs`.

Example:

```yaml
jobs:
  build:
    runs-on: ubuntu-latest
```

Sequential jobs:

```yaml
jobs:
  test:
    needs: build
```

### Steps

A step is a single task inside a job. There are two types of steps:

- `run`: It executes shell command(s).
- `uses`: It uses an action.

> **Note**: A shell type can be defined for a step.

Example:

```yaml
- name: Install dependencies
  run: npm install
  shell: bash
```

#### Do we need to specify the shell for a step?

No (most of the time). GHA automatically chooses a default shell based on the runner:

| Runner         | Default shell       |
| -------------- | ------------------- |
| ubuntu / macOS | `bash`              |
| windows        | `pwsh` (PowerShell) |

We should explicitly specify `shell` in cases like:
- When we want a different shell.
- If the workflow runs on multiple OS and we want cross-platform consistency.

> **Rule of thumb**: Do not specify shell unless there is a reason.

### Actions

An action is a reusable unit of code that performs a task. Tje sources of actions are:

- GitHub Marketplace
- Custom actions

Examples of popular actions:

```yaml
uses: actions/checkout@v4
uses: actions/setup-node@v4
uses: docker/build-push-action@v5
```

> **Note**:
> - Actions are reusable.
> - GitHub provides `ubuntu`, `windows`, `macOS` runners by default.
> - Jobs run in parallel unless linked with `needs`.

## GitHub `event` variable

The `github.event` contains the full event payload that triggered the workflow.

Example:

```yaml
${{ github.event }}
```

Some useful fields are:

```yaml
${{ github.event_name }}      # push, pull_request
${{ github.actor }}           # user who triggered
${{ github.event.repository.name }}
${{ github.event.issue.number }}
```

Example usage:

```yaml
- run: echo "Triggered by ${{ github.actor }}"
```

## Mental Model

```
Event → Workflow → Jobs → Steps → Actions (run on Runners)
```

## `jq` in GHA

`jq` is a JSON processor used to parse GitHub event data.

### Why and when to use `jq`?

`jq` is used when we need to read or extract values from JSON inside workflows.

GitHub provides lots of data as JSON, especially:
- `github.event`
- API responses
- Tool outputs

### Use of `toJson` with `jq`

`toJson` is a GitHub Actions expression function used to convert an object into a JSON string. 

As `${{ github.event }}` is an object, so shell cannot directly process it. So we use `toJson` to parse the object into a JSON String.

### When do we actually need `jq`?

- When we want to specific fields from event payload.
- When we want*conditional logic based on JSON
- When we want to call GitHub API and parse response

### Example 1: Get PR title

```yaml
- run: |
    echo '${{ toJson(github.event) }}' | jq '.pull_request.title'
```

#### Example 2: Use commit message

```yaml
- run: |
    MSG=$(echo '${{ toJson(github.event) }}' | jq -r '.head_commit.message')
    echo "Commit message: $MSG"
```

> **Note**: `-r` in `jq` means "raw output".
> - Without `-r`, the variable is: `"Fix login bug"`.
> - With `-r`, the variable is: `Fix login bug`.

#### Example 3: Conditional logic

Run step only if PR is to `main`:

```yaml
- run: |
    BASE=$(echo '${{ toJson(github.event) }}' | jq -r '.pull_request.base.ref')
    if [ "$BASE" = "main" ]; then
      echo "Target is main"
    fi
```

## Secrets in GHA

Secrets are encrypted environment variables used to store sensitive data like:

- API keys
- Tokens
- Passwords
- SSH keys

They are managed in:

```
Repository → Settings → Secrets and variables → Actions
```

Used in workflows as:

```yaml
${{ secrets.MY_SECRET }}
```

Example:

```yaml
- run: echo "Token is ${{ secrets.API_KEY }}"
```

> **Important**:
> - Secrets are masked in logs.
> - They cannot be printed in plain text.
> - They are not accessible in PRs from forks (by default).

### `secrets.GITHUB_TOKEN`

It is a temporary, auto-generated access token that GitHub creates for every single workflow run. It represents a GitHub App identity for our workflow.

It is needed because the workflows need permission to talk to GitHub.

> **Note**: It is:
> - Not us.
> - Not our account.
> - But a bot user acting on behalf of the repository.

It can be used for:

- Commenting on issues/PRs
- Creating releases
- Pushing commits
- Calling GitHub API

Example:

```yaml
env:
  GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

Its permissions depend on repo settings:

```yaml
permissions:
  issues: write
  contents: read
```

> Think of `GITHUB_TOKEN` as a temporary bot account for the workflow.

## GH CLI

`gh` is the official command-line tool to interact with GitHub. It internally calls GitHub APIs.

It can be used for:

- Creating issues/PRs
- Commenting
- Managing releases
- Calling GitHub API

It is available by default on GitHub-hosted runners.

### Example: Add a comment to a new issue

Trigger on issue creation:

```yaml
on:
  issues:
    types: [opened]
```

Step(s):

```yaml
- run: |
    gh issue comment ${{ github.event.issue.number }} \
      --body "Thanks for opening this issue!"
  env:
    GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

## GitHub APIs

GitHub provides REST and GraphQL APIs to programmatically interact with GitHub.

They allow us to:

- Create / update issues and PRs
- Manage repositories
- Trigger workflows
- Read commits, users, releases
- Build custom bots & tools

The base URLs for the APIs are:

- REST: `https://api.github.com`
- GraphQL: `https://api.github.com/graphql`

### Authentication

All API calls require authentication using a token:

- `GITHUB_TOKEN` (inside workflows)
- Personal Access Token or PAT (outside GitHub)

Example using `curl` in GHA:

```yaml
- run: |
    curl -H "Authorization: Bearer ${{ secrets.GITHUB_TOKEN }}" \
         https://api.github.com/repos/${{ github.repository }}/issues
```

> **Note**: `-H` means Header.

### Example: Create an issue via API

```yaml
- run: |
    curl -X POST \
      -H "Authorization: Bearer ${{ secrets.GITHUB_TOKEN }}" \
      -H "Accept: application/vnd.github+json" \
      https://api.github.com/repos/${{ github.repository }}/issues \
      -d '{"title":"Bug found","body":"Details here"}'
```

> **Note**: `-X` means HTTP method.

### REST vs GraphQL

| REST               | GraphQL               |
| ------------------ | --------------------- |
| Multiple endpoints | Single endpoint       |
| Fixed responses    | Custom responses      |
| Simpler            | More powerful         |
| Easier to learn    | Better for large apps |

### When to use GitHub APIs directly?

- Building external services
- Writing custom bots
- Integrating with non-GitHub systems
- In need of fine-grained control

### Relationship

```
GitHub API  ← core engine
GH CLI      ← human-friendly wrapper
GHA         ← automation platform using both
```

## Why use GH CLI instead of API?

| GH CLI           | GitHub API     |
| ---------------- | -------------- |
| Simple commands  | Raw HTTP calls |
| Auth handled     | Manual tokens  |
| Less boilerplate | More control   |

> GH CLI is perfect for automation scripts inside workflows. API is better for custom tools or external services.

### Real-world usage pattern

Most real projects use:

- `secrets.GITHUB_TOKEN`: internal GitHub tasks
- Custom secrets: AWS, DockerHub, Slack
- `gh`: comments, labels, releases, bots

## Environments in workflow

- Staging
- Dev
- 
