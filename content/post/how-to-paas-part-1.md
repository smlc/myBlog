---
title: "How to PaaS Part 1 - Routing"
date: "2021-02-23"
author: "Marlon"
---

If you haven't read yet the part 0 of this series is [here](https://imars.blog/post/how-to-paas-part-0/).

## Who is routing the requests to your app

PaaS platform host application for many users, so when you create an application in the platform how the platform sends the proper request to the correct application. I guess you don't want someone else receives your request.

Here comes the **routing** component responsible for sending the incoming request to the correct application.

{{< image src="/img/request-routing.png" alt="Request routing" position="center" style="border-radius: 8px;" >}}

## Routing component.

The routing component can use existing technology as HAproxy or Nginx ( Dokku). Or homemade technology as gorouter (Cloudfoundry) and SŌZU (CleverCloud).

The principal responsibility of the router component is to send the request to the correct application. To have his job done, the routing component will need information like :

-   The IP of the machine where the application is running
-   The port for TCP communication
-   The Domain name that needs to be redirect

Let say our PaaS  receive a request for the application  www.mysupersideproject.com

When you ask the PaaS to create an instance of your application, the routing component will need to know where to send each request.

Here a example using HaProxy. 

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

All the requests coming with the ost header www.mysupersideproject.com should be sent to app1, and the one coming for www.anothersideproject.com should be forwarded to app2.

### Keep the routuing component up to date

**Why the PaaS need to update the routing configuration ?**

When you decide to add a new feature to your project, the PaaS will create a new app instance. You now have a new instance with a new IP address.
Once the new instance creates the PaaS will need to kill the old one and update the routing configuration to the new one.

When you have several instances of your app, the PaaS will need to update the routing configuration when he creates a new instance and behaves as a load balancer to send requests to the different instances of your app.

#### How the routing component is updated ? 

{{< image src="/img/routing-configurations-possibility.png" alt="Request routing" position="center" style="border-radius: 8px;" >}}

**Static configuration** : The routing component has all the configuration at the start time.

**Dynamic configuration** : The configurations changes on runtimes and can be pull from external service like etcd,Zookeeper. One of the [main problems while changing the configuration on runtime is reload or restarting the service](https://www.clever-cloud.com/blog/engineering/2017/07/24/hot-reloading-configuration-why-and-how/), which brings interruption. Having to restart this kind of service can make the component lose the open connections.

Here some ressources I found while searching :

- https://www.clever-cloud.com/blog/engineering/2017/07/24/hot-reloading-configuration-why-and-how/
-  https://docs.cloudfoundry.org/concepts/http-routing.html#round-robin
- https://devcenter.heroku.com/articles/how-heroku-works
- https://docs.cloudfoundry.org/concepts/cf-routing-architecture.html
- https://doc.traefik.io/traefik/getting-started/configuration-overview/
