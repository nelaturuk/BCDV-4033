# Pipeline Stages

## Linting

- JSLint is a great tool for helping us issues with your code quickly and easily, ensuring that it meets coding standards and best practices. JSLint can be installed globally through npm by running the following command in the terminal:
- Use the command below to install jslint.
  `sudo npm i -g jslint`
- Now, we can run jslint on a file of our choosing. Let’s check simpleCalc.js.
  `jslint src/simpleCalc.js`
- JSLint gives us feedback for every line where it detects a syntax or stylistic error and gives us suggestions on how to fix the problem. This step will not pass successfully until all of the linting suggestions have been addressed.

**Lab 1 - Use the feedback from Linter to make changes and make the linter pass.**

## Manual Testing

- Jest is a JavaScript testing framework used to test React applications and other JavaScript codebases. Jest is fast, reliable, and easy to use, with a large collection of built-in tools that help developers write robust test cases quickly and efficiently.
- NPM gives us an easy way to install for use in local development or as part of the CI/CD process with the npm install -g jest command. Use jest command to test the simple calculator. 
  `jest`


## Task Automation - Create Task

- We can automate many tasks for our application by using npm, allowing us to run tasks quickly and without having to type out the code by hand every time.
NPM uses a file named package.json to manage dependencies and tasks. To automate a task with npm, we need to open the package.json file for our project. This is where we will write all of our tasks, or commands we want the package manager to execute.
- Let’s define a simple style check tasks
In the scripts section of our package.json file, we’ll add a command to let npm know how to execute what we request.
- In the scripts section of our package.json file, we’ll add a command to let npm know how to execute what we request.

`"style": "eslint src/simpleCalc.js"`
- Once the command is written into our package.json file and saved, we can run the automation task for your project in an open terminal using the following syntax.
  `npm run style`
  
**Lab 1 - Add a new task in the package.json for running "jest" command.**
- NPM provides us with output that indicates whether a task has failed or succeeded. Understanding this output is key to finding mistakes in our code, so it’s important to understand what npm is telling us.
- The exit code of the task defines success or error. If the result of the script is   0
  then the task was completed successfully. Otherwise, npm will return an exit code of   1
 , indicating an error which can prevent the execution of next tasks.
 - To fix more substantial errors, npm provides guidance on how to resolve them or where to look for help in its documentation guide. 
 - We’re also provided with a debugging log, npm-debug.log, with more detailed information on the task error. Once we have fixed all issues, npm will indicate success by returning an exit code of 0.
- By understanding npm outputs, we can accurately detect when errors occur and quickly resolve them to ensure that your tasks are properly automated.
NPM provides a wealth of information about its commands and how to use them, so make sure to check their documentation for any additional help or guidance needed.

**Lab 1 - Create a Sample Workflow in your Github Repository that runs a echo command displaying your name when we push changes to the repository.**

- Events
```
on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Output a message
        run: echo "Action Complete!"

// Commit this change. 
```

**Lab 1 - Add a sample npm project to your github repo. Create a github action that would perform multiple steps as listed below:**
- Checkout code
- Install dependencies in ubuntu.
- Run Jest test command on your repo. 

## Create Artifact

```
- name: Upload artifact
  uses: actions/upload-artifact@v3
  with: 
    name: assets
    path: dist
```

**Lab1 - Creat Artifact based on the build results of your project and upload it to your github repository**

## Add Unit Tests
- You can use `yarn jest` command to run unit tests in your repo. 

**Lab 1 - Create atleast 3 unit tests in your reository. You can use the sample calculator file in this repo. Run the tests using jest command.**

**Lab 1 - Add test task in your package.json**

## Creating GitHub Workflow action for testing

```
name: Unit Tests

on:
  # the 1st condition
  workflow_run:                             # triggers when "build" runs and completes  
    workflows: ["CI-CD"]
    types:
      - completed

jobs:                                       # create job called "test" to perform Unit Tests 
  test:  
    runs-on: ubuntu-latest.                 # this job will run on the latest version of Ubuntu
    steps:                                  # list of steps that need to be taken when Unit Tests is triggered 
    - uses: actions/checkout@v3             # check out code from repository
    - name: Install dependencies            # install all dependencies needed for Unit Tests (ex. Jest) 
      run: npx yarn    
    - uses: actions/download-artifact@v3    # download compiled code from build and make it available for Unit Tests 
      with:
        path: dist
    - name: Run Tests                       # run Unit Tests using Jest
      run: npx yarn test

```

**Lab 1 - Create a new workflow for runnning Unit tests after a build is done in GitHub actions**

**Lab 1 - Add commit tag for the unit test workflow in your readme file**

## Add pre-commit hook for your github

- Add Husky as a prepare task in your package.json file.

```
"scripts": {
    "lint": "npx eslint examples/*.js",
    "style": "prettier --check examples/example2.js",
    "format": "prettier --write examples/example2.js",
    "test": "jest",
    "prepare": "husky install"
  }
```
- Run the below command to add a pre-commit hook.

```
npx husky add .husky/pre-commit "npm style"
git add .husky/pre-commit
git commit -m "Add styling"
```

**Lab 1 - Create a pre-commit hook for your repo to run styling check. You can use your linter if you want to.**

## GitHub Action to run styling check 

```
  test:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
    - name: Install dependencies
      run: yarn    
    - uses: actions/download-artifact@v2
      with:
        name: assets
        path: dist
    - name: Run Lint Checks
      run: yarn style
```

## Automated Deployment

- Creating action in github to deploy app

```
  deploy:
    needs: build
    # Grant GITHUB_TOKEN the permissions required to make a Pages deployment
    permissions:
      pages: write      # to deploy to Pages
      id-token: write   # to verify the deployment originates from an appropriate source

    # Deploy to the github-pages environment
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}

    # Specify runner + deployment step
    runs-on: ubuntu-latest
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v1
```

- For Kubernetes

```
- uses: Azure/k8s-deploy@v4
  with:
     namespace: 'myapp'
     manifests: |
        dir/manifestsDirectory
     images: 'contoso.azurecr.io/myapp:${{ event.run_id }}'
     imagepullsecrets: |
        image-pull-secret1
        image-pull-secret2
```

## GitHub secrets

- below is the run command that accesses a secrets key

```
 - name: build
        run: |
          ./build.sh "${{ secrets.ASSETS_UPLOADER_KEY }}" "${{ secrets.ASSETS_UPLOADER_SECRET }}"
        timeout-minutes: 15
```

- Secrets as environment variables

```
- name: build
        run: |
          ./build.sh
        timeout-minutes: 15
        env:
        ASSETS_UPLOADER_SECRET: "${{ secrets.ASSETS_UPLOADER_SECRET }}"
        ASSETS_UPLOADER_KEY: "${{ secrets.ASSETS_UPLOADER_KEY }}"
```

**Lab 1 - Setup a GitHub action in your repo to get a secret API Key as an environment variable**


## HashiCorp Vault Example

```
  - name: Import Secrets
         uses: hashicorp/vault-action@v2
         id: secrets        
         with:
           url: https://vault.example.com/ 
           role: content
           method: jwt
           secrets: |
               kv/data/content/codio-ed-dev client_id;
               kv/data/content/codio-ed-dev secret_id;
       - name: Publish
         uses: codio/codio-assignment-publish-action@master
         with:
           client-id: ${{ steps.secrets.outputs.client_id }}
           secret-id: ${{ steps.secrets.outputs.secret_id }}
           course-name: <Course Name>
           assignment-name: <Assignment Name>
           dir: ./
           changelog: ${{ github.event.head_commit.message }}
```