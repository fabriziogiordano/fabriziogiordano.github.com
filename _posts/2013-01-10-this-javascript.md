---
layout: post
title: JavaScript this and meaning of document.querySelector.bind(document);
description: JavaScript this and meaning of document.querySelector.bind(document);
excerpt: JavaScript this and meaning of document.querySelector.bind(document);
---

###d.querySelector.bind(d);

I was checking some parallax optimization on [Html5Rocks](http://www.html5rocks.com/en/tutorials/speed/parallax/)
and I notice in a [script](http://www.html5rocks.com/static/demos/parallax/demo-1a/scripts/parallax.js):

<code>
(function(win, d) {

  var $ = d.querySelector.bind(d);

  ....

  var mainBG = $('section#content');

  ....

})(window, document);
</code>

**_```var $ = d.querySelector.bind(d);```_** was not immediately clear, why bind the document?

I asked on [Stackoverflow](http://stackoverflow.com/questions/14251357/what-is-the-meaning-of-document-queryselector-binddocument)
and I got a nice answer from [Bergi](http://stackoverflow.com/users/1048572/bergi):

_The function is not bound to a specific document (there may be other ones, not just window.document).
Try it without, and you will get an WRONG\_THIS\_ERR exception - you will need to apply it on an object that implements the [Document interface](http://www.w3.org/TR/selectors-api/#interface-definitions)._

_Also have a look on [MDN's introduction to the this keyword](https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Operators/this) on how the thisVal("context") of a function call is determined.
However I got back to some other considerations about the ```this``` keyword in JavaScript._


###this

Again it was about the ```this``` keyword in JavaScript. The closest mental representation I came up for the ```this``` keyword in JavaScript is that assuming we are in a browser and not in "strict mode" if we create a function:

```function a() { console.log(this); }```

and we call

```a();```

the console print ```window```. It is like JavaScript **append** ```this``` behind the scene eg. ```this.a();```. In this case ```this``` is the _window_ context.

For the same reason if we create a new object ```var o = {};``` and we assign the a method ```o.a = a; ``` and we execute ```o.a();```
the console print the ```o``` object.

Note, this might not be the proper explanation, but it is the easiest way for me to remember it.

Therefore for ```var $ = d.querySelector.bind(d);```  we are assigning to $ a new function _querySelector_. <br/>
```bind``` assign ```document``` as ```this``` of the new function.<br/>
At the end it is as we execute<br/>
**$('something')** as **document.querySelector('something')**


