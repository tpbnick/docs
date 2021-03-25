# REST vs. SOAP Web Services

## REST Explained

**Re**presentational **S**tate **T**ransfer (REST) is an architectural style that dictates standards for communication between computer systems on the web.  When a developer is looking for simplicity, broad language support, better resource management, and statelessness, they go for REST.  REST offers the ability to send a simple request, utilizing a GET, POST, PUT, and DELETE, to perform tasks.  REST-based web services can also return data in Command Seperated Value (CSV), JavaScript Object Notation (JSON), and Really Simple Syndication (RSS) data formats.

???+ tip
	When APIs embrace the styles and constraints of REST, they are said to be RESTful.

REST has guiding architectural constraints for an API to be considered RESTful:

* Client-Server Architecture  

* Statelessness  

* Layered System  

* Cacheability  

* Uniform Design  

* Code on Demand  

## SOAP Explained
The **S**imple **O**bject **A**ccess **P**rotocol (SOAP) is an industrial-grade API solution that works well within most environments.  Unlike REST, which is strictly an architectural style, SOAP is an actual protocol.   This gives SOAP much greater control over what an API does, from deciding the transport method, enhanced security, etc.  

SOAP has many benefits including:  

* Extensible Markup Language (XML) control over API (Comes at the cost of increased bandwidth).

* Various tooling for quick integration.  

* Transport control (HTTP/TCP/UDP/SMTP).  

* Rigid interaction specifications.  

* Built-in error handling.

## Quick Comparisons

| REST                                             | SOAP                                 |
|--------------------------------------------------|--------------------------------------|
| Stateless                                        | Stateful                             |
| Architectural style                              | Web protocol                         |
| Less bandwidth needed for requests               | More bandwidth needed due to XML     |
| Can make use of SOAP                             | Cannot make use of REST                 |
| Wide use of data formats (HTML, XML, JSON, etc.) | Only works with the XML format       |
| Requires use of HTTP/HTTPS                             | Can utilize HTTP, HTTPS, TCP, UDP, and SMTP |

## When to use REST vs. SOAP

Deciding whether to use REST or SOAP should come down to determining what your end goal is and who will be using the API.  REST and JSON have recently become the go-to for web developers because it consumes less bandwidth, has increased flexibility, and offers easier integration with applications.  SOAP definitely still has its uses, specifically for APIs that need asynchronous and stateful operations, such as the financial industry.  Answering the following questions can also help determine which web service to use:

* Who will be consuming the API data?  

* How often will the API change?  

* What types of applications/integrations will the API interact with?  

* What programming language is the API written in?
