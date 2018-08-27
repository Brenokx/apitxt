FORMAT: X-1A
HOST: https://signpuddle.com/apitxt/

# ApiTxt
> v1.0.0

+ [txt](index.txt) - ApiTxt format
+ [json](index.json) - array of JSON objects
+ [md](index.md) - API Blueprint
+ [html](index.html) - HTML documentation


ApiTxt defines a highly structured plain text format used to define multiple facets of a website api.
Each line in an ApiTxt document is a self-contained element which starts with a name and is followed by &lt;TAB> separated fields.
Writing ApiTxt documents is easier when tabs and spaces appear different, so use a plain text editor and turn on the invisible characters option.

## Input and Output Formats
The various formats are used to define the structure and function of a website API.
The original source is written in ApiTxt format and transformed into an array of JSON objects.
The JSON objects are used to write other formats, including API Blueprint.

### ApiTxt Format (txt)
ApiTxt format uses plain text divided into multiple lines, where each line contains &lt;TAB> delimited fields.
Writing ApiTxt documents is easier when tabs and spaces appear different, so use a plain text editor and turn on the invisible characters option.

### Array of JSON Objects (json)
Each line of ApiTxt format is converted into a JSON object or added to an existing object.  The various objects are stored in an ordered array.

### API Blueprint (md)
[API Blueprint](https://apiblueprint.org/) is a high-level API description language for web APIs. API Blueprint is widely supported with various tooling available.

#### HTML Documentaion (html)
The HTML documentation is generated from the API Blueprint document using the project [bukalapak/snowboard](https://github.com/bukalapak/snowboard/), written in golang.

#### PHP Server (php)
The PHP server is written for the PHP project [Slim Framework v2](https://docs.slimframework.com/) to create the functional web API.
The website directory contains an .htaccess file for an Apache server with PHP support.
Alternatively, the server can be started with a shell script (start_server.sh) using PHP's built in web server and a custom rewrite.php file.

## Transformations
Python programs and shell scripts are used to read and write a variety of data formats including plain text, JSON data, API Blueprint, HTML and PHP scripts.

### Plain Text to JSON Objects (txt2json)
The primary transformation is from the plain text format to an array of JSON objects.

### JSON Objects back to Plain Text (json2txt)
The transformation can be reversed, resulting in a document that is properly structured with standardized indenting.

### JSON Objects to API Blueprint (json2md)
The API Blueprint document is created from an array of JSON objects.
Each object is written as a section of the API Blueprint document using a markdown syntax.

### JSON Objects to PHP Server (json2php)
A functional PHP server is built from the JSON objects for the Slim Framework v2.
The server responses can be based on prewritten responses or functional PHP code using URL parameters and query parameters.

### Plain Text to Tested Mock Servers (txt2mock)
This script calls the previous scripts to create, check, and build the various website API documents.
Multiple calls to [bukalapak/snowboard](https://github.com/bukalapak/snowboard/) are used to check the validity of the API Blueprint, to create the HTML documentation, and to create a mock server.


## Index [/]

The index page contains information about the web API and the routes available.

### Get the index page [GET]

+ Response 200 (text/plain)


     + Body

            The website includes various routes:
            * /root
            * /group
            * /route
            * /parameter
            * /method
            * /request
            * /response
            * /header
            * /line
            * /code

## Group elements
ApiTxt uses ten types of element to define an API.

root, group, route, parameter, method, request, response, header, line, and code.


### root [/root]

Every document should start with a root element.
After the root, the other elements are used to quickly create complex website APIs.
The order of the lines matters and will effect the structure of the JSON objects.

There are two groups of elements, the frame elements and the detail elements.
The frame elements structure a website api and the detail elements attach to a previous frame element.

### Frame elements
There are six frame elements: root, group, route, method, request, and response.
The lines are written in a specific order to create an array of JSON objects.

**route organization**

An ApiTxt document starts with a root, or an assumed root.
Any route that occur before a group element, will be associated with the root.
Groups are always associated with the root.
Group elements can contain routes.

```
    root
      | - routes
      | - groups
            | - routes
```

**route structure**

A route can be associated with a variety of HTTP methods.
Each method can have several requests and responses.
Any response before a request will assume a generic request.
Any response after a request will be associated with that request.
```
    route
      | - methods
        | - responses
        | - requests
              | - responses
```
## Detail elements
There are four detail elements: line, code, parameter, and header.  The detail lines attach to a previous frame element if correctly structured.

**single line elements**
```
    lines for all frame elements

    parameters for route

    codes for method

    headers for request and response
```


#### Get root definition [GET]
Every document should start with a root element.

**root line**

root &lt;TAB> name &lt;TAB> title &lt;TAB> host

+ field 1 - name - uniquely identifies a document
+ field 2 - title - name of the document
+ field 3 - host - website URL

**root example**

root &lt;TAB> apitxt &lt;TAB> ApiTxt &lt;TAB> https://signpuddle.com/apitxt


**root line relationships**
```
    root
     | - lines
     | - routes
     | - groups
```

**root object**
```json
{"root":
  "root" : field[1],
  "title" : field[2],
  "host" : field[3],
  "lines" : []
}
```

+ Request the root definition

     + Body

            null

+ Response 200 (text/plain)


     + Body

            Every document should start with a root element.
            
            **root line**
            
            root   name   title   host
            
            + field 1 - name - uniquely identifies a document
            + field 2 - title - name of the document
            + field 3 - host - website URL
            
            **example**
            
            root   apitxt   ApiTxt   https://signpuddle.com/apitxt
            
            
            **root line relationships**
            ```
                root
                 | - lines
                 | - routes
                 | - groups
            ```
            
            **root object**
            ```json
            {"root":
              "root" : field[1],
              "title" : field[2],
              "host" : field[3],
              "lines" : []
            }
            ```

### group [/group]

#### Get group definition [GET]
The group organizes resources into sections

**group line**

group &lt;TAB> name &lt;TAB> description

+ field 1 - name - the short name used for sections
+ field 2 - description - information about the group

**group example**

group &lt;TAB> Section name &lt;TAB> an example section

**group line relationships**
```
    group
     | - lines
     | - routes
```

**group object**
```json
{"group":
  "group" : field[1],
  "description" : field[2],
  "lines": []
}
```

+ Request the group definition

     + Body

            null

+ Response 200 (text/plain)


     + Body

            The group organizes resources into sections
            
            **group line**
            
            group   name   description
            
            + field 1 - name - the short name used for sections
            + field 2 - description - information about the group
            
            **group example**
            
            group   Section name   an example section
            
            **group line relationships**
            ```
                group
                 | - lines
                 | - routes
            ```
            
            **group object**
            ```json
            {"group":
              "group" : field[1],
              "description" : field[2],
              "lines": []
            }
            ```

### route [/route]

#### Get route definition [GET]
The route element allows access to a resource

**route line**

route &lt;TAB> URI template &lt;TAB> name &lt;TAB> description

+ field 1 - URI template - a resource pattern with parameters
+ field 2 - name - the route name must be unique
+ field 3 - description - information about the resource

**route example**

route &lt;TAB> /example &lt;TAB> an example route &lt;TAB> a description of the route

**route line relationships**
```
    route
     | - lines
     | - parameters
     | - methods
```

**route object**
```json
{"route":
  "route" : field[1],
  "name" : field[2],
  "description" : field[3],
  "lines": [],
  "parameters": []
}
```

+ Request the route definition

     + Body

            null

+ Response 200 (text/plain)


     + Body

            The route element allows access to a resource
            
            **route line**
            
            route   URI template   name   description
            
            + field 1 - URI template - a resource pattern with parameters
            + field 2 - name - the route name must be unique
            + field 3 - description - information about the resource
            
            **route example**
            
            route   /example   an example route   a description of the route
            
            **route line relationships**
            ```
                route
                 | - lines
                 | - parameters
                 | - methods
            ```
            
            **route object**
            ```json
            {"route":
              "route" : field[1],
              "name" : field[2],
              "description" : field[3],
              "lines": [],
              "parameters": []
            }
            ```

### parameter [/parameter]

#### Get parameter definition [GET]
The parameter element is applied to the previous route

**parameter line**

parameter &lt;TAB> name &lt;TAB> example &lt;TAB> type &lt;TAB> description

+ field 1 - name - the name of a parameter for a route
+ field 2 - example - an example value for the parameter
+ field 3 - type - the parameter type, such as "string", "number", "string, optional", "string, required"
+ field 4 - description - information about the parameter

**parameter example**

parameter &lt;TAB> country_code &lt;TAB> US &lt;TAB> string &lt;TAB> the country code of interest

**parameter line relationships**

parameter lines are added to a parameters array

**parameters array**
```json
{"parameters":
  [
    {
      "name" : " field[1],
      "example" : field[2],
      "type" : field[3],
      "description" : field[4]
    }
  ]
}
```

+ Request the parameter definition

     + Body

            null

+ Response 200 (text/plain)


     + Body

            The parameter element is applied to the previous route
            
            **parameter line**
            
            parameter   name   example   type   description
            
            + field 1 - name - the name of a parameter for a route
            + field 2 - example - an example value for the parameter
            + field 3 - type - the parameter type, such as "string", "number", "string, optional", "string, required"
            + field 4 - description - information about the parameter
            
            **parameter example**
            
            parameter   country_code   US   string   the country code of interest
            
            **parameter line relationships**
            
            parameter lines are added to a parameters array
            
            **parameters array**
            ```json
            {"parameters":
              [
                {
                  "name" : " field[1],
                  "example" : field[2],
                  "type" : field[3],
                  "description" : field[4]
                }
              ]
            }
            ```

### method [/method]

#### Get method definition [GET]
The method element represents an action that can be performed on a route

**method line**

method &lt;TAB> HTTP method &lt;TAB> name &lt;TAB> description

+ field 1 - HTTP method - the type of action to perform: GET, POST, PUT, DELETE
+ field 2 - name - the name of the action
+ field 3 - description - information about the method

**method example**

method &lt;TAB> GET &lt;TAB> Get an example &lt;TAB> This method retrieves an example document

**method line relationships**
```
    method
     | - lines
     | - codes
     | - requests
     | - responses
```


**method object**
```json
{
  "method" : field[1],
  "name" : field[2],
  "description" : field[3],
  "lines" : [],
  "codes" : [],
  "dialog" : [
    {
      "request" : {},
      "responses" : []
    }
  ]
}
```

+ Request the method definition

     + Body

            null

+ Response 200 (text/plain)


     + Body

            The method element represents an action that can be performed on a route
            
            **method line**
            
            method   HTTP method   name   description
            
            + field 1 - HTTP method - the type of action to perform: GET, POST, PUT, DELETE
            + field 2 - name - the name of the action
            + field 3 - description - information about the method
            
            **method example**
            
            method   GET   Get an example   This method retrieves an example document
            
            **method line relationships**
            ```
                method
                 | - lines
                 | - codes
                 | - requests
                 | - responses
            ```
            
            
            **method object**
            ```json
            {
              "method" : field[1],
              "name" : field[2],
              "description" : field[3],
              "lines" : [],
              "codes" : [],
              "dialog" : [
                {
                  "request" : {},
                  "responses" : []
                }
              ]
            }
            ```

### request [/request]

#### Get request definition [GET]
The request element is associated with a specific method and can be paired with multiple responses.

**request line**

request &lt;TAB> name &lt;TAB> type

+ field 1 - name - uniquely identifies a request
+ field 2 - type - the content type of the request body

**request example**

request &lt;TAB> matching text within request body &lt;TAB> plain/text

**request line relationships**
```
    request
     | - headers
     | - lines
```

**request object**
```json
{
  "name" : field[1],
  "type" : field[2],
  "headers" : {},
  "lines" : []
}
```

+ Request the request definition

     + Body

            null

+ Response 200 (text/plain)


     + Body

            The request element is associated with a specific method and can be paired with multiple responses.
            
            **request line**
            
            request   name   type
            
            + field 1 - name - uniquely identifies a request
            + field 2 - type - the content type of the request body
            
            **request example**
            
            request   matching text within request body   plain/text
            
            **request line relationships**
            ```
                request
                 | - headers
                 | - lines
            ```
            
            **request object**
            ```json
            {
              "name" : field[1],
              "type" : field[2],
              "headers" : {},
              "lines" : []
            }
            ```
            

### response [/response]

#### Get response definition [GET]
The response element is associated with a specific request, or associated with a specific method with an assumed generic request.

**response line**

response &lt;TAB> status &lt;TAB> type

+ field 1 - status - an HTTP response code indicating the status of the request
+ field 2 - type - the content type of the response body

**response example**

response &lt;TAB> 200 &lt;TAB> plain/text

**response line relationships**
```
    response
     | - headers
     | - lines
```

**response object**
```json
{
  "status" : field[1],
  "type" : field[2],
  "headers" : {},
  "lines" : []
}
```

+ Request the response definition

     + Body

            null

+ Response 200 (text/plain)


     + Body

            The response element is associated with a specific request, or associated with a specific method with an assumed generic request.
            
            **response line**
            
            response   status   type
            
            + field 1 - status - an HTTP response code indicating the status of the request
            + field 2 - type - the content type of the response body
            
            **response example**
            
            response   200   plain/text
            
            **response line relationships**
            ```
                response
                 | - headers
                 | - lines
            ```
            
            **response object**
            ```json
            {
              "status" : field[1],
              "type" : field[2],
              "headers" : {},
              "lines" : []
            }
            ```
            

### header [/header]

#### Get header definition [GET]
The header element is applied to a preceding route

**header line**

header &lt;TAB> name &lt;TAB> value

+ field 1 - name - the header variable name
+ field 2 - value - the header variable value

**header example**

header &lt;TAB> X-Powered-By &lt;TAB> ApiTxt

**header object**
```json
{ field[1] : field[2] }
```

+ Request the header definition

     + Body

            null

+ Response 200 (text/plain)


     + Body

            The header element is applied to a preceding route
            
            **header line**
            
            header   name   value
            
            + field 1 - name - the header variable name
            + field 2 - value - the header variable value
            
            **header example**
            
            header   X-Powered-By   ApiTxt
            
            **header object**
            ```json
            { field[1] : field[2] }
            ```

### line [/line]

#### Get line definition [GET]
The line element adds additional text to frame elements.

For the root, group, route, and method, the lines add details to an element.  For the request and response elements, the line represents the body of the request or response.

The text of the line is everything after the string "line &lt;TAB>".

+ Request the line definition

     + Body

            null

+ Response 200 (text/plain)


     + Body

            The line element adds additional text to frame elements.
            
            For the root, group, route, and method, the lines add details to an element.  For the request and response elements, the line represents the body of the request or response.
            
            The text of the line is everything after the string "line <TAB>".

### code [/code]

#### Get code definition [GET]
The code element adds functionality to the method element.

The code element contains programming text.  ApiTxt comes integrated with the PHP project the Slim Framework v2.  The conversion to working PHP adds boilerplate details for routes and method, with named parameters and query parameters available as functional variables.

The text of the code is everything after the string "code &lt;TAB>".

+ Request the code definition

     + Body

            null

+ Response 200 (text/plain)


     + Body

            The code element adds functionality to the method element.
            
            The code element contains programming text.  ApiTxt comes integrated with the PHP project the Slim Framework v2.  The conversion to working PHP adds boilerplate details for routes and method, with named parameters and query parameters available as functional variables.
            
            The text of the code is everything after the string "code <TAB>".
