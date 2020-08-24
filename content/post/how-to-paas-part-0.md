---
title: "How to PaaS - Part 0"
date: "2020-08-14"
author: "Heimerdinger"
---

Are you ever ask yourself how Platforma as a Service (PaaS) work? Then you are in the right place welcome to How to PasS part 0 (yes part 0, table index start at 0 no ?). 

### What a PaaS ?
Let's begin by defining what PaaS, for some of us it's where we push our fifteenth side project code on free tiers plan and it's get run by some nice peoples (thanks to them!)

Before I start to be curious about what happened on the other side for me PaaS can be resume by this command :
```git
    git push heroku master 
```
Then I get my incomprehensible URL to reach the service. (remember we are on free plan no way to buy a domain name for this side project)

For some of us it's reprensent this picture we all see when Googling PaaS for the first time. 
{{< image src="/img/paasProviderService.png" alt="PaaS Provider Services" position="center" style="border-radius: 8px;" >}}

### What happens inside a PaaS ?  
But what a PaaS for theses peoples of the other side that working on it? This picture comparing On-Premises vs IaaS vs PaaS vs SaaS doesn't tell use how the code we push on PaaS are build or how the request arrived to the instance of our application.

So here another view of all the components we can found into a PaaS that allow your application to run. You can find a more detailed version [here](https://docs.cloudfoundry.org/concepts/architecture/).
{{< image src="/img/paasComponent.png" alt="PaaS component" position="center" style="border-radius: 8px;" >}}

In the next articles of this series, we are gonna try to see how each component work. Follow me on [Twitter](https://twitter.com/MarS_XIV) for the next article.

Here some ressources I found while searching 
- https://youtu.be/3IXZ6Taa9Io
- https://youtu.be/UvIGFh3ZEgU
- https://youtu.be/nassYitfhfc
- https://devcenter.heroku.com/articles/how-heroku-works.



