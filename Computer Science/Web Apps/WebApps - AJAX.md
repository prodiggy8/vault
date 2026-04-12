Asynchronous JavaScript And XML

- Requests can be sent asynchronously
- XMLHttpRequest object
	- Make requests to the web server asynchronously
- Receive server data as XML (or JSON or HTML or text)
- Convert into a DOM tree
- Change the HTML document's DOM tree based on it

- Page is not reloaded, only changes parts of the page
- Requests are asynchronous, user can continue to interact with the page during requests to the server

`onreadystatechange`: event hand;er that gets triggered whenever the readyState of the request changes which allows you to track the progress of an AJAX request. 

`open(method, url, async)`
	`async=false` is deprecated in most browsers
`setRequestHeader(label, value)`
`send(content)`
`readyState`:
	0. unsent
	1. opened
	2. headers rec'd
	3. some data rec'd
	4. response ready
`status`
`responseXML`
`responseText`
