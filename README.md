# Update-Angular

A short post explaining how to quickly upgrade your Angular version 5 application to the new version 6. I’ve used the same steps at my own project. This article is not meant to explain everything in depth, I’m just telling you only the basics.

Let start…
Globally
Add the new CLI
npm install @angular/cli@latest -g
Project
Upgrade the CLI locally in your project
ng update @angular/cli
Upgrade Angular dependencies
npm install @angular/animations@latest @angular/common@latest @angular/compiler@latest @angular/core@latest @angular/forms@latest @angular/http@latest @angular/platform-browser@latest @angular/platform-browser-dynamic@latest @angular/platform-server@latest @angular/router@latest --save
Upgrade Angular dev dependencies
npm install @angular-devkit/build-angular@latest @angular/compiler-cli@latest @angular/language-service --save-dev
Upgrade Angular dependent dependencies
npm install core-js@latest zone.js@latest --save
Upgrade Angular dependent dev dependencies
npm install @types/jasmine@latest @types/node@latest codelyzer@latest karma@latest karma-chrome-launcher@latest karma-cli@latest karma-jasmine@latest karma-jasmine-html-reporter@latest jasmine-core@latest jasmine-spec-reporter@latest protractor@latest tslint@latest --save-dev
Install TypeScript 2.7.2
npm install typescript@2.7.2 --save-dev
Install RxJS 6+
npm install rxjs@latest rxjs-compat@latest --save
And:

npm install rxjs-tslint@latest --save-dev
Followed by (you may need to run it a couple times to get it work):

rxjs-5-to-6-migrate -p src/tsconfig.app.json
Install Webpack 4+
npm install webpack@latest --save-dev
Check your angular.json file
Make sure it looks similar to the next example:

jeroenouw/AngularMaterialFirebase

AngularMaterialFirebase - Full stack starter app with Angular 6, Material Design and Firebase
github.com	
In your angular.json file there are a couple of lines that didn’t change correctly while upgrading to version 6.

Check if you have the following things set:

"newProjectRoot": "projects",
"sourceRoot": "src",
Deleted the second sourceRoot line
"outputPath": "dist/[your-package-name]",
"karmaConfig": "src/karma.conf.js",
"root": "./e2e",
"protractorConfig": "e2e/protractor.conf.js",
"exclude": ["**/node_modules/**"],
Moving files
Move the following files:

karma.conf.js from the root to the src directory
protractor.conf.js from the root to the e2e directory
Add browserslist
Create a file in src directory named browserslist (without extension). Add the next lines to it:

# This file is currently used by autoprefixer to adjust CSS to support the below specified browsers
# For additional information regarding the format and rule options, please see:
# https://github.com/browserslist/browserslist#queries
# For IE 9-11 support, please uncomment the last line of the file and adjust as needed
> 0.5%
last 2 versions
Firefox ESR
not dead
# IE 9-11
Enable Ivy Renderer
In your tsconfig.json file add:

"angularCompilerOptions": {
  "enableIvy": true
}
RxJS refactoring
In RxJS 6 and above, please make sure if you have Observables to change your import path from rxjs/Observable to rxjs/observable .

And if you use operators or similar import, please change the import way. The RxJS 5 way looks like this:

import 'rxjs/add/observable/of';
import 'rxjs/add/operator/map';
In RxJS 6 there is a new way of importing:

import { of } from 'rxjs';
import { map } from 'rxjs/operators';
Environment
Please add the following line at the top in your environment.ts if you want detailed errors from zone.js:
