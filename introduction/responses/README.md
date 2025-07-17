# Responses

### Overview

The Prop-AI API uses conventional HTTP response codes to indicate the success or failure of API requests. In general, codes in the `2xx` range indicate success, codes in the `4xx` range indicate an error that failed given the information provided (e.g., invalid location, missing property parameters), and codes in the `5xx` range indicate an error with Prop-AI's servers (these are rare).

When working with Dubai and Middle East property metrics, you'll most commonly encounter `200` for correct locations, `404` when requesting non-existent locations, and `429` when exceeding rate limits.

<table><thead><tr><th width="84">Code</th><th width="141">Status</th><th>Description</th></tr></thead><tbody><tr><td>200</td><td>OK</td><td>Data retrieved successfully.</td></tr><tr><td>400</td><td>Bad Request</td><td>The request was unacceptable, often due to missing a required parameter (e.g., location, property_type).</td></tr><tr><td>401</td><td>Unauthorized</td><td>No valid API key provided or API key expired.</td></tr><tr><td>402</td><td>Request Failed</td><td>The parameters were valid but the request failed (e.g., request timeout).</td></tr><tr><td>403</td><td>Forbidden</td><td>The API key doesn't have permissions to access this property data or market analysis.</td></tr><tr><td>404</td><td>Not Found</td><td>The requested property or market data doesn't exist in our Dubai/Middle East database.</td></tr><tr><td>409</td><td>Conflict</td><td>The request conflicts with another request (perhaps due to using the same idempotent key for property analysis).</td></tr><tr><td>424</td><td>External Dependency failed</td><td>The request couldn't be completed due to a failure in external property data sources or market APIs.</td></tr><tr><td>429</td><td>Too Many Requests</td><td>Too many requests hit the API too quickly. We recommend an exponential backoff of your requests.</td></tr><tr><td>500*</td><td>Server Errors</td><td>Something went wrong on Prop-AI's end. (These are rare.)</td></tr></tbody></table>

***

> **💡 Hint:** When building property search applications, always handle `404` errors gracefully since property listings change frequently in Dubai's dynamic market. For `429` rate limit errors, implement exponential backoff starting with a 1-second delay to ensure smooth user experience during peak property search times.
