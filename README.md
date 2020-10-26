## Can you read the commit message?

From a push event, yes.

https://docs.github.com/en/free-pro-team@latest/actions/reference/context-and-expression-syntax-for-github-actions#github-context

https://docs.github.com/en/free-pro-team@latest/developers/webhooks-and-events/webhook-events-and-payloads#push

## What can you see in a `workflow_run` event?

You can see it here:

- https://github.com/mattwynne/github-actions-faq/actions/runs/326443410
- https://github.com/mattwynne/github-actions-faq/actions/runs/326443276

## Can you find out the result of the workflow in a workflow_run event?

Yes, use `github.event.workflow_run.conclusion`

e.g. https://github.com/mattwynne/github-actions-faq/blob/52693bf0cc52c7decd70c58c8e49703915998f89/.github/workflows/post-ci.yml#L10

## Does a job run even if ealier jobs failed?

[Yes](https://github.com/mattwynne/github-actions-faq/runs/1308812856?check_suite_focus=true)

## How do I only run a job if ealier jobs failed?

Use the [`needs` context](https://docs.github.com/en/free-pro-team@latest/actions/reference/context-and-expression-syntax-for-github-actions#needs-context):

```yaml
jobs:
  build: ...
  after-build:
    runs-on: ubuntu-latest
    needs: build
    if: needs.build.result == 'success'
```

## Can you use a multi-line `if` conditional?

e.g.

```yaml
publish-image:
  name: Build & publish Docker image to smartbear/gherkin-editor:<git-sha>
  runs-on: ubuntu-latest
  needs: [test-app, test-server, test-git]
  if: |
    (github.ref == 'refs/heads/main' || startsWith(github.ref, 'refs/tags/v') 
    && github.event_name == 'push' 
    && !contains(github.event.head_commit.message, '[ci skip]')
```
