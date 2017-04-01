There are some limits on the number of metrics and events per application (that is, per instrumentation key). 

Limits depend on the [pricing tier](https://www.azure.cn/pricing/details/application-insights/) that you choose.

**Resource** | **Default Limit** | **Maximum Limit**
-------- | ------------- | -------------
Session data points<sup>1, 2</sup> per month | unlimited | 
Total data points per month for request, event, dependency, trace, exception, and page view | 5 million | 50 million<sup>3</sup>
[Trace and Log](/documentation/articles/app-insights-search-diagnostic-logs) data rate | 200 dp/s | 500 dp/s
[Exception](/documentation/articles/app-insights-asp-net-exceptions) data rate | 50 dp/s | 50 dp/s
Total data rate for request, event, dependency, and page view telemetry | 200 dp/s | 500 dp/s
[Raw data](/documentation/articles/app-insights-diagnostic-search) retention | 7 days
[Aggregated data](/documentation/articles/app-insights-metrics-explorer) retention | 90 days
[Property](/documentation/articles/app-insights-api-custom-events-metrics#properties) name count | 100 |
Property name length | 150 | 
Property value length | 8192 | 
Trace and Exception message length | 10000 |
[Metric](/documentation/articles/app-insights-api-custom-events-metrics#properties/) name count | 100 |
Metric name length |  150 | 
[Availability tests](/documentation/articles/app-insights-monitor-web-app-availability/) | 10 | 

<sup>1</sup> A data point is an individual metric value or event, with attached properties and measurements.

<sup>2</sup> A session data point logs the start or end of a session, and logs user identity.

<sup>3</sup> You can purchase additional capacity beyond 50 million.

[About pricing and quotas in Application Insights](/documentation/articles/app-insights-pricing)