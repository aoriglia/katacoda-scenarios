
The previous request gave us a list of tests.

Select *vars.js* and copy the following content in this file. Replace **YOUR_TEST_ID_HERE** with one of test id of your choice.

<pre class="file" data-filename="vars.js" data-target="replace">
module.exports = { test_id : 'YOUR_TEST_ID_HERE' };
</pre>

Let's request the elements of type REQUEST from this test.
Select *request.js* and copy the following code in this file:

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
