
Here is the app file which contains the request to the API. Copy/Paste the following content in the app.js file.

<pre class="file" data-filename="app.js" data-target="replace">var request = require('request');

var auth = require('./auth');

// Set the headers
var headers = {
    'User-Agent':       'Super Agent/0.0.1',
    'Content-Type':     'application/json',
    'accept':           'image/png',
    'accountToken':     auth.access_token
}

// Configure the request
var options = {
    url: 'https://preprod-neoload-api.saas.neotys.com/v1/tests/' + auth.test_id + '/statistics',
    method: 'GET',
    headers: headers
}

// Execute the request
request(options, function (error, response, body) {
   console.log(body)
})
</pre>

Do not forget to set your own access token and test id.

*The default test id is the identifier of the first test of the samples auto-generated on a brand new account.*
