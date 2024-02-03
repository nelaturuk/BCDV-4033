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