---
layout: post
title: Serverless - AWS Lambda
date: 2019-08-01 23:36 +0000
---

## Handler

### Node.js

```javascript
exports.handler =  async function(event, context) {
  console.log("EVENT: \n" + JSON.stringify(event, null, 2))
  return context.logStreamName
}
```

### Python

```python
def handler_name(event, context): 
    # 
    return some_value
```

```python
def my_handler(event, context):
    message = 'Hello {} {}!'.format(event['first_name'], 
                                    event['last_name'])  
    return { 
        'message' : message
    }  
```

### Go

```golang
package main

import (
        "fmt"
        "context"
        "github.com/aws/aws-lambda-go/lambda"
)

type MyEvent struct {
        Name string `json:"name"`
}

func HandleRequest(ctx context.Context, name MyEvent) (string, error) {
        return fmt.Sprintf("Hello %s!", name.Name ), nil
}

func main() {
        lambda.Start(HandleRequest)
}
```

### C#
```java
returnType handler-name(inputType input, ILambdaContext context) {
   ...
}

```

```java
using System.IO;

namespace Example
{            
  public class Hello
  {
    public Stream MyHandler(Stream stream)
    {
       //function logic
    }
}
```


### Java
```java
package example;

import com.amazonaws.services.lambda.runtime.RequestHandler;
import com.amazonaws.services.lambda.runtime.Context; 

public class Hello implements RequestHandler<Request, Response> {
    
    public Response handleRequest(Request request, Context context) {
        String greetingString = String.format("Hello %s %s.", request.firstName, request.lastName);
        return new Response(greetingString);
    }
}
```

---