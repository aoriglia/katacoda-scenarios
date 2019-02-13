
The previous request gave us the list of the test requests. Choose an element id.

Select *post.js* and copy the following content in this file. Replace **YOUR_ELEMENT_ID** with the element id of your choice.

<pre class="file" data-filename="post.js" data-target="replace">
module.exports = { json : 
    {
      'width': 800,
      'height': 200,
      'title': 'My Awesome Test',
      'rasterType': 'PNG',
      'xAxisLabel': '',
      'yAxisLabel': '',
      'legend': true,
      'multiYAxis': true,
      'theme': 'LIGHT',
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

Select *request.js* and copy the following code in this file:

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
        fs.writeFileSync('graph.png', body);
    } else {
       console.log(body)
    }
})

http.createServer(function(request, response) {
    fs.readFile('graph.png', function(error, data) {  
        if (error) {
            throw error;
        }        
        response.setHeader('Content-type', 'image/png');
        response.end(data);
    });
}).listen(8080);

</pre>



Execute the request:

`node request.js`{{execute}}

Then click on the tab named *Graph* to see the result image.
