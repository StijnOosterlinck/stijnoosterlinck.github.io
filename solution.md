my data is published here: https://stijnoosterlinck.github.io/lab1.ttl

This is the result of 'curl -I https://stijnoosterlinck.github.io/lab1.ttl':


HTTP/2 200 
server: GitHub.com
content-type: text/turtle; charset=utf-8
permissions-policy: interest-cohort=()
last-modified: Sun, 03 Mar 2024 10:13:08 GMT
access-control-allow-origin: *
strict-transport-security: max-age=31556952
etag: "65e44d34-29b"
expires: Sun, 03 Mar 2024 10:29:38 GMT
cache-control: max-age=600
x-proxy-cache: MISS
x-github-request-id: FAE4:3484A2:1501F0A:156AA9D:65E44EB9
accept-ranges: bytes
date: Sun, 03 Mar 2024 10:29:04 GMT
via: 1.1 varnish
age: 565
x-served-by: cache-bru1480053-BRU
x-cache: HIT
x-cache-hits: 1
x-timer: S1709461744.377603,VS0,VE1
vary: Accept-Encoding
x-fastly-request-id: 32c6dde3e62633e9d4adead4fef8db54a432cd6c
content-length: 667



Due to the -I option, the content is not shown. 

- The content type is correctly set to text/turtle. The server uses the vary header to indicate which request headers it used for content negotiation. In this case however, we did not do any negotiation from the client-side.
- Cross origin resource sharing: this is set to 'allow all origins', indicated by the star after 'access-control-allow-origin'. This means that the browser may permit any origins to load resources.
- HTTP/2 is used, indicating a better performance than when HTTP/1 would be used. However, HTTP/3 is not used, but in this case this would not lead to performance gains since my personal website would never have very heavy traffic.
- Cashing is enabled, based on expiration. This can be seen by the cache-control header which has a max-age defined, and the age header which defines the age of the response. The expires header also specifies the lifetime of the cache by using an explicit time. The vary: accept-encoding header indicates that requests will be seen as separate by the server if their accept-encoding header is different. If this header is the same, then the cached result can be used instead. The http object is also assigned a unique etag, which could be used for future content validation.
- The cache that is used is 1.1 varnish. This is a very old version of varnish, so http compression is probably not done. As stated on their website, before 3.0, varnish would never compress objects (https://varnish-cache.org/docs/5.1/users-guide/compression.html).
- In this scenario, only polling is needed since there are very few requests, and this is also not a case in which the maximum acceptable latency is extremely low.
