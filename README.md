Node
====

> Node projects style guide

### Table of contents

1. [Project architecture](#project-architecture)
1. [Main file](#main-file)
1. [Config files management](#config-files-management)
1. [Files content structure](#files-content-structure)
1. [Global data](#global-data)

### Project architecture

We suggest the next architecture for your node project, these suggestons are to help you make it understandable.

```sh
.
├── index.js
├── globals.js
├── config.js
├── lib/
└── cfg/
     └── development.js
     └── production.js
```

### Main file

To know which is the main file on your project, we recommend name it as index.js simulating the main file of web project, also in the index.js file, we suggest declare the root directory change code, to set the project directory on the function process.cwd().

```javascript
//Change the root path for all project
process.chroot(__dirname);

```

### Config files management

Use a folder called cfg with many files as you require to manage different params for specific environments.

For example:

```sh
└── cfg/
     └── development.js
     └── production.js
     └── testing.js
```

When you have the cfg folder, you must write a file that include code to manage the files to return analyzing the NODE_ENV variable on your OS, which you could set as "development", "production" or "testing".

```javascript
module.exports = (function(env) {
  return require('./config/' + env + '.js');
})((process.env.NODE_ENV || 'development'));

```

### Files content structure

```javascript
//Node libraries import
var http = require('http'),
    path = require('path');
    
//3th party libraries
var express = require('express'),
    redis = require('redis');

//Local libraries
var mylib1 = require(process.cwd() + '/lib/mylib1'),
    mylib2 = require(process.cwd() + '/lib/mylib2');

//Write your code below

```

### Global data

We suggest you to write a file global.js that helps you to keep global variables, all the project along and use it on your response sending.

The content in global.js, , for example:

```javascript
module.exports = function(req) {
    var data = {
        currencies: ['USD', 'MXN', 'EUR'],
        yearsLeft: (function(left) {
            var currentYear = new Date().getFullYear();
            var years = [];
            for (var i = 0; i < left; i++) {
                years.push(++currentYear);
            }
            return years;
        })(20)
    };
    return data;
}
```
