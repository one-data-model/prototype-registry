# One Data Model Registry

[One Data Model Registry](https://one-data-model.github.io/prototype-registry/)


### Update JSON file
1. `data/convertjson.json`stores the content of the registry.
2. Each time that a new registration is introduced this file MUST be updated.

### Run In Development - On Terminal
Before rendering the GitHub Pages the dynamic table MUST be `build`.

To do that follow this process:

`1. npm install`

`2. npm audit fix`
(if needed)

`3. npm run-script build`

`4. npm run-script build:server`

`5. npm run-script server`

Go to `Localhost:9088` in your browser to verify that the new content is available.

### GitHub pages
During the `build` the dynamic pages are created and stored in:
* `/dev/server/dist/build.js`, and
* `/dev/server/dist/build.js.map`

1. `Push` these two files to the `gh-pages` of the official registry.
2. Refresh `gh-pages` by forcing a new build.
3. The new content should be available in the GitHub Pages.

