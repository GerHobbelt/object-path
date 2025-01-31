

object-path
===========

Access deep properties using a path

[![NPM](https://nodei.co/npm/object-path.png?downloads=true)](https://nodei.co/npm/object-path/)

[![Build Status](https://travis-ci.org/mariocasciaro/object-path.png)](https://travis-ci.org/mariocasciaro/object-path)
[![Coverage Status](https://coveralls.io/repos/mariocasciaro/object-path/badge.png)](https://coveralls.io/r/mariocasciaro/object-path)
[![devDependency Status](https://david-dm.org/mariocasciaro/object-path/dev-status.svg)](https://david-dm.org/mariocasciaro/object-path#info=devDependencies)

[![browser support](https://ci.testling.com/mariocasciaro/object-path.png)](https://ci.testling.com/mariocasciaro/object-path)

## Install

### Node.js

```
npm install object-path
```

### Browser

```
bower install object-path
```

## Usage

```javascript

var obj = {
  a: {
    b: "d",
    c: ["e", "f"]
  }
};

var objectPath = require("object-path");

//get deep property
objectPath.get(obj, "a.b");  //returns "d"

//get the first non-undefined value
objectPath.coalesce(obj, ['a.z', 'a.d', ['a','b']], 'default'); 

//empty a given path (but do not delete it) depending on their type,so it retains reference to objects and arrays. 
//functions that are not inherited from prototype are set to null. 
//object instances are considered objects and just own property names are deleted 
objectPath.empty(obj, 'a.b'); // obj.a.b is now ''
objectPath.empty(obj, 'a.c'); // obj.a.c is now []
objectPath.empty(obj, 'a'); // obj.a is now {}

//works also with arrays
objectPath.get(obj, "a.c.1");  //returns "f"
objectPath.get(obj, ["a","c","1"]);  //returns "f"

//can return a default value with get
objectPath.get(obj, ["a.c.b"], "DEFAULT");  //returns "DEFAULT", since a.c.b path doesn't exists, if omitted, returns undefined

//set
objectPath.set(obj, "a.h", "m"); // or objectPath.set(obj, ["a","h"], "m");
objectPath.get(obj, "a.h");  //returns "m"

//set will create intermediate object/arrays
objectPath.set(obj, "a.j.0.f", "m");

//push into arrays (and create intermediate objects/arrays)
objectPath.push(obj, "a.k", "o");

//ensure a path exists (if it doesn't, set the default value you provide)
objectPath.ensureExists(obj, "a.k.1", "DEFAULT");

//deletes a path
objectPath.del(obj, "a.b"); // obj.a.b is now undefined
objectPath.del(obj, ["a","c",0]); // obj.a.c is now ['f']

```

### Credits

* [Mario Casciaro](https://github.com/mariocasciaro) - Author
* [Paulo Cesar](https://github.com/pocesar) - Major contributor




