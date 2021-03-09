# renovate-config

A shareable Renovate config for imgix SDK repos

## How to use

1. Set your `.renovaterc.json` or `renovate.json` config to:

  ```json
  {
    "extends": ["github>imgix/renovate-config"]
  }
  ```

2. You will also need to ensure that CI (e.g. Travis) will run for `renovate/*` branches.

3. Extend the config in a way that suits your repo. For example, in Angular we have configured some dependencies not to update for major updates:

  ```json
  "packageRules": [
    {
      "packagePatterns": [
        "^@angular/",
        "^zone.js$",
        "^@angular-devkit/",
        "^jasmine",
        "karma",
        "ng-packgr",
        "protractor",
        "tslint",
        "typescript"
      ],
      "updateTypes": ["major"],
      "enabled": false
    },
    {
      "packagePatterns": [
        "typescript"
      ],
      "updateTypes": ["major", "minor"],
      "enabled": false
    }
  ]
  ```

### Required status checks

You may need to configure `requiredStatusChecks` if PRs or branches aren't automerging as they should.

See [https://docs.renovatebot.com/configuration-options/#requiredstatuschecks](https://docs.renovatebot.com/configuration-options/#requiredstatuschecks) for more information

### Integration with Semantic Release

Since this config instructs dependency updates to use `deps(deps):` and dev-depedency updates to use `dev(dev-deps):` for commit messages, you should consider configuring Semantic Release to use these different messages to release dependency updates as new versions. 

To do this, update your Semantic Release plugin configuration to have the following:

```json
[
  "@semantic-release/commit-analyzer",
  {
    "releaseRules": [
      // Any other rules you want, e.g. for "docs:" PRs
      {
        "type": "deps",
        "scope": "deps",
        "release": "patch"
      }
    ]
  }
],

// and

[
  "@semantic-release/release-notes-generator",
  {
    "preset": "conventionalcommits",
    "writerOpts": {
      "types": [
        {
          "type": "feat",
          "section": "Features"
        },
        {
          "type": "fix",
          "section": "Bug Fixes"
        },
        {
          "type": "docs",
          "section": "Documentation",
          "hidden": false
        },
        // 👇 Important part
        {
          "type": "deps",
          "section": "Dependency Updates",
          "hidden": false
        },
        {
          "type": "chore",
          "hidden": true
        },
        {
          "type": "style",
          "hidden": true
        },
        {
          "type": "refactor",
          "hidden": true
        },
        {
          "type": "perf",
          "hidden": true
        },
        {
          "type": "test",
          "hidden": true
        }
      ]
    }
  }
],
```



