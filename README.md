# renovate-config

A shareable Renovate config for imgix SDK repos

## How to use

Set your `.renovaterc.json` or `renovate.json` config to:

```json
{
  "extends": ["github>imgix/renovate-config"]
}
```

Extend the config in a way that suits your repo. For example, in Angular we have configured some dependencies not to update for major updates:

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
