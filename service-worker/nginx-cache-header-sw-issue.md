# case-studies

I am trying to set cache header for sw with nginx, in the configuration like it has been done in firebase, I tried

```
location /service-worker.js {
    add_header Cache-Control "no-cache";
    proxy_cache_bypass $http_pragma;
    proxy_cache_revalidate on;
    expires off;
    access_log off;
}
```

However when I load my page, sw registration fails with the message.

`A bad HTTP response code (404) was received when fetching the script.
registerServiceWorker.js:71 Error during service worker registration: TypeError: Failed to register a ServiceWorker: A bad HTTP response code (404) was received when fetching the script.`

Asked help cra team, issue filed
https://github.com/facebook/create-react-app/issues/2440

Now CRA is using the serve command to output its build folder. It didnt struck me though, may be we can do something with it.

Thanks to this thread
I found https://github.com/facebookincubator/create-react-app/issues/3516

Jeff gave an option to build it with serve with caching disabled
`serve -s -c 0 build`

Using the above solution led to another problem, which even affected the performance of the project that I was working on.

It didnt just disable caching for  sw, but for every resources, which is a huge problem.

Hence I need to find a solution through nginx with which it is hosted.
