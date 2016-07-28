# Contribution guide :crystal_ball:

[STYLE GUIDE read before making a commit](https://github.com/feross/standard)

[Some interactive tutorials](http://nodeschool.io/#workshoppers)

[Install node.js](https://nodejs.org/en/)

If you are using a computer where you do not have administrator access, create an account on [Cloud 9 IDE](https://c9.io/) which will give you access to a virtual machine with node.js and javascript editor that will run in the browser. You can then make a new workspace directly from a github repository where you can run `npm` and `standard`.

To lint your code using Standard.JS and check that it conforms to the style guide you can use the "standard" node module. To install this globally run:

```bash
$ npm install -g standard
```

After that you can run the command ```standard``` in the root directory of the project and it will alert you to javascript formatting errors in any of the source files. You can *automagically* fix any errors by running.

```bash
$ standard --fix
```

Programming guide:
------------------

If you enter in a new function, add it to the ```exampleNS``` namespace e.g. if you want to add the ```clamp``` function to the ```exampleNS``` namespace write something like this:

```javascript
var exampleNamespace = {};

(function (exampleNS) {
  ...
  exampleNS.clamp = function (x, min, max) {
    if (x <= min) {
      return min
    } else if (x > min && x < max) {
      return x
    } else if (x >= max) {
      return max
    }
  }
  ...
})(exampleNamespace)
```

You can then call this from inside the namespace like this:

```javascript
...
(function (exampleNS) {
  ...
  exampleNS.somefunc = function () {
    var y = exampleNS.clamp(15, 10, 20)
  }
  ...
})(exampleNamespace)
```

and from other scripts like this:

```javascript
var y = exampleNamespace.clamp(15, 10, 20)
```

If you want to declare a namespace-local "private" variable or function, then declare it as normal but within the namespace:

```javascript
...
(function (exampleNS) {
  var namespaceLocal = 5
  ...
  exampleNS.addOne = function () {
    return namespaceLocal + 1
  }
  ...
})(exampleNamespace)

console.log(namespaceLocal === undefined); // true
```

Create objects as normal:

```javascript
...
(function (exampleNS) {
  ...
  exampleNS.Vector3 = function (x, y, z) {
    this.x = x
    this.y = y
    this.z = z
  }

  exampleNS.Vector3.prototype.getLength = function () {
    return Math.sqrt(Math.pow(this.x, 2), Math.pow(this.y, 2), Math.pow(this.z, 2))
  }
  ...
})(exampleNamespace)

var vector = new exampleNamespace.Vector3(3, 4, 5)
console.log(vector.getLength()) // 7.07...
```
