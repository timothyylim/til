* HTTP ONLY (Secure) cookies cannot be accessed in JavaScript. If you try to read some token, etc from a secure cookie it's not going to work.
* Cross-domain cookies cannot be accessed. In case you are building a single page application and your server is on a different domain. You cannot access the cookies on your SPA. The `withCredentials` flag will just make sure that the network calls made include the cookies and accept any incoming cookies.

https://github.com/axios/axios/issues/295
