## Best Practices for writing Code Services/Libraries
Follow these practices in order to have clean, working and scalable code on ClearBlade Platform.

* Place global constants in a Constants/Configuration library.
    Ex: `TwilioConstants.js`
    ```javascript
    /** TODO Create an account on twilio.com, and enter account credentials below
    *  ex. USER: "BC218b72987d86855a5adb921370115a20"
    *  ex. PASS: "4579ac6ba4fae7b452c03c64aeae40e7"
    *  ex. SOURCE_NUMBER: "(+1 512-713-2913)"
    **/
    const TWILIO_CONFIG = {
        USER : "",
        PASS : "",
        SOURCE_NUMBER : ""
    }
    ```
* Avoid using globals, instead prefer using local variables in a function(). This simplifies coding when using complex systems where multiple libraries are being imported. 

* If adding debugging logic, use a debug object with this format to minimize impact on production execution path:

```javascript
var DEBUG = {
    enabled:false,
    payload:{
    "param1": "key1",
    ...
    "paramn": "keyn"
  }
}
function submitBodyMeasurement(req, resp){
    log(req)
    if(DEBUG.enabled){
        req.params = DEBUG.payload
    }
    ...
}
```

* Prefer using constants instead of using 'strings' directly.
Option 1: Declare Constant at the beginning of the service.
```javascript
    function serviceName(req, resp){
        const DEVICES_COLLECTION = "devices_metadata";
        // ... rest of the code 
    }
```
Option 2: Declare constants in a library.
```javascript
// In a library SystemConstants
function SystemContants(){
    const SC = {
        "collections":{
            "DeviceMetadata":"devices_metadata",
            "GatewaysData":"gateways_data"
        }
    }
    return SC;
}

// In a codeservice ServiceName which imports SystemConstants library
function ServiceName(req, resp){
    const SC = SystemContants();
    ClearBlade.init({request:req});

    var query = ClearBlade.Query({
        collectionsName : SC.collections.DevicesMetadata
        });
}
```

* Avoid writing code after resp.success() or resp.error(). The code service exits when resp.success or resp.error methods are called.
```javascript
function ServiceName(req, resp){
    resp.success("Nothing Executes after me");
    log("You won't see me, because I was never executed..")
}
```

* It is always advisible to write the resp.success or error inside of the callback. 
```javascript

// Bad Practice..
function ServiceName(req, resp){
    var http = Requests();
    const options = {
        "uri":"https://api.ipify.org?format=json"
    }

    var result, failed = false;
    http.get(options, function(err, data){
        if(err){
            failed = true;
        }
        else{
            result = data;
        }
    });
    // The code below might get executed even before the response's recieved 
    if(failed){
        resp.error("failed");
    }
    resp.success(result);
}

// Good
function ServiceName(req, resp){
    var http = Requests();
    const options = {
        "uri":"https://api.ipify.org?format=json"
    }
    http.get(options, function(err, data){
        if(err){
            resp.error(err);
        }
        else{
            resp.success(data);
        }
    });
}
```
