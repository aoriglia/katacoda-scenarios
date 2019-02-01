
The request gives us a list of tests.

Copy the following content in the file *testid.js* and replace the test id with one of your choice.

<pre class="file" data-filename="vars.js" data-target="replace">
module.exports = { test_id : 'YOUR_TEST_ID_HERE' };
</pre>

Let's request the elements of type REQUEST from this test.
Copy the following code in the file *request.js*:

<pre class="file" data-filename="request.js" data-target="replace">var request = require('request');

var auth = require('./auth');
var vars = require('./vars');

// Set the headers
var headers = {
    'User-Agent':       'Super Agent/0.0.1',
    'Content-Type':     'application/json',
    'accept':           'image/png',
    'accountToken':     auth.access_token
}

// Configure the request
var options = {
    url: 'https://preprod-neoload-api.saas.neotys.com/v1/tests/' + vars.test_id + '/elements?category=REQUEST',
    method: 'GET',
    headers: headers
}

// Execute the request
request(options, function (error, response, body) {
   console.log(body)
})
</pre>

Execute the request:

`node request.js`{{execute}}
