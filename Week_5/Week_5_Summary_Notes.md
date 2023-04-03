# Notes 

## Intro to Networking & TCP 
* A computer network is when two or more computers are connected and can communicate with each other 
* How to build a network (Wireless Router)
* LAN - Local Area Network 
  * Your house 
* Network Interface Card [NIC]
  * Acts as the ear and mouth of the computer 
* WAN - Wide Area Network 
  * Office campus 
* Mac Address
  * 6 bytes long or 48 bits 
* Collision Detection/Avoidance 
  * Original days of networking, was detection 
  * Avoidance nowadays - sees if there is a message before it sends its message  
* TCP - Transmission Control Protocol, provides a standard that allows machines to speak to each other 
* TCP based communication allows two machines to establish an open channel for two way data communication 
  * Once established, both parties can start sending and receiving data until one of them decides it's had enough and terminates the connections
  * Specific type of protocol (guideline, standard, agreement) which is commonly used to structure the data and workflow of data over the network  
  * IP Address 
  * Port 

## HTTP 
* HTTP is a request-response protocol, where the client makes requests and the server sends responses
* HTTP is a text based protocol, making it easy to read and understand for humans
* Client wants to communicate with a server it issues a request. Many components... Focusing on these... 
  * Path - What resource the client wants to act on 
    * Path is a part of the URL 
    * Protocol - https/http - set method for exchanging or transferring data around a computer network
    * Domain/Host - www. -> .com
    * Port - technical gate used to access resources, omitted if it uses the standardd http protocol 
    * Resource Path - is the path to the resource on the Web server. Abstraction now!
    * Query Parameters - key/value pairs seperated with the & symbol, can be used to do extra stuff before returning the resource 
    * Anchor - bookmark inside the resource 
  * Method - What action it would like to perform 
    * Get -> get data from the server
    * Post -> create some new data
    * Put -> editing existing data on the server 
    * Delete -> delete existing data  
* After the server has tried to perform the requested action, it sends a response back to the client. 2 IMP Parts: 
  * HTTP Status Codes 
    * 3 digit number to let the client know whether the operation was successful or not 
      * 200 - Great
      * 201 - Succeeded and a new resource has been created as a result 
      * 404 - Not found
      * 500 - Server had an error 
      * 451 - Not available due to legal reasons 
  * Response Body 
    * Data requested 
  * Requests and responses both contain key-value based headers (eg: Accept-Language: fr, Content-Type: text/html, etc.)

## Intro to JSON & APIs
* JSON - stands for JavaScript Object Notation 
  * Built on two structures: 
    * A collection of name/value pairs 
    * An ordered list of values
```javascript 
{
  "name": "New York City",
  "boroughs": [
    "Manhattan",
    "Queens",
    "Brooklyn",
    "The Bronx",
    "Staten Island"],
  "population": 8491079,
  "area_codes": [212, 347, 646, 718, 917, 929],
  "position": { "lat": 40.7127, "lng": -74.0059 }
}
```
  * keys are always double-quoted "strings"
  * values can be numbers, strings, or objects themselves 
  * JSON syntax is and must be valid JS 
* Serialization 
  * Converts objs or data structures into a format that can be stored or transmitted between computers (typically as a string of text)
  * Opposite is called deserialization 
  * JSON.parse()
    * Parse a string as JSON, optionally transform the produced value and its properties, and return the value.
    * returns it to origin, object, ... 
  * JSON.stringify()
    * Return a JSON string corresponding to the specified value, optionally including only certain properties or replacing property values in a user-defined manner.
    * Makes it into a string 
  * JSON Media Type - Can check the Content-Type in the response header by running the following cURL command in terminal 
  ```javascript
  curl -i ipinfo.io
  ```

## What is an API 
* Application Programming Interface - allow systems to work together 
* Set of requirements that govern how one application can talk to another 
* REST API [Representational State Transfer] 
  * Client to Server 
  
## Promises 
* Don't avoid callbacks, simply wrap them in promises
* Promise is an object 
* .then method that you pass a callback in 
* Makes error handling simpler 
* Makes async code easier to test 
* Promise.all can be used to run multiple async operations in parallel and have a single callback to see al the results together 

