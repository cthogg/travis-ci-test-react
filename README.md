Minimal setup for a react app with travis ci, and deploy to github pages. 

## Inspired From
`https://medium.com/@bezgachev/6-simple-steps-to-automatically-test-and-deploy-your-javascript-app-to-github-pages-c4c32a34bcb1`

## Stack 
1. create react app 
2. travis-ci 
3. github pages

## Create React App 
1. Download the npm pacakge for create react app: 
`npm i create-react-app`
2. Then create a new app by: 
`npx create-react-app my-app`
3. `cd` into `./my-app`
4. To test `npm test`

## Travis CI 
1. In your user profile `https://travis-ci.org/profile/USERNAME` make sure the public repo is activated. 
2. In the public repo add `.travis.yml` and add the following to the file: 

```yaml
language: node_js
node_js:
  - "stable"
cache:
  directories:
  - node_modules
script:
  - npm test
  - npm run build
deploy:
  provider: pages
  skip_cleanup: true
  github_token: $GITHUB_TOKEN
  local_dir: build
  on:
    branch: master
```
## Githb pages
1. Create a githb personal access token. 
2. Create a GITHUB_TOKEN environmental variable in the settings of the travis-ci project.
`https://travis-ci.org/GITHUB_USERNAME/REPO_NAME/settings` 
3. Setup homepage in `package.json` file. 
  `"homepage": "https://GITHUB_USERNAME.github.io/REPO_NAME/",`
3. When you commit and push you should see a `gh-page` branch. These are the static files which are served to github pages. 

## Adding Eslint and Prettier 
inspired from 
`https://www.youtube.com/watch?v=bfyI9yl3qfE`
ESlint should already be installed in  `,/node_modules`
1. Check the version `./node_modules/.bin/eslint --version`
2. Run the init `./node_modules/.bin/eslint --init`
3. An `.eslintrc.json` file should be created in the project root. 
4. Install Prettier by `npm i prettier eslint-config-prettier eslint-plugin-prettier -D `
5. In the `.eslintrc.json` file add 

```json
{
    "extends": ["react-app", "plugin:prettier/recommended"]
}
```
6. Run eslint (with prettier by) `./node_modules/.bin/eslint . ` (pay attention to the dot) or `npm run lint` 
7. Automatic fixing `./node_modules/.bin/eslint --fix . ` or  `npm run lint-fix`
8. Ignore RegisterServiceWorker by adding an `.eslintignore` file and `/src/registerServiceWorker.js`