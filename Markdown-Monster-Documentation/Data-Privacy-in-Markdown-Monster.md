By default Markdown Monster tracks anonymous launch and shutdown telemetry, as well as logging all errors and warnings in the application. The data logged is anonymous and not user identifiable and all telemetry can be disabled via a configuration switch.

### What Markdown Monster logs
Markdown Monster logs the following operations:

* Usage telemetry at application shutdown
* Error reports

#### Usage Telemetry of Startup and Shutdown
Startup and shutdown information is used in Markdown Monster to provide information on usage trends. We don't log specific operations in the application. Only a single operation is sent to the logging server when the application is closed down.
  
The telemetry information sent includes:

* Launch and Shutdown time
* Markdown Monster Version
* Markdown Monster usage count (on this instance)
* Registration status
* .NET Version
* Windows Version

#### Error Logging
Markdown Monster logs all fatal errors as well as a number of 'soft' warnings when both hard unhandled failures occur, as well as a few known and handled error operations.

The error information logs all the same information as the basic telemetry information plus full exception information including a full stack trace.


### Anonymous Data Storage
The data recorded both for usage telemetry and error logging is not explicitly logging any individually traceable data and doesn't include user identifiable information. With the exception of potential errors that might contain local machine information the data is completely void of any user identifiable information.  

> Error information in exceptions may reveal file locations for I/O errors. We don't use this information, but it comes as part of the exception information for certain errors.

### How we use this data and how long it is held
We use both the telemetry data and error log for basic usage statistics and for discovering repeating bugs in the software. Reports are run for the last 3 days' worth of data and are only used for online review and error triage.

The telemetry uses [Microsoft's Application Insights](https://docs.microsoft.com/en-us/azure/azure-monitor/app/app-insights-overview) Analytics service for recording and storing the telemetry and error data which stores the data on Microsoft Azure servers. This service stores data for 3 months on Azure servers, although we only access a few days' worth of that data at any time for our online usage and error reports. Any data older than 3 days is never accessed by our reporting operations.

### Disabling Telemetry and Error Reporting
The telemetry and error reporting described above provides us with very useful anonymous usage statics. The error reporting in particular has been invaluable in helping make Markdown Monster a better application by identifying application problems and bugs early and fixing them quickly.

> We hope you'll leave telemetry enabled - it helps us make Markdown Monster better!

But we understand you might want to turn off any data telemetry for privacy concerns, and you can do this easily in Markdown Monster via a simple configuration switch in Markdown Monster's settings. 

By default telemetry is enabled.

All telemetry can be disabled in Markdown Monster by:

* Going to **Tools -> Settings** from the menu
* Checking  `Send Telemetry` checkbox 

or by:

* Opening the `MarkdownMonster.json` configuration file
* Setting `SendTelemetry=false`