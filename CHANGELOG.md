## 0.1.2 (2014-10-27)

* Bugfix: window.scrollX & window.scrollY are not available in IE, use fallback
* Feature: Add "timer" property to DOMSpot, which is used as default timer for
  new "appeared" queries.
* Mutation observer shim will only look for changes once per second, not 33 times

## 0.1.1 (2014-08-20)

* Added `appeared`: trigger callbacks when an element first appears on screen
* Bugfix: only relative positions to an element's parent were used, not to root

## 0.1.0 (2014-03-25)

* Fixed `introduced`: elements would only fire once for all the queries

## 0.0.1 (2014-03-09)

* First version