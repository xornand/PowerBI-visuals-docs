#Visual Project

This document contains basic information about the visual project structure

##File Structure

* **.tmp/**
    * hidden temp directory used for compiling (do not modify)
* **.vscode/**
    * settings for [VS Code](https://code.visualstudio.com/)
* **assets/**
    * Used to store visual assets (icon, screenshots, etc)
* **dist/**
    * when you run `pbiviz package` the pbiviz file will be generated here
* **src/**
    * Typescript code for your visual goes here
* **style/**
    * Less styles for your visual go here
* **typings/**
    * Used to store TypeScript type definitions
* **.gitignore**
    * tells git to ignore files that shouldn't be tracked in the repository
* **capabilities.json**
    * used to define the capabilities of your visual [learn more about visual capabilities](Capabilities/readme.md)
* **package.json**
    * Used by npm to manage modules [learn more about npm](https://www.npmjs.com/)
* **pbiviz.json**
    * Main configuration file for your visual
* **tsconfig.json**
    * Typescript compiler settings [learn more about tsconfig](https://www.typescriptlang.org/docs/handbook/tsconfig-json.html)
* **typings.json**
    * Used by typings to manage TypeScript type definitions [learn more about typings](https://github.com/typings/typings) 
    
##pbiviz.json

This file is the main configuration file for your visual. It contains metadata as well as information about the files needed to build your visual.

```javascript
{
    "visual": {
        "name": "myVisual", // internal visual name (should not contain spaces)
        "displayName": "My Visual!", // visual name displayed to user (used in gallery)
        "guid": "PBI_CV_xxxxxxx", // a unique id for this visual MUST BE UNIQUE
        "visualClassName": "Visual" // the entry class for your visual
        "version": "1.0.0", // visual version. Should be semantic version (increment if you update the visual)
        "description": "", // description used in gallery
        "supportUrl": "", // url to where users can get support for this visual
        "gitHubUrl": "" // url to the source in github (if applicable)
    },
    "apiVersion": "1.0.0", //API version this visual was created with
    "author": {
        "name": "", // your name
        "email": "" // your e-mail
    },
    "assets": {
        "icon": "assets/icon.png" // relative path to your icon file (20x20 png)
    },
    "style": "style/visual.less", // relative path to your less file
    "capabilities": "capabilities.json" // relative path to your capabilities definition 
}
```


##Visual source (TypeScript)

Visual code should be written in TypeScript which is a superset of JavaScript that supports some advanced features and early access to ES6/ES7 functionality.
 
All TypeScript files should be stored in the `src/` directory and added to the `files` array in `tsconfig.json` so the typescript compiler knows to load them and in what order.

When your visual is built all of the typescript will be compiled into a single JavaScript file so you can reference exported elements from other files without needing to manually `require` them (as long as both files are listed in the tsconfig).

Feel free to create as many files and classes as you need to create your visual. 

[Learn more about TypeScript](http://www.typescriptlang.org/)


##Visual style (Less)

Visual styling is handled using css. For your convinence, we use the Less pre-compiler which supports some advanced features such as nesting, variables, mixins, conditions, loops, etc. If you don't want to use any of these features you can just write plain css in the less file and it will work perfectly fine.

All Less files should be stored in the `style/` directory whichever file is specified under `style` in your `pbiviz.json` file will be loaded. Any additional files should be loaded using `@import`.

[Learn more about Less](http://lesscss.org/)