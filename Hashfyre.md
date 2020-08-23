# Hashfyre (Joy), Devops

- Building Signoz.io with @pranay01
- Early members of DevOps team at Razorpay. Scaled Razorpay from 40 to 40K customers over 2.5 yrs, with @nemo and @tasdik
- Worked with @cruisemaniac at Zoomcar
- At Hotstar, worked with their infra metric pipeline and did around 8M RPM on a k8s cluster during IPL 2018
- Currently working as a consultant with multiple orgs, with Signoz.io being the most interesting of them, who are building an lightweight APM solution

<details>

<summary>What specific skillsets do you think are useful for freshers aiming to get into DevOps?</summary>

- Try and be a generalist, the flux in devops is constant. Adapting fast is a huge bonus
- Linux Systems knowledge helped me
</details>

---

<details>

<summary>How did you scale from 40 to 40k, overview of the architecture?</summary>

- it's a lot about using the right tool and the right time and convincing stakeholders and devs alike that investment on devops process and toolchain is worthwhile in the long run
- So we went like this,
  - AWS, EC2, 1 monolith, CICD with wercker
  - VPC migration to terraform, packer, ansible
  - [Shipping servers continuously with ansible packer and terraform Slides](https://speakerdeck.com/hashfyre/shipping-servers-continuously-with-ansible-packer-and-terraform)
  - ASG, loadbalancers, NAT Gateways
  - Prometheus, ES
  - CoreOS + single Docker per Ec2 with systemd
  - kubernetes with bootkube + terraform
- all in a span of 2.5 yrs
- delivery velocity was a huge thing for us
- 10+ deploys to prod / day in the initial days, this was slowed down over time to make room for more complexity and a slower cadence

> No lambda or serveless, also thoughts on server less?

- we did some lambda circa 2016, but there was no serverless buzzword hype then
- a lot of our financial institution file transfer stuff was on lambda
- when we interacted with orgs that didn't have apis and had to send them consolidated data as files
- Also yeah DevOps != BuzzWordOps
- This is mostly about tech evolution albeit breifly
</details>

---

<details>

<summary>what is the most challenging piece of the work you have faced?</summary>

- Writing Self-review
- Convincing leadership to invest in tech-debt

> I meant in devops though

- Yes, that's the most important part. Tech is easy. Building a DevOps culture is difficult.
- Whatever you're trying to do, if you can't get buy-in from leadership, it's gonna go down the drain. Sooner or later.
- Tech is more or less deterministic within certain bounds, people are the hardest part

</details>

---

<details>

<summary>How do you decide where/what you want to work on?</summary>

- Depends on the scope
- a roadmap highlights long term goals
- a sprint kanban defines 2 weeks worth of work
- with 30% buffer for ad-hoc
- in my experience pure sprint, agile etc doesn't work for a devops org unless you've a split platform and SRE team
- at any time revenue loss takes top priority
- any incident that makes the org hemorrhage money is P1

> I also meant in a broader sense. Like how do you decide between companies/job ?

- Hmm, I may not be the best person to offer advice on that, I've a bias towards hacker-culture over super-structured orgs which has knowledge silos
- I'm still figuring this out, I end up working for people I like more than the org
</details>

---

<details>

<summary>Whats your favourite prod incident story?</summary>

> A migration story

- Moving an entire VPC from us-east-1 to ap-south-1 during demo under peak load seamlessly
- our devs didn't know the next day that we had moved regions
- the frontend person noticed reduced response times and came to ask us during lunch the next day
- we did this with a 2 month prep + code + rehearsals and zero downtime
- it was me, my lead, nemo and a Sr. Architect
- we had excellent Irish whiskey in the morning at 7 am and went home to sleep

> Incident story would be the one at HotStar:

- Where I had to trick the `volumeAttachDetachController` to mount a volume / PV from another region by manually altering PV / PVC IDs, labels, annotations
- because we had exhausted one AZ and prometheus node wasn't coming up in that region
- without prometheus we lost real time metrics, which meant our metric-server + HPA + DynamoDB based stepped-scaling logic wouldn't work
- unable to scale means unable to stream and and losing users
- I still have a [P1 bug on thanos](https://github.com/thanos-io/thanos/issues/981) from the time, seems it got closed 26 days ago, it got stale and closed down, wasn't solved

> Be so big you empty out the AZ

- of that particular machine type, c5.9XL
- Which is why when someone asks me what's the solution for scale, I say money

> But if you were mounting a PVC from another region wouldn't that affect the response time severely? (Guess that was an acceptable tradeoff)

- we had other nodes, on the other regions
- I cloned over the volume to the AZ, but had to fake volume ID -> PV -> PVC manually identically so that the controller feels it's a PV from the same AZ and mounts it on a new node in the healthy AZ
- we were only losing metrics forwarded to one of the prom nodes
- thanos dedup should have taken care of it
- but due to the above issue, the overall metric numbers tanked whenever a gap overlapped with full data
- triggering a scale down
- so we had to freeze auto-scale up/down during the duration of the fix
</details>

---

<details>
<summary>How do you create those amazing D&D characters, tell me the whole process?</summary>

- I'll have to record a YouTube video
- I just watch other videos on YouTube and practice, my RPG group also has great people who offer feedback and teach me a thing or two (artists themselves)

</details>

---

<details><summary>Have you thought about starting your own thing, as you were one of the early members in many companies; if yes, what it will be, if not, why not</summary>

- Yes.
- But I believe I still have a lot to learn from people. Which is why I left HS to work on a product idea that my ex-mentor from Razorpay had (one of his friends who was the CEO of a Service based company wanted to build this under his org's banner) . I built it to our mutual vision. So even though the company tanked, I built my first Product to spec in a year with only two freshers in my team.
- Which is also why I'm trying to work with folks in Signoz who are focused on building platforms
- Lots to learn.
- Most of my current clients are folks building MVPs

> What things now are more important compared to the time when you have started in building products/MVPs?

- I have to unlearn a bit of my detail oriented approach. Focus more on core functionality than getting everything right (which comes from my DevOps background)

</details>

---

<details>
<summary>what are the major mistakes do you think that freshers/early stage devs do when building a platform compared to the experienced devs as you have worked with both the kind of peoples?
</summary>

- Trust in their headcanon rather than do market research, user base cultivation
- If you feel that you're version is the best possible version. It may be more hubris than ingenuity.
- Sometimes you can launch a product with an XL sheet and build the tech later, if you can find how to cultivate your first customer set
</details>

---

<details>
<summary>
what do you feel about this remote working for the onsite working companies where osmosis learning is almost impossible and what should be the right way to help the juniors?
</summary>

- After a 5mo WFH marathon, I think I'll personally be glad to be among people in an office.
- The only circumnavigation is through video calls. But I'm not sure how that renders unto osmosis learning.
- I found it very challenging leading even a small team full remote.
- Afterwards I've just been working solo.
</details>

---

<details>
<summary>From supporting 40 to 40k customers, how did the team grow? Did you scale in some linear fashion (most probably not), or just grow by a couple of folks (probably the other extreme)? What helped you choose the right path to grow this team?
</summary>

> interesting to hear what the numbers were at the start and end, and the journey (though I suspect the magnitude will be a lot smaller)

- our team scaled from 2 to 5, then 8 at the tail end, in the course of my 2.5yrs
- we grew the team initially in a reactive manner, proportional to pending workload per sprint
- then we actively started being proactive about it, sort of working out 1 yr roadmap and hire based on that + scale buffer of 5x load

> Ah, that last part is pretty nice. I've mostly been in teams where the team grew in a reactive manner, this is a nice way to think about it!

</details>

---

<details>
<summary>
Sort of related: how did you change tooling as you grew? What were your leading and lagging indicators that certain components were not going to serve you over the next few stages of growth? And, how did you handle deprecation once you realised that some stuff had to go?
</summary>

> I'm sure the channel would be very interested in the technical aspects. I'd also love to hear about the organisational aspects of this change

- Our first driving factors were twofold, speed and security
- Other aspects been explained in one of the above questions
- Core choice was automate everything, Infra-as-code everything
- git RBAC, SG access
- every single resource and rule was defined in terraform
- later the app layer transferred into docker and infra layer to k8s
- which was almost a year long effort for 10+ microservices
- and once we got in the mood for microservices, there was a new one planned every month
- so migration + service onboarding was a challenge
- one of the core aspects that were lagging back then was observability
- especially **Logging**
- we had splunk which had license cost and storage volume issues
- then we moved to ES, which became almost a full time job of one of our team members to keep fixing indexes and creating dashboards
- A single node prometheus worked for us for a while, with 15d retention
- NewRelic later became the core of our o11y stack after a while
- but I guess a lot has changed since then
- I'm aware of the current efforts, but I guess you can hear it from the horse's mouth. cc @nemo

> There's absolutely no doubt that everything checked into code for infra is a massive boost for keeping a team sane...

> Thank you so much for the detailed replies! Adding a follow up question...

> How did you operationalise the 'new micro service every month' bit later? Did you rely on documentation alone, or did you rely on scaffolding tools to make it easier for new teams to onboard? How did you then keep people from copy/pasting stuff and making it a mess to maintain as a central team?

- this was a time we were slowly going polyglot
- from the initial PHP monolith to go microservices for smaller stuff and python microservices for data / ML stuff
- a good practice we carried over from the PHP world was core modules / libraries
- our PHP monolith, even though such was built on top of few clean interfaced modules
- so that first batch of PHP microservices sort of were spun off with these core libraries re-used
- go, python were new to the team
- and were mostly being developed by the new hires
- we had like 3-4 go, 2 python services IIRC
- so not much boilerplate was done, but we were cognizant that it would have to be done some day
- I was more focussed on building easy delivery pipelines and on-demand envs
- which were getting harder with just terraform
- the tooling around multi-tenancy was still in it's earliest days
- ephemeral clusters were something we were planning to get to
- also, we never had the pod approach
- so there was no getting a team onboarded
- every dev had access to all repos
- there were no silos
- devs participated in ops and vice-versa
- our pipeline was to get a new service from spec to prod in shortest time as possible
- and ensure reactive changes could be deployed through quick dev-stage-uat-prod pipeline

> Per developer branch environments are hard to manage in a micro services model, we felt that Terraform was the wrong tool to define that infra...

- we had per feature branches and rebase arch
- no per dev branches
- But yeah, which is why moving to k8s was essential

</details>

---

<details>
<summary>
Few questions on open-tracing:
- What are the easy/cheap/simple/perfect stack choices for open tracing?
- What's a cool not-so-famous opentracing project, and why is it cool?
- Thoughts on open-tracing without any of the Kubernetes/service-mesh hype? What does that even look like?</summary>

```
Answered by @Ankit Nayan
> What are the easy/cheap/simple/perfect stack choices for open tracing?
Jaeger and Zipkin among opensource projects. Though I couldn't find any TCO blogs for setting up and running them. Apache Skywalking has some Opentracing compliant APIs [https://github.com/apache/skywalking/issues/4722#issuecomment-619733912]
> What's a cool not-so-famous opentracing project, and why is it cool?
A cool project eventually becomes famous. I guess, what you meant is a cool project that is still not heavily adopted?
> Thoughts on open-tracing without any of the Kubernetes/service-mesh hype? What does that even look like?
OpenTracing becomes important for microservices architecture where multiple services interact with each other and thus pointing out which dependency service is responsible for a breaking API becomes difficult. Tracing is very relevant even for non-kubernetes or service-mesh setup
```

- OpenTracing is going to get deprecated and moved to OpenTelemetry anyways
- Jaeger, Zipkin, all of the folks are in the middle of starting to support OpenTelemery APIs
- which to most extent are OpenTracing compliant too
- as of now the easiest I can think is jaeger + openTelemetry with JBOD storage
- later JBOD (just a bunch of disks) can be replaced by cassandra-kafka
- do look at this demo: [otel-k8s](https://github.com/Hashfyre/otel-k8s)
- @nemo Hashfyre also wrote a blog around Otel for k8s - if you are interested - [opentelemetry-kubernetes](https://signoz.io/blog/opentelemetry-kubernetes/)

</details>
