# Repository Rulesets

This document records the expected baseline GitHub ruleset for Zero Foundry
repositories.

Rulesets are configured in GitHub organization or repository settings. GitHub
does not automatically apply rulesets from this repository. This file is the
version-controlled source of intent for humans and automation that configure
repository rules.

## Baseline Ruleset

Importable JSON:

```text
rulesets/zero-ci-cd.json
```

Name:

```text
Zero CI/CD
```

Target:

```text
Branch ruleset targeting the default branch
```

Recommended scope:

```text
Organization ruleset for zero-foundry repositories
```

Current source export:

```text
Repository ruleset from zero-foundry/fod-claims-automation
```

## Rules

The baseline protects the default branch by requiring changes to flow through
Pull Requests and by preventing destructive history changes.

Repository merge and branch cleanup settings, including automatic deletion of
merged head branches, are tracked separately in
[`repository-settings.md`](repository-settings.md).

Required rules:

- Block branch deletion.
- Block non-fast-forward updates.
- Require a Pull Request before merge.
- Dismiss stale reviews when new commits are pushed.
- Require review thread resolution before merge.
- Allow merge commits as the merge method.

Current review posture:

- Required approving review count is `0`.
- Code owner review is not required.
- Last-pusher approval is not required.

This means the ruleset requires the Pull Request workflow and review-thread
hygiene, but does not yet require another person to approve. This is useful
while repositories are being bootstrapped by a small team or solo maintainer.

## Importable Shape

Use [`../rulesets/zero-ci-cd.json`](../rulesets/zero-ci-cd.json) as the
portable baseline for importing or recreating the ruleset.

The importable JSON intentionally omits repository-specific export fields such
as `id`, `source`, and `source_type`.

## Original Export Shape

The repository-level export that this policy is based on:

```json
{
  "name": "Zero CI/CD",
  "target": "branch",
  "source_type": "Repository",
  "source": "zero-foundry/fod-claims-automation",
  "enforcement": "active",
  "conditions": {
    "ref_name": {
      "exclude": [],
      "include": [
        "~DEFAULT_BRANCH"
      ]
    }
  },
  "rules": [
    {
      "type": "deletion"
    },
    {
      "type": "non_fast_forward"
    },
    {
      "type": "pull_request",
      "parameters": {
        "required_approving_review_count": 0,
        "dismiss_stale_reviews_on_push": true,
        "required_reviewers": [],
        "require_code_owner_review": false,
        "require_last_push_approval": false,
        "required_review_thread_resolution": true,
        "allowed_merge_methods": [
          "merge"
        ]
      }
    }
  ],
  "bypass_actors": []
}
```

The exported `id`, repository `source`, and repository `source_type` are not
portable org-wide policy. When recreating this as an organization ruleset, use
the importable JSON, organization scope, and the intended repository target set.

## Applying To New Repositories

When a new Zero Foundry repository is created:

1. Confirm the default branch is `main`.
2. Confirm the `Zero CI/CD` ruleset targets the default branch.
3. Confirm the repository is included in the organization ruleset target set.
4. Confirm direct pushes to `main` are blocked.
5. Confirm Pull Requests can merge with the expected merge method.

If a repository needs a temporary exception, document the reason and expected
removal date in that repository.

## Future Tightening

As projects mature, consider adding:

- at least one required approving review;
- required status checks;
- required CODEOWNERS review for sensitive paths;
- required linear history if merge commits become noisy;
- merge queue for repositories with frequent concurrent changes.
