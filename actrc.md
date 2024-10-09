# Act usage examples

## Online resources

- [Act repository](https://github.com/nektos/act)
- [Act usage guide](https://nektosact.com/usage/index.html)
- [How to Run GitHub Actions Locally Using the act CLI Tool](https://www.freecodecamp.org/news/how-to-run-github-actions-locally/)
- [A guide to using act with GitHub Actions](https://blog.logrocket.com/guide-using-act-github-actions/)

## Example commands

### Welcome

Running a full workflow

```bash
act -W act -W .github/workflows/hello.yaml
```

### Basic commands

List all available workflows and its jobs

```bash
act -l
```

List jobs for specific workflow

```bash
act -l -W .github/workflows/hello.yaml
```

Run single job

```
act -W .github/workflows/hello.yaml -j welcome
```

### Events

[Events that trigger workflows](https://docs.github.com/en/actions/writing-workflows/choosing-when-your-workflow-runs/events-that-trigger-workflows)

**push** - default event used

```bash
act -W .github/workflows/events.yaml
```

**push** with defined event data

```bash
act -W .github/workflows/events.yaml -e events/push.json
```

**pull_request**

```bash
act pull_request -W .github/workflows/events.yaml
```

**pull_request** with defined event data

Opened PR

```bash
act pull_request -W .github/workflows/events.yaml -e events/pull_request.opened.json
```

Labeled PR

```bash
act pull_request -W .github/workflows/events.yaml -e events/pull_request.labeled.json
```

**sheduled**

```bash
act scheduled -W .github/workflows/events.yaml
```

### Workflow with cache

First run without cache server

```bash
act -W .github/workflows/cache.yaml
```

#### Install Cache server

Installation: [github-act-cache-server](https://github.com/sp-ricard-valverde/github-act-cache-server)

Environment variables used in the `.actrc`

```
--env ACTIONS_CACHE_URL=http://127.0.0.1:8080/
--env ACTIONS_RUNTIME_URL=http://127.0.0.1:8080/
--env ACTIONS_RUNTIME_TOKEN=foo
```

### Skip Job when using the Act

```bash
act -W .github/workflows/skip-job.yaml -e events/push.json
```

add `"act": true` into `events/push.json and re-run

### Using local code for the shared action

Replace `actions/setup-node` with the local mock

```bash
act -W .github/workflows/cache.yaml --local-repository https://github.com/actions/setup-node@v4=./fake-setup-node
```
