## NOTE
**Although the functionality is sound, the Contract API is still in Beta in undergoing changes as it is finalised.**

### Installation (Gradle)
```compile group: "org.http4k", name: "http4k-contract", version: "X.X.X"```

### About
The `http4k-contract` module adds a much more sophisticated routing mechanism to that available in `http4k-core`. It adds the facility 
to declare server-side `Routes` in a completely typesafe way, leveraging the Lens functionality from the core. These `Routes` are 
combined into `RouteModules`, which have the following features:
* **Auto-validating** - the `Route` contract is automatically validated on each call for required-fields and type conversions, removing the requirement 
for any validation code to be written by the API user. Invalid calls result in a `HTTP 400 (BAD_REQUEST)` response. 
* **Self-describing:** - a generated endpoint is provided which describes all of the `Routes`  in that module. Implementations 
include [Swagger/OpenAPI](http://swagger.io/) documentation, including generation of [JSON schema](http://json-schema.org/) models for messages.
* **Security:** to secure the `Routes`  against unauthorised access. Current implementations include `ApiKey`.

#### 1. Defining a Route
Firstly, create a route with the desired contract of path, headers, queries and body parameters. 

#### 2. Dynamic binding of calls to an HttpHandler
Next, bind this route to a function which creates an `HttpHandler` for each invocation,
which receives the dynamic path elements from the path:

#### 3. Combining Routes into a contract and bind to a context
Finally, there `ServerRoutes` are added into a reusable `Contract` in the standard way, defining a renderer (in this example Swagger) and a security model (in this case an API-Key):

<script src="http://gist-it.appspot.com/https://github.com/http4k/http4k/blob/master/src/test/kotlin/site/Contract_Module/module.kt"></script>

When launched, Swagger format documentation (including JSON schema models) can be found at the route of the module.

For a more extended example, see the following example apps: 
* [Todo backend (typesafe contract version)](https://github.com/http4k/http4k-contract-todo-backend)
* [TDD'd example application](https://github.com/http4k/http4k-contract-example-app)