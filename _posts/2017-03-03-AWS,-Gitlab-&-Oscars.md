---
layout: post
title: "The AWS-S3 & Gitlab outages, & Oscars too"
keywords: "AWS, S3, Gitlab, Oscars, Netflix, chaosmonkey, principles of chaos engineering, checkyourbackups"
---

There was a [debilitating S3 outage](https://twitter.com/awscloud/status/836656554212372480) around March 1, and now [AWS has put out a document](https://aws.amazon.com/message/41926/) on what might have gone wrong.

Before we go onto what might have started the chain of events, let me also quickly mention the Gitlab incident earlier this month, which led to this [website being birthed](http://checkyourbackups.work) somewhere on the Internet.

On January 32, [Gitlab had an incident](https://about.gitlab.com/2017/02/01/gitlab-dot-com-database-incident/) with one of its database servers which led to a few thousand lost commits & users, among other things.

Now with the two events in context, let me just quickly cite the one bit I find very amusingly common in both of them. Per AWS' release linked to earlier, and I quote:

> At 9:37AM PST, an authorized S3 team member using an established playbook executed a command which was intended to remove a small number of servers for one of the S3 subsystems that is used by the S3 billing process. Unfortunately, one of the inputs to the command was entered incorrectly and a larger set of servers was removed than intended.

and this now is quoted from [GitLab's post-mortem report](https://about.gitlab.com/2017/02/10/postmortem-of-database-outage-of-january-31/):

> Trying to restore the replication process, an engineer proceeds to wipe the PostgreSQL database directory, errantly thinking they were doing so on the secondary. Unfortunately this process was executed on the primary instead. The engineer terminated the process a second or two after noticing their mistake, but at this point around 300 GB of data had already been removed.

If you're thinking clearly humans messed this one up, then wait. You maybe thinking about the [Oscars mix-up](https://www.theguardian.com/film/2017/feb/27/pricewaterhousecoopers-issues-sincere-apology-for-oscars-blunder)

When working with distributed systems, which is nearly every computing system right now, [Principles of Chaos]( http://principlesofchaos.org/) is a great place to start.

I learnt of it from [Netflix' reaction](http://techblog.netflix.com/2011/04/lessons-netflix-learned-from-aws-outage.html) to a AWS outage back in the day, which led to them expanding the scope of a tool they already had, [chaosmonkey](https://github.com/netflix/chaosmonkey).

When working with the cloud, the joke to remember is its always someone else' computer, and that someone maybe having a good or bad day at work, at their own computer, completely oblivious to your code or assets residing within their reach. So make sure you are always ready to move at a moments notice.

Now before I close this post, that Oscar incident. There are always two envelopes on either side of the stage for every category of the prize. That's redundancy, or availability, in CAP theorem speak. And we naturally have partition as well. Whenever you have partition, communication and latency is key.
The two stacks on the either sides got de-synced after the Best Actress category award was given out, and one side still retained the Best Actress envelope, and it is this envelope that the presenter for the Best Picture was handed, bearing the name of Emma Stone, for the film La La Land. What we had then, was an AP system.
The team handling the envelopes could have practiced for this consistency disaster, which brings us to the topic of readiness we're addressing in this post.
Here's a quote from [the team members](https://www.theguardian.com/film/2017/feb/27/pricewaterhousecoopers-issues-sincere-apology-for-oscars-blunder) that sheds some light on the aspect of readiness
>In a prescient interview with the Huffington Post last week, under the headline "What would happen if a presenter announced the wrong winner at the Oscars?", Cullinan and Ruiz discuss the "unlikely" eventuality that the wrong nominee will be called.
They told the news website that the exact procedure for dealing with such a mistake was unknown because such errors had never been made in the Oscars' 88-year history.

Hope for the best, but prepare for the worst.
