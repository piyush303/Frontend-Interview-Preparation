## Interceptors
* Interceptors are like middleware that allows commo patterns around retrying, caching, logging, and authentication to be abstracted away from individual requests.
* Interceptors are general function which processes the request or response .
* Some common patterns where we can use interceptors are given below.
  <ol></ol>
  1. Adding authentication header to outgoing request. <br/>
  2. Retry if any request is failed. <br/>
  3. Cache the response for a defined time. <br/>
  4. Showing loader whenever network request is in progress. <br/>
  5. Regularly polling the server and refreshing results. <br/>

### Define an interceptor
**Example**

```js
export function loggingInterceptor(req: HttpRequest<unknown>, next: HttpHandlerFn): Observable<HttpEvent<unknown>> {
  console.log(req.url);
  return next(req);
}
```
* Interceptor is basic function which accepts outgoing http request and next function which represents the next step in interceptors chain.
* E.g. aboove interceptor example will log request url before forwarding request.

### Configure interceptors
```js
bootstrapApplication(AppComponent, {providers: [
  provideHttpClient(
    withInterceptors([loggingInterceptor, cachingInterceptor]),
  )
]});
```
* Above configured interceptors are chained in the order that you've listed them in the providers.
* E.g. loggingInterceptor would process the request and then forward it to the cachingInterceptor.

Below is an example of how to intercept request and add Authetication token in http request.
```js
export function authInterceptor(req: HttpRequest<unknown>, next: HttpHandlerFn) {

  // Inject the current `AuthService` and use it to get an authentication token:
  const authToken = inject(AuthService).getAuthToken();

  // Clone the request to add the authentication header.
  const newReq = req.clone({headers: {
    req.headers.append('X-Authentication-Token', authToken),
  }});

  return next(newReq);
}
```
