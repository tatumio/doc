# Logging

Tatum comes with a built-in logger which can help you debug your application, display errors and warnings from the inner workings of TatumSDK. You can also use it to log your own messages.

Tatum comes with 3 builtin loggers:

* `TatumDevelopmentLogger` - formats messages for easy viewing terminal
* `TatumDevelopmentBrowserLogger` - formats messages for browser console
* `TatumProductionLogger` - avoids formatting where possible, wraps global `console`

You can pick choose which logger you use based on your needs.&#x20;

By default, Tatum will use of the development loggers if you are running in development mode, and `TatumProductionLogger` if you are running in production mode. Of course, you can override this behaviour by passing your own logger to Tatum SDK.

{% code lineNumbers="true" fullWidth="false" %}
```typescript
import { TatumSDK, TatumDevelopmentLogger } from "@tatumio/tatum"

const logger = new TatumDevelopmentLogger()

const tatum = await TatumSDK.init<Ethereum>({
  logger,
  // ...
})
```
{% endcode %}

### Log levels

Tatum supports 5 logging levels in order of severity:

* `TRACE`
* `DEBUG`
* `INFO`
* `WARN`
* `ERROR`

{% hint style="info" %}
By specifying a certain log level, all logs with a lower severity will be ignored
{% endhint %}

You can set the log level by passing `level` to any of our loggers' constructor.

{% code lineNumbers="true" %}
```typescript
import { TatumDevelopmentLogger, LogLevel } from "@tatumio/tatum"

const logger = new TatumDevelopmentLogger({ level: LogLevel.DEBUG })

logger.trace("This is a trace message") // will not be logged
logger.debug("This is a debug message")
logger.error("Ooopsie!")
```
{% endcode %}

### Bring your own logger

You can also use your own logger, as long as it implements the following interface importable from `@tatumio/tatum`:

{% code lineNumbers="true" %}
```typescript
interface Logger {
  trace(...args: any[]): void
  debug(...args: any[]): void
  info(...args: any[]): void
  warn(...args: any[]): void
  error(...args: any[]): void
}
```
{% endcode %}

{% hint style="info" %}
Many popular of-the-shelf loggers such as `pino`, `loglevel` or `log4js` already do so! You can use them without any additional configuration
{% endhint %}

&#x20;Alternatively, you can implement it yourself:

{% code lineNumbers="true" %}
```typescript
const myLogger = {
  trace(...args) {},
  debug(...args) {},
  info(...args) {},
  warn(...args) {},
  error(...args) {},
}

const tatum = await TatumSDK.init<Ethereum>({
  network: Network.ETHEREUM,
  logger: myLogger,
})
```
{% endcode %}

