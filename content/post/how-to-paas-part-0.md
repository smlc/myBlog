---
title: "How to PaaS - Part 0 (DRAFT)"
date: "2020-08-14"
author: "Heimerdinger"
---

Are you ever ask yourself how Platforma as a Service work? Then you are in the right place welcome to How to PasS part 0 (yes part 0, table index start at 0 no ?). 

### What a PaaS ?
Let's begin by defining what PaaS, for some of us it's where we push our fifteenth side project code on free tiers plan and it's get run by some nice peoples (thanks to them!)

Before I start to be curious about what happened on the other side for me PaaS can be resume by this command :
```git
    git push heroku master 
```
Then I get my incomprehensible URL to reach the service. (remember we are on free plan no way to buy a domain name for this side project)

For some of us it's reprensent this picture we all see when Googling PaaS for the first time 
{{< image src="/img/paasProviderService.png" alt="PaaS Provider Services" position="center" style="border-radius: 8px;" >}}

### What happend inside a PaaS ?  
But what a PaaS for theses peoples of the other side that working on it ? I'm sure you already see this picture comparing On-Premises vs IaaS vs PaaS vs SaaS. 
But it doesn't tell us how the code source we push on PaaS is built or how the request arrived at the instance of our application. 

{{< image src="/img/paasComponent.png" alt="PaaS component" position="center" style="border-radius: 8px;" >}}

In the next articles of this series, we are gonna try to see how each component work.




