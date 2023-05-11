# simenandre/publish-with-yarn

This composite action will publish your package to NPM using Yarn.

It parses tag version and set that in `package.json` before publishing, and pushes that
to the default branch after publishing.

```yaml
name: Release to NPM

on:
  release:
    types: [released]

jobs:
  release:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3

      - name: Use Node LTS ✨
        uses: actions/setup-node@v3
        with:
          node-version: lts/*
          registry-url: https://registry.npmjs.org
          cache: yarn

      - name: Install dependencies 📦️
        run: yarn install --immutable

      - name: Build 🔨
        run: yarn build

      - uses: simenandre/publish-with-yarn@v1
        with:
          npm-auth-token: ${{ secrets.NPM_TOKEN }}
```

## Other actions

- [simenandre/publish-with-yarn-classic](https://github.com/simenandre/publish-with-yarn-classic)
- [simenandre/publish-with-pnpm](https://github.com/simenandre/publish-with-pnpm)