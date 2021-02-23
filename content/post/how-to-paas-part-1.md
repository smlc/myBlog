---
title: "How to PaaS Part 1 - Routing"
date: "2021-02-23"
author: "Dr.Mundo"
---
 
 Who is routing the requests to your app




PaaS platform host application for a lot of users, so when you create an application in the platform how the platform sends the right request to the right application. I guess you don't want someone else receive your request. 

Here come the **routing** component who is responsable to send the incoming request to the right application.
Some PaaS leave routing for external tools like nginx (Doku)*

![](routing-paas-bg-none.png)
How cloudfoundry did ?

How Clever did ?

How heroku did?




 ### Routing component.

 This component can use alredy existing technology as HAproxy or Nginx ( Dokku). Or homemade technology as gorouter (Cloudfoundry) and SŌZU (CleverCloud).
 
The principale responsabilyof the router component is to send the request to the right application. In order to do his job well the routing component will need information like.

I receive a request for the application  www.mysupersideproject.com which application inside the PaaS this requestion is for.

Here the routing configuration come, when you ask the PaaS to create an instance of your application the routing component will need to know for each application that this request gone for this instance.

```yml
frontend api_gateway
    bind :443 ssl crt /etc/hapee-1.8/certs/cert.pem
    acl VHOST_app1 req.hdr(Host) -i -m dom www.mysupersideproject.com
    acl VHOST_app2 req.hdr(Host) -i -m dom www.anothersideproject.com
    use_backend app1 if VHOST_app1
    use_backend app2 if VHOST_app2

backend app1
    server s1 10.0.0.3:80

backend app2
    server s1 10.0.0.5:80
```
Here a example using HaProxy. Saying all the request coming with Host header www.mysupersideproject.com should be send to app1 and the one coming for www.anothersideproject.com should be send to app2.

**Keep the routuing component up to date**

Why the PaaS need to update the routing configuration there is different scenario. When you decide to add a new feature to your project in some case the PaaS will create a new instance of your app. You now have a new instance with a new IP address. In the case when you only have one instance of your app because you know it's a side project you don't need to scale with several instance. Once the new instance it's create the PaaS will need to kill the old one and update the routing configuration to the new one.

How the a routing component it's update ? 
They is two way ask for update (or receive them from someone else. 

Schema of routing component pull and push data.

Link to https://www.clever-cloud.com/blog/engineering/2017/07/24/hot-reloading-configuration-why-and-how/ and  https://docs.cloudfoundry.org/concepts/cf-routing-architecture.html








---
### Routing TCP and Http request in PaaS

Http and TCP are often the kind of protocole that PaaS have to deal with


---
### Load balancing
Important for scalibity,Session affinity




PaaS platform host application for a lot of users, so when you create an application in the platform how the platform sends the right request to the right application. I guess you don't want someone else receive your request.
Some PaaS leave routing for external tools like nginx (Doku)*



And others use a homemade tool like  Gorouter for Cloudfoundry or SŌZU (CleverCloud).

Inside 

TCP router and Http Router. 
App is accessing by using router like (gorouter, ngxin) that can be based in the http request param. Most of the time http routing is about configuation like url -> specific another url (made schema). That can be used to send request to multiple other instance of the app and to do load balancing. Some PaaS use internal implementation or other integrate other tool like Nginx for does routing. 

PaaS also need to keep routing information up to date while create new application or instance of already existing application.  This can be done by keeping a routing table.
These table or configuration files consist of attribute for patter or specific request an address to send the request to.




### How message are transported to your app (talk about this in messaging)
### Message broker vs network transport
You may ask yourself why are talking about message broker or network transport ? 
We will also talk about the layer on which the message being transported. Why sometimes the network as layer to transport messages is not enough and a message broker is needed.



My router feature : (https://docs.cloudfoundry.org/concepts/http-routing.html
- Handling Http request only.
- Get routing table by configuration
- CRUD on routes
- The update need to be done by react to update event (new app created, app instance addresse id modify). 
- router balancing (see https://docs.cloudfoundry.org/concepts/http-routing.html#round-robin)
- session affinity
Configure proxy config
https://www.clever-cloud.com/blog/engineering/2017/07/24/hot-reloading-configuration-why-and-how/


Related  links : 
-  Routing at https://youtu.be/CeaoTAXkIZE?list=PLwrg5JSccBqwMKmxQBqCTRBUNSEb5ovBR&t=5108
- https://www.clever-cloud.com/blog/engineering/2017/07/24/hot-reloading-configuration-why-and-how/
-  https://docs.cloudfoundry.org/concepts/http-routing.html#round-robin
- https://devcenter.heroku.com/articles/how-heroku-works
- https://docs.cloudfoundry.org/concepts/cf-routing-architecture.html


Tail keywords and topics : 
scability
### Check
- [x] Headlines (subheadline)
- [ ] Varied formatting 
- [ ] Shorten the intro and answer the question
- [ ] Cliff-hangers, create suspens
- [ ] Bit of humor ??
- [ ] Call to action
- [ ] External link
- [ ] Add the keywords
