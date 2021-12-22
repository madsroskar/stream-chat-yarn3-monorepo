# Stream Chat React Native monorepo with yarn 3 (berry)

Setting up React Native in a monorepo is tricky because it doesn't play well with hoisting.

This repo exists for me to test and have a reference for configuration of projects I encounter that use yarn berry for a monorepo setup

## The setup in short:

``` text
| root/
| .yarnrc.yml
| package.json
| -- packages/
| ---- RNApp/
| ---- package.json
| ---- metro.config.js
| ---- ExpoApp/
| ---- package.json
| ---- metro.config.js
```

### Configuration to note

#### Root package.json

``` json
  "packageManager": "yarn@3.1.1",
  "workspaces": [
    "packages/*"
  ]
```

#### Root .yarnrc.yml

``` json
yarnPath: .yarn/releases/yarn-3.1.1.cjs
nodeLinker: 'node-modules'
```

#### RNApp package.json

``` json
  "installConfig": {
    "hoistingLimits": "dependencies"
  }

```

#### RNApp metro.config.js

``` json
module.exports = {
  transformer: {
    getTransformOptions: async () => ({
      transform: {
        experimentalImportSupport: false,
        inlineRequires: true
      }
    })
  }
}

```
