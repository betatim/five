# 5️⃣ five

> The video ident checkpoint

## Build Setup

```bash
# install dependencies
$ yarn install

# serve with hot reload at localhost:3000
$ yarn dev

# build for production and launch server
$ yarn build
$ yarn start

# generate static project
$ yarn generate
```

For detailed explanation on how things work, check out [Nuxt.js docs](https://nuxtjs.org).

## Prerequisite: Install commitizen globally

Let's try to use commitizen for repo commits. Organised commit messages make it
easier to read and find certain commits. See https://github.com/commitizen/cz-cli#conventional-commit-messages-as-a-global-utility for a more detailed
description.

```bash
# Install commitizen
$ npm install -g commitizen

# Then install commitizen adapter
$ npm install -g cz-conventional-changelog

# Then create a .czrc file
$ echo '{ "path": "cz-conventional-changelog" }' > ~/.czrc
```
