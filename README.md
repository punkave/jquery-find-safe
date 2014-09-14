# `jquery.findSafe`

Run a query selector, but ignore matches nested within specific elements.

<a href="http://apostrophenow.org/"><img src="https://raw.github.com/punkave/jquery-projector/master/logos/logo-box-madefor.png" align="right" /></a>

**Problem**: I want to select all elements that match `.hello`, but not if `.hello` is inside of `.ignore-me`.

```html
<div class="parent">
  <div class="hello"></div>
  <div class="hello"></div>
  <div class="hello"></div>
  <div class="hello"></div>

  <div class="ignore-me">
    <div class="hello"></div>
  </div>
</div>
```

Running `$('.parent').find('.hello')` on the above markup will return all five instances of hello. We could use some tricky css-style selecting to isolate the four instances of `.hello` that aren't inside of `.ignore-me`, but that can be unreliable (and unreadable).

### `$.findSafe(selector, ignore)`

`$.findSafe` runs the `$.find` function but ignores any matches within a second selector. Using the example above:

```javascript
var hellos = $('.parent').findSafe('.hello', '.ignore-me');
// -> returns for instances of hello
```

`$.findSafe` works with arbitrarily nested elements. A more complex example:

```html
<div class="parent">
  <div class="hello"></div>
  <div class="hello"></div>
  <div class="hello"></div>
  <div class="hello"></div>

  <div class="ignore-me">
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

`$('.parent').findSafe('.hello', '.ignore-me')` still returns only the first four `.hello`s.

## About P'unk Avenue and Apostrophe

`jquery-projector` was created at [P'unk Avenue](http://punkave.com) for use in Apostrophe, an open-source content management system built on node.js. If you like `jquery-projector` you should definitely [check out apostrophenow.org](http://apostrophenow.org). Also be sure to visit us on [github](http://github.com/punkave).

## Support

Feel free to open issues on [github](http://github.com/punkave/jquery-projector).


<a href="http://punkave.com/"><img src="https://raw.github.com/punkave/jquery-projector/master/logos/logo-box-builtby.png" /></a>