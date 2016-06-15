---
title: Merge Hells? Feature Toggles to the rescue!
date: '2016-03-29 15:48:08'
tags:
- cap-leena
- business
wp:post_id: '6050'
link: http://www.multunus.com/blog/2016/03/merge-hells-feature-toggles-rescue/
---

![Merge Conflicts](http://images.memes.com/meme/369621)




















Familiar with the above story? Has it ever happened to you? Then read on, these are simple techniques which can help you to prevent your team working on such non-value added tasks such as fixing merge conflicts.


[]()Before jumping on to the solution, let’s first correct some misunderstandings/misconceptions about Continuous Integration.


#Continuous Integration



[](https://en.wikipedia.org/wiki/Continuous_integration)


Let's go back to the practices the Team X were following. They had CI setup for each feature branch, which is against the above definition of CI.


BothContinuousandIntegrationare important in CI and it means continuously integrating the code in one branch, not in multiple branches. Let us see why this is important.


##Mainline Development



[Mainline Development](http://paulhammant.com/2013/04/05/what-is-trunk-based-development/), also known as Trunk based development, is where everyone in the team commits to a single branch. Continuous Integration on the mainline branch guarantees that the branch is ready for deployment at any given point of time.


If Team X was following the same, the time they spend on merging and fixing conflicts could have been used for creative tasks.


Wondering how will you handle the situations such as following?


*Features under development

    
*Features waiting for Acceptance from business stakeholders

    
*Pushing quick fixes or patches to production


Read on.


#Feature Toggles


[caption id="" align="alignleft" width="718"]
![Feature Toggles](https://pixabay.com/static/uploads/photo/2013/07/13/13/47/button-161555_960_720.png) 
[Credit: 
[https://pixabay.com/static/uploads/photo/2013/07/13/13/47/button-161555_960_720.png](https://pixabay.com/static/uploads/photo/2013/07/13/13/47/button-161555_960_720.png)][/caption]


This is where Feature Toggles come to the rescue.


A Feature Toggle -  also known as a Feature Flag, Feature Flip or Feature Switch - is a simple technique where you can turn on or off a certain feature through configuration.


Let’s go back to the Team X. By keeping toggles for the features, the entire team could have continued working on the same branch and the long-living branches could have been completely avoided. This along with[Continuous Integration as mentioned above](#ci), where the code gets merged and tested multiple times a day, merge issues should be very minimal or non-existent.

By keeping the toggle off in the production environments, the worry of end users seeing the incomplete feature can be avoided.





In the above code snippet,is the feature which can be turned on and off depending upon the environment where it is running such as testing, staging, production etc.


Yes, I know what you are thinking. So many “”. Yes, it’s true. It can get complicated. But it’s only for a short period of time. Once the feature is done, the toggle can and should be removed completely.

In case there is a quick fix that needs to be pushed to production, there is no confusion about which branch to fix and rebased with as there is only one branch. The fix can be very confidently pushed to production, with the feature under development being turned off.


##Experimental Toggles



The release toggles, the toggles to hide partly built  features, are a very common use of feature toggle.


Another type of toggle isExperimental Toggles, where the feature is exposed to a set of users for quick experimentation and feedback. This is commonly done using one of the below techniques.


*[A/B testing](https://en.wikipedia.org/wiki/A/B_testing)or[Multivariate testing](https://en.wikipedia.org/wiki/Multivariate_testing)- to test multiple parallel experiments

    
*[Canary Release](http://martinfowler.com/bliki/CanaryRelease.html)or[Blue Green Deployments](http://martinfowler.com/bliki/BlueGreenDeployment.html)-  - to incrementally launch the feature to batches of users

    
*[Dark Launching](https://www.facebook.com/notes/facebook-engineering/hammering-usernames/96390263919/)- Launch the feature to soak test even before releasing it to the users


##Ops Toggles



A good system should be designed for failures. A failure can due to anything that comes under the “unexpected” category, such as unexpected load on the system or unexpected hardware failure or unexpected network failure.


When you see such surprising behaviors in production, the usual thing to do is to rollback the code. The rolling back of code can be as complicated as merging long-lived branches.


Ops Toggles, another type of Feature Toggle, can be used for degrading a specific feature or for removing a specific feature completely until the situation is brought under control. Using Ops Toggles, you can turn off the feature without rolling back the code.  Ops Toggles can be considered as a way to manage[Circuit Breakers](http://martinfowler.com/bliki/CircuitBreaker.html).


Users might have a degraded experience which is much better than keeping the buggy feature which will continue to embarrass many users.

[caption id="" align="alignleft" width="676"]
[![Types of Feature Toggles](http://martinfowler.com/articles/feature-toggles/chart-3.png)](http://martinfowler.com/articles/feature-toggles.html) [Credit: 
[http://martinfowler.com/articles/feature-toggles.html](http://martinfowler.com/articles/feature-toggles.html)][/caption] 


Keep in mind toggles need to be short lived, except for Ops Toggles. And keep toggles as few as possible.


##Cathedral vs Bazaar Model



[Github workflow](https://guides.github.com/introduction/flow/)is a model that is commonly used by many. It is a good model for Open Source Projects to bring in some amount of rigor to the[bazaar](https://en.wikipedia.org/wiki/The_Cathedral_and_the_Bazaar). But in a more controlled environment, relying on interdependence within the team for code reviews or pair programming might be better. The value of the code will start coming in only when it reaches the users. Until then it is a Work In Progress or inventory. And our goal should be reduced Work In Progress.


Please read[my earlier post](http://www.multunus.com/blog/2013/06/github-workflow-vs-mainline-development/), which talks about this in detail.


##The Dark Side



As we discussed above, Feature Toggles introduces, which can add to the Code Complexity. Ideally, the toggles should exist for a short duration until the experiment is done or until the feature reaches to all the users. But ideal, at times, may be far from reality, which can create issues as shown below.


[![Dark side of Feature Toggles](https://s3.amazonaws.com/next.multunus.com/wp-content/uploads/2016/03/Screen-Shot-2016-03-29-at-3.33.29-PM-1024x589.png)](https://s3.amazonaws.com/next.multunus.com/wp-content/uploads/2016/03/Screen-Shot-2016-03-29-at-3.33.29-PM.png)


Case in point: Knight Capital Group’s[$460 million dollar mistake](http://dougseven.com/2014/04/17/knightmare-a-devops-cautionary-tale/), where a wrong use of the Feature Flag and Manual deployment caused the company many $$ in just 45 minutes.


##Tips



Every approach has pros and cons.


I would like to relate this to “how to pay off technical debt?”. Different teams might be following different tricks for[paying off the technical debt](http://martinfowler.com/bliki/TechnicalDebtQuadrant.html). But the goal for every team is to reduce it to the minimum so that it doesn’t affect the predictability or sustainability of software delivery. There is no “silver bullet” that really works for every team because the context is different for each team.

The same applies to Feature Toggle too. There is no silver bullet to make sure that the Feature Toggles are short lived. There are quite a few tips and tricks followed by the teams, which can potentially work for many.

At Multunus, what we have seen working is adding the card to the backlog to get rid of the Feature Toggle, along with reviewing the feature toggles once in every few weeks.


Another technique is to define[“expiry date” for toggles](http://martinfowler.com/articles/feature-toggles.html)and also logic to break the build or refusing to start the application if toggles exist beyond the. The same article talks about feature toggles in detail and a variety of different ways of reducing code complexity through better design of the code.

Try out different approaches and see what works and what doesn’t. A common thing with any tool is that when people are new to the tool, there is a probability that they don’t use the tool in the way it was supposed to be used.

The solution is not to blame the tool or person who used it wrong. Instead, fix the issue quickly and identify the gap and provide better training mechanisms to avoid similar issues happening again in the future.


This requires a systematic way of conductingpostmortems. This is known as  [Blameless Postmortems](https://codeascraft.com/2012/05/22/blameless-postmortems/), as referred by[John Allspaw](https://twitter.com/allspaw), where the effort is to balance safety and accountability.


#Further Readings


Both Mainline Development and Feature Toggles are practices followed by many high performing organizations since their very early days. You can go through the below posts which refer to some of those:


*[10+ deployments a day @ Flickr](http://www.slideshare.net/jallspaw/10-deploys-per-day-dev-and-ops-cooperation-at-flickr/47-1_RespectIf_there_is_only)

    
*[50+ deployments a day @ Etsy](http://www.infoq.com/news/2014/03/etsy-deploy-50-times-a-day)

    
*[Amazon does deployments every 11.6 seconds](http://joshuaseiden.com/blog/2013/12/amazon-deploys-to-production-every-11-6-seconds/)

    
*[Google - commit to production is 8 minutes](https://air.mozilla.org/continuous-delivery-at-google/)

    
*[Dark Launching @ Facebook](https://www.facebook.com/notes/facebook-engineering/hammering-usernames/96390263919/)

    
*[Netflix - Lessons learned during AWS Outage](http://techblog.netflix.com/2011/04/lessons-netflix-learned-from-aws-outage.html)

 
