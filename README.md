# DOMSpot

DOMSpot allows you to detect when DOM elements are inserted, moved around or
removed from the document.

It uses a MutationObserver instance at its core.
If the browser doesn't have a MutationObserver implementation, a polyfill
will be used.

## In the Browser

Using DOMSpot is very easy, just include it like this

```html
<script src="domspot.js"></script>
<script>

    DOMSpot.placed('.added', function(list) {
        console.log('These items were placed:')
        console.log(list);
    });

</script>
```

## Documentation

### introduced(query, [includePresent,] callback)

When an element matching the given query is added to the document for the first
time, the given callback will be called.

Note: elements removed from the document and re-inserted later will not trigger
this again. It only happens once in an element's lifetime.

__Arguments__

* query - The CSS3 query selector the element should match to.
* includePresent - Wether this callback should be triggered for elements that
  were already in the document before this listener was added.
  Defaults to true.
* callback(ArrayOfElements) - A callback that gets an array of all the matching
  elements.

__Example__

```js
DOMSpot.introduced('.added', function(list) {
	console.log('These items were introduced:')
	console.log(list);
});
```

---------------------------------------

### placed(query, [includePresent,] callback)

When an element matching the given query is placed somewhere in the document,
the given callback will be called.

Note: this will always fire after an `introduced` event.

__Arguments__

* query - The CSS3 query selector the element should match to.
* includePresent - Wether this callback should be triggered for elements that
  were already in the document before this listener was added.
  Defaults to true.
* callback(ArrayOfElements) - A callback that gets an array of all the matching
  elements.

__Example__

```js
DOMSpot.placed('.added', function(list) {
	console.log('These items were placed:')
	console.log(list);
});
```

---------------------------------------

### taken(query, callback)

When an element matching the given query is taken from the document,
the given callback will be called.

Note: for an element already in the document, this will fire before the `placed`
or the `removed` event.

__Arguments__

* query - The CSS3 query selector the element should match to.
* callback(ArrayOfElements) - A callback that gets an array of all the matching
  elements.

__Example__

```js
DOMSpot.taken('.added', function(list) {
	console.log('These items were taken:')
	console.log(list);
});
```

---------------------------------------

### removed(query, callback)

When an element matching the given query is removed from the document,
the given callback will be called.

Note: removed does NOT mean destroyed. There is no way to check for destroyed
items in JavaScript.

Side effect: the element being removed will get a property called
'__domspot_removed'. The initial value is 1, and it will increase every time
it is removed from the document.

In case it is absolutely necesary to check for re-introductions, this property
can be consulted.

Note again: laggy functions can cause elements to be 'removed' from the document
for a short while, before being added again.

__Arguments__

* query - The CSS3 query selector the element should match to.
* callback(ArrayOfElements) - A callback that gets an array of all the matching
  elements.

__Example__

```js
DOMSpot.removed('.added', function(list) {
	console.log('These items were removed:')
	console.log(list);
});
```

---------------------------------------

### appeared(query, options, callback)

When an element matching the given query is first visible on the screen,
the given callback will be called.

___Arguments___

* `query` - The CSS3 query selector the element should match to.
* `options` - The optional object containing the following options:
 * `topOffset` - How close the element should be to the viewport
 * `leftOffset` - How close the element should be to the viewport
 * `interval` - Per how many milliseconds the checker should fire. Default 250ms
* `callback(ArrayOfElements)` - Callback that gets an array of appeared elements

__Example__

```js
DOMSpot.appeared('.myClass', function(list) {
	console.log('These items are now visible on the screen:');
	console.log(list);
});
```