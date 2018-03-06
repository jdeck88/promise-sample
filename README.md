# promise-sample
A sample of using promises in javascript.  Promise with parameters example. Here we go request some data and wait for it to finish:

```
// Create a request object
var request = require('request');

// Define a function called fetchAgency which then returns a promise
// that is filled with data when it is resolved
var fetchAgency = function(agency_type, agency_name) {
    return new Promise(function(resolve,reject) {
        // The base URL to call.  This includes everything except our POST params
        var url = "http://www.mapcollaborator.org/cpad/search/by_agency" 
        // The headers to send in our request
        var headers = { 'Content-Type': 'application/x-www-form-urlencoded'};
        // Here are the POST parameters
        var formData = 'agency_type='+agency_type +'&agency_name='+agency_name;

        // Make the request and the callback is a function with
        // error (1st param) =  error message, if applicable
        // response (2nd param) = all of the metadata about the response itself.  lengthy
        // data (3rd param) = just the JSON data that is returned
        request.post({
            headers: headers,
            url: url,
            method: "POST",
            form: formData 
        }, function (error, response, data){
            resolve(data);
        });
    });
}

// Call our function which returns a promise
fetchAgency('State','University+of+California').then(function(data) {
        // Do something with the data
        console.log(data)
})
```
