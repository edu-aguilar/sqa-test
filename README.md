# Sopra Quiz 

<!-- [![Build Status](https://travis-ci.org/PolymerElements/polymer-starter-kit.svg?branch=master)](https://travis-ci.org/PolymerElements/polymer-starter-kit) -->

This is an internal app created for testing the technical skills of possible new employees, in hopes of helping the human resources team with the recruitment process. It uses [Polymer 2](https://www.polymer-project.org/2.0/docs/about_20), [Flexbox Layout](https://css-tricks.com/snippets/css/a-guide-to-flexbox/) and [CSS Grid Layout](https://css-tricks.com/snippets/css/complete-guide-grid/). 

This project was created using the `polymer-cli` toolchain and is based of the `starter-kit` template provided by the Polymer team. 

### Setup

##### Prerequisites

First, install [Polymer CLI](https://github.com/Polymer/polymer-cli) using [npm](https://www.npmjs.com) (we assume you have pre-installed [node.js](https://nodejs.org)).

    npm install -g polymer-cli

Second, install [Bower](https://bower.io/) using [npm](https://www.npmjs.com)

    npm install -g bower

Finally, install dependencies for [esLint](https://eslint.org/)

    npm install -g eslint eslint-config-google eslint-plugin-html

##### Install bower dependencies 

After cloning the project from the repository, install the dependencies using bower 

    cd sopra-quiz-app
    bower install

### Start the development server

This command serves the app at `http://127.0.0.1:8081` and provides basic URL routing for the app:

    polymer serve

*Optional:* you can add the `-o` or `--open` flag and the command will serve the app and open it in your default browser.  

    polymer serve -o


### Build

The `polymer build` command builds your Polymer application for production, using build configuration options in our project's `polymer.json` file.  

You can configure your `polymer.json` file to create multiple builds. This is necessary if you will be serving different builds optimized for different browsers. You can define your own named builds, or use presets. See the documentation on [building your project for production](https://www.polymer-project.org/2.0/toolbox/build-for-production) for more information.

We maintain [the three builds](https://www.polymer-project.org/2.0/toolbox/build-for-production#build-presets) provided by the Polymer Starter Kit:

```
"builds": [
  {
    "preset": "es5-bundled"
  },
  {
    "preset": "es6-bundled"
  },
  {
    "preset": "es6-unbundled"
  }
]
```

Builds will be output to a subdirectory under the `build/` directory as follows:

```
build/
  es5-bundled/
  es6-bundled/
  es6-unbundled/
```

* `es5-bundled` is a bundled, minified build with a service worker. ES6 code is compiled to ES5 for compatibility with older browsers.
* `es6-bundled` is a bundled, minified build with a service worker. ES6 code is served as-is. This build is for browsers that can handle ES6 code - see [building your project for production](https://www.polymer-project.org/2.0/toolbox/build-for-production#compiling) for a list.
* `es6-unbundled` is an unbundled, minified build with a service worker. ES6 code is served as-is. This build is for browsers that support HTTP/2 push.

Run `polymer help build` for the full list of available options and optimizations. Also, see the documentation on the [polymer.json specification](https://www.polymer-project.org/2.0/docs/tools/polymer-json) and [building your Polymer application for production](https://www.polymer-project.org/2.0/toolbox/build-for-production).

### Preview the build

This command serves your app. Replace `build-folder-name` with the folder name of the build you want to serve.

    polymer serve build/build-folder-name/

### Run tests

This command will run [Web Component Tester](https://github.com/Polymer/web-component-tester) against the browsers currently installed on your machine:

    polymer test

Alternatively, you can run tests on your browser by going to `http://127.0.0.1:8081/test/`. You could also just run tests for an specific component by adding the name of the file that contains those tests, e.g. `http://127.0.0.1:8081/test/sopra-quiz-app.html`.

If running Windows you will need to set the following environment variables:

- LAUNCHPAD_BROWSERS
- LAUNCHPAD_CHROME

Read More here [daffl/launchpad](https://github.com/daffl/launchpad#environment-variables-impacting-local-browsers-detection)

### Document elements

We follow the recommendations provided by the Polymer team to document our components. You can read more about it in the [Polymer 2 documentation](https://www.polymer-project.org/2.0/docs/tools/documentation).

    polymer analyze > analysis.json

This command will generate an `analysis.json` file that contains the documentation of every element in your project.
At the moment of writing this, the command is still in beta and has some issues, one of them being that it includes the documentation to every single dependencia your component has (yes, this includes Polymer itself)! So, the hack to overcome this problem is extending your element from a "mixing", 

    class NewElement extends (class extends Polymer.Element {}) 

Now `polymer analyze` will generate a clean documentation for your element.

### Adding a new view

You can extend the app by adding more views that will be demand-loaded e.g. based on the route, or to progressively render non-critical sections of the application. Each new demand-loaded fragment should be added to the list of `fragments` in the included `polymer.json` file. This will ensure those components and their dependencies are added to the list of pre-cached components and will be included in the build.

### Multi-language

We use [i18n-msg](https://www.webcomponents.org/element/ebidel/i18n-msg) to make our app multi-language. This component replaces literals found in our app with the corresponding translation in the current language.

The configuration is pretty simple. The `sopra-quiz-app.html` extends from the `i18n-msg` behavior and we have a property called `language` that holds the current language (`es` by default) and we set this on the global `I18nMsg` object, 

    I18nMsg.lang = this.language;

This line of code sets the current language and loads the object with the translations (`locales\es.json`). After doing this you just need to add the `i18n-msg` dependency to your component (if needed) and use the `i18n-msg` tag or behavior. For more information on how these two work check the [i18n-msg documentation](https://www.webcomponents.org/element/ebidel/i18n-msg).

```
<i18n-msg msgid="label"> Label </i18n-msg>
```

### Work-flow

We use `git-flow` to create our branches for new features and hotfixes, along with their rules for merging those into `develop` and updating `master`. For more information about `git-flow` you can read [Daniel Kummer's cheatsheet](https://danielkummer.github.io/git-flow-cheatsheet/).

Following these rules, you should always create your new branches from `develop` and once you're done you must create a **Pull Request** and **only the administrators can approve and merge your branch into `develop`**. 

In general, we use English as our main language when coding. So, every commit, comment on pull requests, line of code, comment in code and documentation **has** to be written in English. 

##### Semantic commits

We like our commit messages to be **clear** and describe the content of the commit itself. Also, we use [semantic commits](https://seesparkbox.com/foundry/semantic_commit_messages) messages and this makes our `git log` easier to read and understand. 

Commit type | Description                                                        |
------------|--------------------------------------------------------------------|
feat        | new                                                                |
fix         | bug fix                                                            |
docs        | changes to documentation                                           |
style       | formatting, missing semi colons, etc; no code change               |
refactor    | refactoring production code                                        |
test        | adding missing tests, refactoring tests; no production code change |
chore       | updating grunt tasks etc; no production code change                |

An example of a semantic commit of type `chore` could be

    git commit -m "chore: added semantic commit section to readme file" 

##### Steps before creating a Pull Request - Definition of code ready 

These are a few key points we defined to determined if our code is ready for a Pull Request,

- Finish your user story or chore functionalities. Make sure to use `i18n-msg` for any literal or label you use in your code, this will make sure the app remains multi-language. 
- If you have any custom styles in your components, make sure you leave `mixins` open for users to change them. 
- Document your component and create the file `analysis.json` to see it. Make sure everything looks good.
- Create the unit tests for your component. In general we usually create them in the following order,
    - Validate the existance of imported components.
    - Validate that the received properties have the right type.
    - Test your component functionalities. 
- Run the task `npm run validate-branch`. This will make sure your branch is valid for deployments. 
- Make sure our app diagram (_draw.io_) is up to date with the current state of the code. 
- Finally, create your Pull Request with a short description to let reviewers briefly know what you did.
