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
