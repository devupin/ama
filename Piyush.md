# Questions with Piyush (Ex-CoFounder of Verloop)

<details>

<summary>What was the most challenging piece of tech you faced while at verloop</summary>

- Challenging conceptually: The in house MQ(Message Queue).
- Challenging to make maintainable: the bot framework.
- Challenging to debug outside of Machine Learning: Message drops between Go's SockJS implementation with the SockJS client.
- Challenging to keep scaling through the years: The Nodejs monolith we started with.

I guess the ML team would call dibs on the most challenging overall.

</details>

---

<details>

<summary>How did Verloop come to be</summary>

**Short version**: After MagicX (B2C concierge bots) shut, investors had some left over money and asked us to play with it, we did and it clicked.

**Long-ish story**: The initial story of GoDeliver is kind of [here](https://www.reddit.com/r/india/comments/2x3fy1/mostlyrant_semiselfpromotion_the_last_straw_np/). We eventually realised that ops is not something we could deal with and unit economics would just not work. We were very naive when we started.
Eventually, Gaurav met Pratyush and MagicTiger (B2C concierge humans) aquihired us, didn't work. Pivoted to MagicX (B2C concierge bots)
MagicX didn't work on multiple fronts. Mostly one big name competitor screwed big time and the hype cycle of entire space suddenly dried up. In general investors did not want to get into the B2C side.
We learnt a lot from it though. Among other things, we figured that utility of bots was somewhat there, distribution was a bitch and it wouldn't work in B2C.
So we figured we could build a bot platform for other businesses to automate part of their L1 support. They already had the problem and the distribution, our solution could cut their costs down and add a lot of consistency/timezone cover.
Some investors were kinda iffy and wanted us to become India dev center of their friends, we declined and gave this a shot, it worked

</details>

---

<details>

<summary>Please tell a production crash story</summary>

The most fun crash was when our bot and a WhatsApp business account's auto-responder started talking to each other. We didn't have rate limit at the time.
It was a long distance snowballing infinite loop of messages.
Each message from WhatsApp would produce 2 messages from our bot. So with each iteration, the number of messages would double. [We crashed within minutes](https://youtu.be/jZu050yHZ8w?t=174)!

</details>

---

<details>

<summary>What does your tech stack look like in Verloop</summary>

Google Compute VMs + CloudSQL + GKE (Terraform, scripts, duct tape and hope)
RabbitMQ/Cloud PubSub (config on our deployment manager + wild west)
Most new services are in Go. Some old services are in Python. Most of Machine Learning is in Python, a little bit in haskell and some C++.
And there's a monolith that's slowly being broken into microservices

</details>

---

<details>

<summary>How did you get your initial 10 customers</summary>

Gaurav(Founder of Verloop) would have a much better answer to this than me.
He transformed from an engineer/product guy to a salesman within the span of a few months and made the magic happen!
The network he built on his own + investor connects + lots of travel and meetings later, we got our first real customer.
I don't think he considers any customer we get today less special than the ones we got back then.

</details>

---

<details>

<summary>How did you get initial funding? How did you manage to fund till that time</summary>

After MagicX shut down, there was still a little money left in the bank.
That's what we ran on.

For long answer check the above question on verloop starting.

</details>

---

<details>

<summary>Tell us about your personal programming journey. Also how was the workload like</summary>

For workload, I kept trying to make it low/consistent for others by piling on things on myself. Terrible decision, I should have delegated way more.

My 11th grade tutor had made his tutorial's site on Geocities. I asked him how he'd done it, as if it were magic. He introduced me to HTML.
The internet cafe I used to go to surf at, they were also the local cable TV operators. They wanted to build a local news site. I built a static one for them that I would update every morning by hand. Someone on yahoo chat forums told me that they'd just made a bunch of money with this thing called PHP. I was running out of "aashirvaad money" so I thought I could learn it and make money myself. My dad, like the typical Indian father, had threatened to throw me out when I turned 18, so somehow in the teenage brain of mine, it sounded like a viable thing to do in case my father did follow through
I went to the local bookstore and asked him to get a book on PHP. Used that book to teach myself PHP in the internet cafe.
Made a bet with the cafe guy that I could automate the cricket scoreboard, they bet that they'd give me free unlimited internet access if I could pull it off. I won :D
Found this site called `getafreelancer.com` (which eventually turned to shit and became `freelancer.com`). [This is me](https://www.freelancer.com/u/xuberance).

Since then, most of my learning has been "I need this, what tool can I use to get it done" or "the software I need to work with uses X, let me learn it".
Through freelance projects, learnt Ruby on Rails and AngularJS (back when jQuery and backbone were the only other things that existed)
Picked up Python for GoDeliver because we figured ML would need to be in Python and it would be easier to have the entire stack in Python. Picked up Ansible around the time we moved to MagicTiger. Learnt Go towards the end of MagicX/early Verloop.
Since our ops genius had left the company, I moved us to easier to manage and understand Kubernetes (GKE), Terraform etc came later.
Got deeper into messaging, consensus and distributed systems in general over the course of Verloop.
Still haven't learnt jack about ML though. Might learn this year.

</details>

---

<details>

<summary>Is this a pure SaaS product (i.e. customers can self-service themselves) or do you have to do customizations for each customer? What's the geographic distribution of your customers like? Are most of them based in India? How do you built an outreach for clients based abroad? How do you build differentiators w.r.t other similar products (e.g. drift, intercom)</summary>

> Is this a pure SaaS product

Yes and no.

The core offering was self-serve. You can integrate on your own and do whatever you want with it. But the low end of the market was not our target.
When I'd left, some were purely self-serve. For some, there's some work in the initial onboarding. Helping them make their bot flow and such.
For the bigger ones, we had a team that would help with integrations with their APIs.
The strategy was to build things that work and help customers irrespective of being pure SaaS or not, learn and keep making the SaaS part wider over time, then go partnered vendors route like Salesforce etc.

> What's the geographic distribution of your customers like?

India and MENA were the main ones. We'd just started building presence in SEA when corona hit and those companies had to slow/halt operations for a while. I am not sure how the distribution looks like now.

> How do you built an outreach for clients based abroad?

Gaurav would know to answer this better. The short answer is, build and work the network

> How do you build differentiators w.r.t other similar products

The answer to this keeps changing over time. Last I knew, our main differentiator was that our bots were a lot more capable than those.
Much better and deeper support, premium pricing.

</details>

---

<details>

<summary>You were working on Unity too, are you still doing that? Are you going to invest more time on this? What are you working on currently</summary>

I did for [github game](https://github.com/ofpiyush/EcoFighter) off 2018!
Silly game made in a month.
But that was probably the first time I acknowledged that environment has an issue that needs addressing.

> Are you going to invest more time on this?

I might make games for fun, haven't given it a serious thought to be honest.

> What are you working on currently?

Right now I am working on myself, recovering from the mental and emotional burnout. Becoming more resilient I guess :)
Outside of self, learning more about climate change and sustainability, weighing solutions there.
The last couple of weeks, I've felt much better than before. If this continues, I'll start looking for work soon I guess, in OSS and/or climate change!

</details>

---

<details>

<summary>How did you deal with burn out over the years? What broke you eventually</summary>

Whenever I felt very stressed out, I would take a breather. Sometimes just for a few moments, sometimes a day off.
After the first couple of years, I stopped pushing myself on weekends and late nights.
I listened to music more. Weekends, I would go for movies or something relaxing.
When things would get really bad, a long cuddle fest helped a lot
Then it kept getting progressively worse.
Last year, I started smoking again.
Then I started spending emotional energy on it, "this is my baby", "I owe it to the people to give them my best".
Then came negotiation with self, "let me see how far I can keep stretching, this wil feel great in the long run when I get better at it"
Eventually I ran out of emotional energy, most of my day was spent on doing things I didn't enjoy.
At first I would tell myself "oh I don't like it because I'm terrible at it" but then I started getting the hang of it and still didn't like it.
One colleague was going through terrible time and I found myself saying to myself, "well, what can I do. Life is hard for everyone, some eggs will get broken along the way"
That was the big reality check. "This is not the person I wanted to become."
The final straw was something I am not prepared to share yet. But I don't think the final straw alone would have made me leave.

</details>

---

<details>

<summary>3 best and 3 worst things about startup ecosystem</summary>

I am not big into the 'ecosystem' to be honest.
I can speak of things I've seen in trends and personally.

**Best**:

- You get a shot at changing lives.
- You work in an extremely high trust environment.
- You go through near death experience on a regular basis. As a result, you learn a lot about the world and yourself.

**Worst**:

- You go through near death experience on a regular basis. As a result, you learn a lot about the world and yourself.
- The whole game is very rigged on multiple fronts. Venture backed, next unicorn, infinite expectation on growth at the cost of everything else is the only kind we truly call 'startup' anymore.

> If I may ask further, what do you mean by game being rigged?

Value to customer is a much smaller part of a successful business than capital.
Once you've entered the investment cycle, you're always at the whim of the VC, at least in India.
Your competitors do unethical things, you are at a massive disadvantage if you do not.

> Everything seems like Silicon Valley season to me

Not watched the show, from the clips I've seen. Reality is way more chaotic and way less funny

> Silicon valley isn't funny either. :P

</details>

---

<details>

<summary>How hard was it to quit? What do you see from a co-founder? What should be the most important trait? And whom should you never make a co-founder? How was your first pitch (to VC/stakeholder/first customer) like? Did they tell you off or believed there is something in it? Will you startup again? What would be something you'd want to NOT do this time</summary>

**Very**. When we'd started Verloop, I'd said to myself that I'd see this through till the end. In some respects, I did, I guess.

**Trust and comprehension**. The amount of shit you'll go through over the course of the company. If I can't trust someone with my life, I can't work with them.
After MagicX, I pitched for more of an API aggregator approach. I was promptly shot down. Gaurav then pitched the B2B bot platform and it worked.

**I don't know yet**. If I were to, I'd probably do a section 8 company next. I'll probably not make a VC backed company unless I absolutely need to.

> What did you do after quitting?

Slept a bunch, cried a bunch, ate a bunch, went completely offline as much as I could.
Tried CBT thanks to a co-worker's advice. That helped a lot.
In parallel, started looking at climate change to get a broad idea. Dug slightly deeper into some areas. Looked at OSS projects as well.
Looked back at various things that happened and tried to deal with them.

> Other than sigh of relief? How has life been? Fast? Slow?

Healthier. Especially mentally. I'm now learning things that would have really helped 2-3 years ago!
I'm still catching up to life that I wasn't paying attention to while chasing the butterfly!

</details>

---

<details>

<summary>If you’d happen to become a founder/co-founder again in a for-profit, what would it be</summary>

Something around climate change/sustainability probably.
Some ideas I'm thinking of:

- Plant trees or putting up solar panels with CSR money.
- Launch an ad network which only allows sustainable products. As a matter of fact, you can kind of do that with any existing business model. Add sustainable as one restriction. You'll get better PR for some effort in curation.
  As long as you can find a business model where the delta in cost of customer acquisition can cover the additional effort you need to put in, it's like any other business. If you don't have VC breathing down to ooze every last rupee out of the business, you can do it for smaller margins and live/grow.

> Why did you leave

The one I usually give out in public is that I burnt out and left.
But to be honest there were multiple reasons, still not sure of their relative weight.
Part of it was emotional exhaustion, part was that I hadn't done things I like in a long time, only things that were necessary.
Part of it was that I wanted to do something more meaningful.
Then there are reasons that I am not comfortable sharing yet.
It's... complicated?

Verloop is very dear to my heart, and it felt more like walking out of a deep and long term relationship than quitting a job.

> Are you planning to move to sustainable.business?

I am not really planning anything yet. Just healing and trying to figure what I want to be in life.
Right now the overwhelming feeling is that I'd like to be an IC working in OSS and/or in climate change. If IC isn't possible, maybe I'll become a consultant and try opening a section 8 company. plans upon plans, backups upon backups

> Did you earn a lot of money?

No, I was at 50% paycut by market standards and I lost a big chunk of my stocks when I quit. Depending on how those stocks do, I'd have either lost money or made a little.
But that's way too much into the future. Right now, I'm just sad about the amount of tax I'll have to pay on the stock options that I need to exercise!

> Was that money worth spending X years of your life?

Not really, but then money was not the primary goal.
When we started, I wanted to chase an idea. Over time it changed to many things: work with some scale, learn a little about business, build a company I'd like to work with, give people a good work life balance, make a difference in the world, just be an IC.
Some panned out, some I gave up on, some are still ongoing.

> What is your advice for someone who is bored of it and has already put some years of his life into it but do not find it fascinating enough?

I am not sure what they've put their lives into. Maybe change? I can't say without knowing more. DM me if you want to talk.

---
