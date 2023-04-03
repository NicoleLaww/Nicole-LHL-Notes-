# Notes 

## cURL 
* cURL is a command line utility that is used to make HTTP requests to a given URL and it outputs the response. It allows you to see the URL.
* curl url - download a single file 
* Save the cURL output into a file 
  * -o result will be saved in the filename provided in the command line 
  * -O filename in the url will be taken and will be used as the filename to store the result 
* Can download several files at the same time 
* curl -C -> continue/resume a previous download 
  * Can use crtl + c to stop it in between the download
* Can limit the rate of data transfer 
  * $ curl
 --limit-rate 1000B -O http://www.gnu.org/software/gettext/manual/gettext.html
* Download a file only if it is modified before/after the given time 
  * Will work for both FTP and HTTP 
  * $ curl
 -z 21-Dec-11 http://www.example.com/yy.html
* Pass HTTP Authentication in cURL
  * $ curl -u username:password URL
* Download Files from FTP server 
  * $ curl -u ftpuser:ftppass -O ftp://ftp_server/public_html/
* List/Download using ranges
* Upload files to FTP server
  * -T 
  * $ curl -u ftpuser:ftppass -T myfile.txt ftp://ftp.testserver.com
  * Can upload multiple files at the same time 
    * $ curl -u ftpuser:ftppass -T "{file1,file2}" ftp://ftp.testserver.com
* -v -> more info & -trace -> even more info
  * Comes in handuy when cURL fails 
* Get definition of a word using DICT Protocol 
  * $ curl dict://dict.org/d:bash
* Use Proxy to download file 
  * $ curl -x proxysever.test.com:3128 http://google.co.in
  * Need to specify host and port 
* Send mail using SMTP Protocol 
  * Specify from address, to address and mailserver ip address 
  * $ curl --mail-from blah@test.com --mail-rcpt foo@test.com smtp://mailserver.com
  * Once the command is entered it will wait for the user to provide the data to mail
  * Once message is complete. Type . as the last line which will send the email immediately. 

## Character Encoding 
* Choose the UTF-8 character encoding
* Needs to be in header for website 
* 95% of the world uses it 

## Domain Name System 
* The root of the internet's namespace 
  * The dot at the end of a url, that you don't see 
  * Then they proceed to look up the IP 
    * Cache - Memory 
  * Browser asks the operating system where the url is? 
  * If they don't know, the operating system ask a resolving name server
  * The resolving name server knows where to find the root name servers 
  * Root name servers know where to find the com name servers/TLD Top Level Domain servers
  * They point to the authoritative name servers. 
  * The TLD knows which authoritative name servers to use because of the registrar 
  * When the domain is purchased, they are told which authoritative name servers they should use. They notify the organization responsible for the TLD, the registry, and tell them to update the TLD name servers 
  * The resolving name server takes the response from the TLD name server, stores it in cache and then queries the example.com name servers. 
  * Authoritative name server then give us an IP address. 
  * Place it in cache and give it to the operating system then the browser 
* Record Types 
  * A: most common; map a hostnames to IP address (IPv4, 32-bit address)
  * NS: Name Server that is responsible for a DNS zone
  * MX: Mail Exchange record specifies where email gets sent to
  * CNAME: Canonical Name, an alias for another hostname
  * AAAA: similar to A, but uses IPv6, 128-bit address
  * set type=NS
  * dig +trace url

## Template 
* Useful for keeping server logic (JS) separate from markup (HTML)
* Seperating different parts of an HTML document into different files, keeping the length of those documents short and manageable

## Template engines 
* Need in order to use template files 
* Template engine replaces variables in a template file with actual data, and transforms the template into an HTML file sent to the client 
* We will be using EJS 
* <%- include('partials/_header') %>
* [EJS Tutorial](https://www.digitalocean.com/community/tutorials/how-to-use-ejs-to-template-your-node-application)

## res.render
* template + variables -> html -> browser 
  * This is called server side rendering 
  * Took a template and render out an html string from it

## CRUD and HTTP 
* CRUD: Web apps allow users to manipulate data in various ways: 
  * Create - Add a new record 
  * Read - Retrieve the value of a record 
  * Update - Update a record
  * Delete - Delete a record
* CRUD: Action	JavaScript
  * Create	users["5315"] = {first_name: "John", last_name: "Smith"}
  * Read	users["5315"]
  * Update	users["5315"].first_name = "Jane"
  * Delete	delete users["5315"]
* Http is the protocol to facilitate communication between the interface and the database
  * Server and browser is in between 
* HTTP: HTTP Method	- CRUD Action
  * GET	- Read
  * POST	- Create
  * PUT	- Update
  * DELETE -	Delete
* Safe methods - read only - do not modify the state of the server 
* Idempotent Methods - A request method is idempotent if multiple identical requests with that method have the same effect as a single such request. 

## Git Branching
* git branch bug/duplicate-message OR git branch feature/display-name-color
* git checkout master - switching to master branch 
* git merge bug/duplicate-message 
* git merge feature/display-name-color
* Special pointer called HEAD, tells you which branch you are on 
* You can see this by running git log 
* git log --all -> will show you all branches
* git switch on newer versions of git instead of checkout
* Return to your previously checked out branch, -> git switch -
* Create a new branch and switch to it -> git switch -c new-branch

## Cookies 
* HTTP server can tell a client to remember certain keys and values ("cookies") using a Set-Cookie header
* Are small blocks of data created by a web server while a user is browsing a website and placed on the user's computer or other device by the user's web browser. Cookies are placed on the device used to access a website, and more than one cookie may be placed on a user's device during a session.