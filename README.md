# express-metrics

Express middleware for collecting and reporting metrics about response times.

## Installation

Node.js, on project path:

```
npm install express-metrics
```

## Examples

Node projects:

```js
var express = require('express');
var metrics = require('express-metrics');
var app = express();

// add '/metrics' route to summary the response times
app.use(metrics(app));

// express-metrics will record the response time for every time this handler returns
// the greet
app.get('/', function (req, res, next) {
  res.json({greet: 'Helo world!'});
});
```

then, in /metrics path, you  will see:
```js
{
  'GET_/': {
    type: "timer",
    duration: {
      type: "histogram",
      min: 1,
      max: 49,
      sum: 140,
      variance: 136.69005847953213,
      mean: 7.368421052631579,
      std_dev: 11.691452368270253,
      count: 19,
      median: 2,
      p75: 5,
      p95: 49,
      p99: 49,
      p999: 49
    },
    rate: {
      type: "meter",
      count: 19,
      m1: 0.09594670244481206,
      m5: 0.019860059817214587,
      m15: 0.007863370827271138,
      mean: 0.008451182854240225,
      unit: "seconds"
    }
  }
}
```
_Note:_ requests are grouped by method and path. Also, metrics for all request are added.

If you want change the default route to metrics:

```js
var express = require('express');
var metrics = require('express-metrics');
var app = express();

app.use(metrics());

app.get('/', function (req, res, next) {
  res.json({greet: 'Helo world!'});
});

app.get('/custom', metrics.summary);
```

## Contributions

Do you want to contribute?. Please, follow the below suggestions:
  - To add features, `pull requests` to `develop` branch.
  - To fix bugs in release version, `pull request` both `master` and `develop` branches.
  - Be consistent with style and design decisions.
  - Cover your implementation with tests, add it under `test/*-test.js`.

## Change history

To view change history, please visit: [history.md](https://github.com/dgaubert/express-metrics)

Versioning strategy:

  - The major version will increase for any backward-incompatible changes.
  - The minor version will increase for added features.
  - The patch version will increase for bug-fixes.

## License

To view the MIT license, please visit: [The MIT License (MIT)](https://github.com/dgaubert/express-metrics)
