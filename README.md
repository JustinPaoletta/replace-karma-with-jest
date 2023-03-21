# Replacing Karma With Jest

This project was generated with [Angular CLI](https://github.com/angular/angular-cli) version 14.1.3.

## Instructions 

To replace Karma with Jest in your Angular project follow these steps

1) Delete these files: 

    - karma.conf.js
    - src/test.ts (if it exists)

<br>

2) Remove the following from dev dependencies in package.json:

    "@types/jasmine"\
    "jasmine-core"\
    "karma"\
    "karma-chrome-launcher"\
    "karma-coverage"\
    "karma-jasmine"\
    "karma-jasmine-html-reporter"

<br>

3) Install Jest:

    ```
    npm i -D jest @types/jest ts-jest @angular-builders/jest jest-preset-angular
    ```

<br>

4) Create a Jest Config at the project root level named jest.config.js:

    /** content of jest.config.js */

    ```
    module.exports = {

    collectCoverageFrom: [
        '<rootDir>/src/app/**/*.ts',
        '!<rootDir>/src/app/**/index.ts',
        '!<rootDir>/src/app/**/*.module.ts'
    ],

    coverageDirectory: 'coverage',

    coverageReporters: [
        'lcov',
        'text-summary'
    ],

    testPathIgnorePatterns: [
        '<rootDir>/coverage/',
        '<rootDir>/dist/',
        '<rootDir>/e2e/',
        '<rootDir>/node_modules/',
        '<rootDir>/src/app/*.(js|scss)'
    ],

    testMatch: [
        '<rootDir>/src/app/*.spec.ts',
        '<rootDir>/src/app/**/*.spec.ts'
    ]
    };
    ```

<br>

5) In tsconfig.spec.json:

    - Replace jasmine with jest in the compilerOptions.types array

    - Add this key pair in compilerOptions: "module": "commonjs",

    - Remove "src/test.ts" from the files array (if it exists)

<br>

6) Edit angular.json:

    Remove projects.projectname.architect.test and replace with:

    ```
    "test": {
        "builder": "@angular-builders/jest:run",
        "options": {}
    },
    ```

<br>

7) Delete node_modules and re-install

    ```
    npm i
    ```

<br>

8) Run your tests:

    ```
    npm run test
    ```

<br>

9) You can also run the tests with coverage by adding a script in package json:
    
    ```
    "test:cov": "ng test --coverage"
    ```

    Execute the script on the command line:

    ```
    npm run test:cov
    ```

<br>

### Thanks For Reading :)
Written by Justin Paoletta
