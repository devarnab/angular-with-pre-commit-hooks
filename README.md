# Angular With PreCommit Hooks

This project was generated with [Angular CLI](https://github.com/angular/angular-cli) version 10.0.3.

## Husky Pre-commit hook Setup

This is the pre-commit hook set up a strategy for angular projects. By setting this hook we can ensure that committed files will be linting error-free and formatted with prettier code-formatter. This is a sanitization technique before pushing any code that may have a linting issue or having a build issue.

<strong>STEP I:</strong> Run below command:

```javascript
yarn add husky lint-staged prettier -D
```

- `husky` makes it easy to use githooks as if they are npm scripts.
- `lint-staged` allows us to run scripts on staged files in git. See this [blog post about lint-staged to learn more about it](https://medium.com/@okonetchnikov/make-linting-great-again-f3890e1ad6b8).
- `prettier` is the JavaScript formatter we will run before commits.

<strong>STEP II:</strong> Add below configuration to package.json file:

```javascript
"devDependencies": {
  // ...
},
"lint-staged": {
  "src/**/*.{js,ts,scss,md,html,json}": [
    "prettier --write",
    "git add"
  ]
},
"husky": {
  "hooks": {
    "pre-commit": "ng lint && lint-staged",
    "pre-push": "ng build --prod"
  }
}
```

## Usage

<strong>STEP I:</strong> Run below command to stage your un-committed files

```javascript
git add .
```

<strong>STEP II:</strong> Run below to commit the changes

```javascript
git commit -m <commit message>
```

 - It will run `ng lint` first to lint the files. If there is any linting issue, it will not proceed to commit the files, else, the staged files will be formatted automatically and committed.

### If there are linting issues:

 - First, resolve the linting issues then again start from STEP I.

<strong>STEP III:</strong> Run below to push the changes to repo

```javascript
git push
```
This will run the `ng build --prod` command first to check if the build is not getting failed by the new changes. If everything works fine it will let you finally push the code to the repo.
