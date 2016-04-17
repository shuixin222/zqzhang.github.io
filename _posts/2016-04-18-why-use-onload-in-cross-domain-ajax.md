---
layout: post
type: post
title: Why Use onload in Cross-domain Ajax
---

## `XMLHttpRequest.onreadystatechange`

Generally the `XMLHttpRequest.onreadystatechange` property is used in an Ajax
request.

```js
var xhr = new XMLHttpRequest(),
xhr.open("GET", "http://zqzhang.github.io", true);
xhr.onreadystatechange = function () {
    if(xhr.readyState === xhr.DONE && xhr.status === 200) {
      console.log(xhr.responseText);
    }
  };
xhr.send();
```

## `XMLHttpRequest.onload`

The `XMLHttpRequest.onload` event handler, however, is suggested to be used in
cross-domain Ajax with Cross-Origin Resource Sharing (CORS) instead of the
`onreadystatechange` event handler.

```js
var xhr = new XMLHttpRequest();
xhr.open("GET", "http://zqzhang.github.io:8080", true);
xhr.onload = function(){  // instead of onreadystatechange
    // do something
  };
xhr.send(null);
```

Why?

## Is `onload` equal to `readyState==4` in XMLHttpRequest?

Stackoverflow records this question and answers
[here](http://stackoverflow.com/questions/9181090/is-onload-equal-to-readystate-4-in-xmlhttprequest).
Copy the most accepted answer here:

> This is _almost_ always true. One significant difference, however, is that the
> `onreadystatechange` event handler also gets triggered with `readyState==4`
> in the cases where the `onerror` handler is usually triggered (typically a
> network connectivity issue). It gets a status of 0 in this case. I've verified
> this happens on the latest Chrome, Firefox and IE.

> So if you are using `onerror` and are targeting modern browsers, you should
> not use `onreadystatechange` but should use `onload` instead, which seems to
> be guaranteed to only be called when the HTTP request has successfully
> completed (with a real response and status code). Otherwise you may end up
> getting two event handlers triggered in case of errors (which is how I
> empirically found out about this special case.)

## Reference

* Nicholas C. Zakas. [Cross-domain Ajax with Cross-Origin Resource
  Sharing](https://www.nczonline.net/blog/2010/05/25/cross-domain-ajax-with-cross-origin-resource-sharing/)
* Arun Ranganathan. [cross-site xmlhttprequest with
  CORS](https://hacks.mozilla.org/2009/07/cross-site-xmlhttprequest-with-cors/)
* Eric Bidelman. [New Tricks in
  XMLHttpRequest2](http://docs.webplatform.org/wiki/tutorials/file_xhr)
* Monsur Hossain. [Using CORS](http://www.html5rocks.com/en/tutorials/cors/)
