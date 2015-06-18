# throttled

Express.js Middleware to Throttle Requests. Supports clustering using redis.

## Usage

```js
/**
 * Configure the middleware
 *
 * @type    {Function}
 */
var throttled = require('throttled')({

  /**
   * Redis Prefix
   *
   * @type    {String}
   */
  prefix: 'throttled:',

  /**
   * How many requests to limit per period
   *
   * @type    {Number}
   */
  limit: 1000,

  /**
   * How long before the count resets in seconds
   *
   * @type    {Number}
   */
  period: 60 * 15,

  /**
   * How long should someone be banned in seconds if they exceed the limit
   *
   * @type    {Number}
   */
  ban: 15 * 60,

  /**
   * Should we use the console, a custom logger, or nothing at all
   *
   * @type    {Object|Falsey}
   */
  logger: console,

  /**
   * Redis options. Read more about them at
   * https://github.com/mranney/node_redis#rediscreateclient
   *
   * @type    {Object}
   */
  redis: {}
});

/**
 * Can be applied to your entire server
 */
app.use(throttled);

/**
 * Or a specific route
 */
app.get('/rest/resource', throttled, handleGetResource);
```
