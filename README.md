reqLog
===========

reqLog is a Node.js logging library that can

* print log messages according to your own functions
* be customized per module and per logging level
* have any amount of logging levels
* print statements in full color (background too!!!)
* print statements with console qualities such as "italics" or "bold"
* print messages with module name and current line number so you know from where it was called
* be configured from file or by a module

Install
-----
```javascript
npm install reqLog
```

Usage
-----
Use npm or download. Then add to your code:

```javascript
var log = require('reqLog').with(module);
```

*module* is object defined automatically by Node.js. If you don't want automatic module names, replace it with your desired string name.

```javascript
log.info(arg1, arg2, arg3);
```

Strings arguments are not inspected unless the log level allows for printing of the statement.  This avoids unnecessary JSON.stringify calls.

Examples
--------

```javascript
var log = require('reqLog').with(module);
log.info('Info message');
log.debug('Debug message');
log.warn('Warning message');
log.error('Error message');
log.trace('Trace message');
log.info('Array =', [1, 2, 3, 4], '; Object = ', {one: 1, two: 2});
```


Output samples
--------------

```
2012-02-00T00:00:00.000Z INFO  main:2 - Info message
2012-02-00T00:00:00.000Z DEBUG main:3 - Debug message
2012-02-00T00:00:00.000Z WARN  main:4 - Warning message
2012-02-00T00:00:00.000Z ERROR main:5 - Error message
2012-02-00T00:00:00.000Z TRACE main:6 - Trace message
2012-02-00T00:00:00.000Z INFO  main:7 - Array = [ 1, 2, 3, 4 ]; Object = { one: 1, two: 2 }
```

Advance Example
---------------

```javascript
var log = require('./examples/max_utilization_helper').with(module);
var iden = function(d) {return d;};

                                                              // qualifiers to make it a 'req' object
var req = {session: { user: {email: "jobs@metamarkets.com" } } , route: {}, res: {}, next: iden};
var fourtyTwo = 42;
log.info(req, "The answer to life the universe and everything: '", fourtyTwo, "'")
// "2012-02-00T00:00:00.000Z; main; jobs@metamarkets.com; INFO ; main:18; The answer to life the universe and everything: '!¿!fourtyTwo!¿!'; 1"

log.info(req, "Info counter should be at 2. Counter value:")
// "2012-02-00T00:00:00.001Z; main; jobs@metamarkets.com; INFO ; main:21; Info counter should be at 2. Counter value:; 2"

log.debug(req, "Debug counter should be at 1. Counter value:")
// "2012-02-00T00:00:00.001Z; main; jobs@metamarkets.com; DEBUG; main:24; Debug counter should be at 1. Counter value:; 1"

log.trace(req, "this should not execute. Level is not included (too low in stack)")
//
```

Take a look at the examples directory for different uses.


Changes
-------
0.0.1 - First npm release


License
-------
Released under MIT License. Enjoy and Fork!
