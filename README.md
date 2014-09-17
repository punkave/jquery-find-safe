# `jquery.findSafe`

Run a query selector, but ignore matches nested within specific elements beneath the original element. Helps you cope with nested controls.

<a href="http://apostrophenow.org/"><img src="https://raw.github.com/punkave/jquery-projector/master/logos/logo-box-madefor.png" align="right" /></a>

**Problem**: I want to select all elements *inside* a div of class `nifty` that match `.hello`, but not if they are nested inside *another* div of class `nifty`.

```html
<div class="nifty outer">
  <div class="hello"></div>
  <div class="hello"></div>
  <div class="hello"></div>
  <div class="hello"></div>

  <div class="nifty">
    <div class="hello"></div>
  </div>
</div>
```

Running `$('.nifty.outer').find('.hello')` on the above markup will return all five instances of hello. If we try to solve this by using `:not` in a naive way, it will reject everything, because the original div also has the class `nifty`.

### Solution: `$.findSafe(selector, ignore)`

`$.findSafe` runs the `$.find` function but ignores any deeper matches of a second selector. Using the example above:

```javascript
var hellos = $('.nifty.outer').findSafe('.hello', '.nifty');
// -> returns four instances of hello
```

`$.findSafe` works with arbitrarily nested elements. A more complex example:

```html
<div class="nifty outer">
  <div class="hello"></div>
  <div class="hello"></div>
  <div class="hello"></div>
  <div class="hello"></div>

  <div class="nifty">
    <div>
      <div>
        <div>
          <div class="hello"></div>
        </div>
      </div>
      <div class="hello"></div>
    </div>
  </div>
</div>
```

`$('.nifty.outer').findSafe('.hello', '.nifty')` still returns only the first four `.hello`s.

## Changelog

0.1.2: clarified documentation re: only rejecting matches of the second selector *beneath* the original element.

0.1.1: much simpler implementation, thanks to [kachitta](https://github.com/kachitta). Also added a unit test in `test.html`.

## About P'unk Avenue and Apostrophe

`jquery-find-safe` was created at [P'unk Avenue](http://punkave.com) for use in Apostrophe, an open-source content management system built on node.js. If you like `jquery-find-safe` you should definitely [check out apostrophenow.org](http://apostrophenow.org). Also be sure to visit us on [github](http://github.com/punkave).

## Support

Feel free to open issues on [github](http://github.com/punkave/jquery-find-safe).


<a href="http://punkave.com/"><img src="https://raw.github.com/punkave/jquery-projector/master/logos/logo-box-builtby.png" /></a>
