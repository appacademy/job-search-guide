# Rest
> **Re**presentational **S**tate **T**ransfer - A set of design principles for making network communication more scalable and flexible

### Fielding Constraints (by Roy Fielding who coined REST)
#### Client-Server 
* The network must be made up of servers (computer that has resources) and clients (computer that interacts with server's resources)

#### Stateless
* Server's and clients do not need to keep track of each other's state
  * When a client is not interacting with the server, the server has no idea of its existence
* The server does **not** keep track of past requests 

#### Uniform Interface 
* There must be a common language between servers and clients
* This allows parts to be swapped without breaking the system
* Sub-constraints: 
  * identification of resources
    * A resource can be: HTML document, image, JSON, etc.
    * The Web used URI (Think URL) to indentify resources (`/pokemon/5`) and HTTP requests.
    * When we type an address, we make an HTTP GET request to that URI
  * manipulation of resources through representations
    * Client sends resource representation (ex., JSON) saying what should change (i.e. change a Poke name)
    * While the client makes the request, the server still has full control over the modifications
  * self-descriptive messages
    * The message contains everything the recipient needs to understand. 
    * Type in "www.google.com"; HTTP request has request type and protocal
    * The server will send back a response, telling client how to interpret the body, and whether or not it was successful
  * hypermedia
    * Data sent from the server that contains information about what the client can do next
    * in REST, servers should _only_ be sending hypermedia to clients
    * HTML is a type of hypermedia
      * `<a href= “http://www.recurse.com”> Check out the Recurse Center! </a>` tells the client that it should make a GET request to http://www.recurse.com if the user clicks on the link.
      * `<img src="awesome-pic.jpg">` tells the client to immediately make a GET request to http://www.example.com/awesome-pic.jpg so it can display the image

* When a system has **identifiers for each resource**, **manipulates them through sending representations** from the client to the server, and has messages that are **self-descriptive** and composed of **hypermedia**, it is said to have a uniform interface.

