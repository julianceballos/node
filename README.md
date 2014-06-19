Node
====

> Node projects style guide

### Table of contents

1. Project architecture
2. Main file
3. Config files management
4. Files content structure
5. Global data

### Project architecture

We suggest the next architecture for your node project, to help you make undestandable project for your current and future contributors.

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

We suggest name the main file as index.js, this just as a similar for an website that starts with index.html and change the project root directory for keep the root path all the subfolders along with process.cwd() function.

```javascript
//Change the root path for all project
process.chroot(__dirname);

```



### Config files management

We suggest you to use a folder called cfg with many files as you require to manage different config params.

For example:

```sh
└── cfg/
     └── development.js
     └── production.js
     └── testing.js
```

And you must write a file that would include code to manage the files to return analyzing the NODE_ENV variable on your OS.

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

We suggest you to write a file global.js that helps you to keep global variables, all the project along and use it on your response returns.

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


