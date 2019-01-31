`npm init --yes`{{execute}}
`npm install request --save`{{execute}}

the app.js file:

<pre class="file" data-filename="app.js" data-target="replace">var request = require('request');

// Set the headers
var headers = {
    'User-Agent':       'Super Agent/0.0.1',
    'Content-Type':     'application/json',
    'accept': 'image/png',
    'accountToken': ''
}

// Configure the request
var options = {
    url: 'https://preprod-neoload-api.saas.neotys.com/v1/tests/cc43cf5c-2d3a-456d-b441-43caa9530269/statistics',
    method: 'GET',
    headers: headers
}

// Start the request
request(options, function (error, response, body) {
    if (!error && response.statusCode == 200) {
        // Print out the response body
        console.log(body)
    }
})
</pre>
