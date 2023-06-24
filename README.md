# 🔥🌎 Firebase Functions GitHub Action

## Usage

### Deploy on merge

Add a workflow (`.github/workflows/deploy.yml`):

```yaml
name: Deploy Functions

on:
  push:
    branches:
      - main
    # Optionally configure to run only for specific files. For example:
    # paths:
    # - "website/**"

jobs:
  deploy_functions:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - run: cd functions && npm ci
      - uses: jxw1102/action-functions-deploy@0.7.1
        with:
          firebaseServiceAccount: "${{ secrets.FIREBASE_SERVICE_ACCOUNT }}"
          projectId: your-Firebase-project-ID
```

## Options

### `firebaseServiceAccount` _{string}_ (required)

This is a service account JSON key. The easiest way to set it up is to run `firebase init hosting:github`. However, it can also be [created manually](./docs/service-account.md).

It's important to store this token as an
[encrypted secret](https://help.github.com/en/actions/configuring-and-managing-workflows/creating-and-storing-encrypted-secrets)
to prevent unintended access to your Firebase project. Set it in the "Secrets" area
of your repository settings and add it as `FIREBASE_SERVICE_ACCOUNT`:
`https://github.com/USERNAME/REPOSITORY/settings/secrets`.

### `projectId` _{string}_

The Firebase project that contains the Hosting site to which you
want to deploy. If left blank, you need to check in a `.firebaserc`
file so that the Firebase CLI knows which Firebase project to use.

### `firebaseToolsVersion` _{string}_

The version of `firebase-tools` to use. If not specified, defaults to `latest`.
