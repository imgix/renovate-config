# renovate-config

A shareable Renovate config for imgix SDK repos

## How to use

Set your `renovate.json` config to:

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
