# Google Cloud Functions Typescript project template

A very minimal project template that deploys a Typescript project as a Google Cloud Function.

## Setup

First, you need to install and set up Google Cloud SDK. This includes creating a project in Google Cloud, enabling billing for it, installing Google Cloud SDK locally and then authorizing it. You can follow the section "Before you begin" of this [quickstart guide](https://cloud.google.com/functions/docs/quickstart). (Later sections are useful too, but not neccessary to use this project, as they just guide you through another code sample).

Then, clone this repository, navigate to it and set up npm:

`git clone git@github.com:golergka/gcf-typescript-template && cd gcf-typescript-template && npm init`

## Launching and deploying

This project is set up for a single function (called `helloWorld`), which you can test locally or deploy to the cloud.

To test locally, use **start** script:

`npm run start`

This will run Typescript compiler and functions framework in watch mode, so you can access your function on localhost. It will be rebuild when you modify your Typescript sources.

To deploy to your GCF project, use **deploy** script:

`npm run deploy`

## Modifying for your needs

You probably will want to change the name of the function from `helloWorld` to something more sensible. New function name needs to be the same in:

1. `index.ts`, where it is exported
2. **start** and **deploy** scripts in `package.json`

If you need to support more than one function in a single repo, you'll need to figure scripts for local testing and deployment on your own (or submit a PR here if you find a univeral and minimalistic way to do it).

## How it works

`tsconfig.json` configures Typescript compiler to treat `src` folder as source and output compiled Javascript files to `dist` folder. `package.json` specifies compiled `dist/index.js` as an entry point for the app. The `dist` folder is added to `.gitignore` file since these js files are build artifacts that you don't want to track. However, a `.gcloudignore` file (which works just as .gitignore, but for gcloud tool) does not include the `dist` folder in the ignore list, because it needs to upload these js files and use them for running your project.

For local testing, `functions-framework` and `tsc-watch` are used.
