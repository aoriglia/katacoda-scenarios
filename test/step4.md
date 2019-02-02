
The previous request gave us the list of the test requests. Choose an element id.

Copy the following content in the file *post.js* and replace **YOUR_ELEMENT_ID** the with one of your choice.

<pre class="file" data-filename="post.js" data-target="replace">
module.exports = { json : 
    {
      'width': 600,
      'height': 200,
      'title': 'My Awesome Test',
      'rasterType': 'PNG',
      'xAxisLabel': '',
      'yAxisLabel': '',
      'legend': true,
      'multiYAxis': true,
      'theme': 'TRANSPARENT',
      'elementIds': [
        {
          'id': 'YOUR_ELEMENT_ID',
          'statistics': [
            'AVG_DURATION'
          ]
        }
      ]
    }
};
</pre>

Let's choose an element and try to get its specific average duration as a PNG image.

Copy the following code in the file *request.js*:

<pre class="file" data-filename="request.js" data-target="replace">var request = require('request');
var fs   = require('fs');
var http = require('http');

var auth = require('./auth');
var vars = require('./vars');
var post = require('./post');

// Set the headers
var headers = {
    'User-Agent':       'Super Agent/0.0.1',
    'Content-Type':     'application/json',
    'accept':           'image/png',
    'accountToken':     auth.access_token
} 

// Configure the request
var options = {
    url: 'https://preprod-neoload-api.saas.neotys.com/v1/tests/' + vars.test_id + '/graph',
    method: 'POST',
    body: JSON.stringify(post.json),
    headers: headers,
    encoding: null
}

// Execute the request
request(options, function (error, response, body) {
    if (!error && response.statusCode == 200) {
        fs.writeFileSync('images/graph.png', body);
    } else {
       console.log(body)
    }
})

http.createServer(function(request, response) {
    fs.readFile('images/graph.png', function(err, data) {  
        if (err) throw err;
        response.setHeader('Content-type', 'image/png');
        response.end(data);
    });
}.listen(8080);

</pre>



Execute the request:

`node request.js`{{execute}}
