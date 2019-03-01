# Legacy systems

Legacy code is well-known in software engineering, generally what engineers call "legacy code" is synonym of "horror" or "do not touch!", but it can be characterized by the following traits:

- It's old code that has accumulated a lot of patches, fixes, stuff along the years
- It's daunting to code in that code just to fix an issue or evolve a features
- It started with engineers who are no longer with the company 
- The technology used is no longer state of the art
- To some extend, no one is really sure of this code works and what it really does (think edge cases)
- Performance slowly degrades
- ...

Legacy code can be visible as part of a product UI and generally you feel it's antiquated, but it can be invisble as part of a server-side service for example.
Now, in the eye of a business leader legacy code is synonym of cash cow (well, assuming the company is doing well). It may not be the most glamorous piece of software but it makes money and we want to milk it by squeezing it down to the last drop. it's in the maturity/decline phase of a product and there is little appetite to invest in this code. There is an exception when it's the UI itself: customers may start to not like it anymore but existing customers are generally incredibly sticky to old interfaces: they are used to them, they know the shortcuts, tricks and workarounds by heart and may not necessarily welcome any change (I am still amazed at the airport when I see agents using these old text-based black and green mainframe terminals. What's interesting too is that when they don't know what to do in a specific case, they always call the next agent who knows a trick such as "oh yes, just enter 0000 and move on to the XXXX field and type 123" and... it works!)

So there are three perspectives on legacy code: 
- the developer perspective, or in general the engineering/operations/support perspective - the DevOpS perspective
- the business perspective
- the customer perspective

Business wants this code to survive at a decreasing cost and DevOpS is claiming that costs cannot be reduced and may even increase.
Customers don't care until they find a disruptor that can show a much easier system to use. 
What do we do?

## Lost island

There are techniques to overhaul legacy code. One of my favorite is to chunk it into islands. If there is a lot of coupling, the legacy is it's single island and the only thing you can do, without spending too much, is to wrap it and plug a new UI on top of it. It's ugly, but this can give you enough runway to keep some distance with your disrupting competition. It's then up to the business to assess wether or not it's worth crack-opening the rest of the software. 

Here is a concrete example: assume you have an old product developped in the late 90s/early 2000 and it has a Web 1.0 interface: old forms, one click = a rountrip to server with a new page load. Widgets are old. The code by now if alsmot free of bugs. Say for example that this system is a payroll system. Now with new entrants like for example Payfit, you feel that your existing customers are close to switch to a full SaaS cheaper version than your old license-based (and possibly on-prem) product. 

I would argue that you can throw a new face to your system in simply wrapping all the old system access to modern REST-based type of APIs. You will have a two lane project:

1. APIs - the definition is pretty much set in advance, but you can imagine having some new code for a direct access to the database. Say you have about 20 API calls, this would cost you about 150 days of DevOps 
2. UI - now you can think of a modern UI. Say have about 50 significant pages in your system, you will now want to get a responsive single-page design UI following some known graphcial charts such as [Material Design](https://material.io). Your UI/UX design time may cost you a lot, but since you have the disruptor as a benchmark (and someone to copy), I'd argue that in a couple of months you should have a good [Sketch](https://www.sketchapp.com) for what you need and implementation with something like [React](https://reactjs.org) should not take more than a couple of months as well with a small DevOps team. Let's set a comfortable budget: something like 250 man days.

So in a period of probably four to five months, spending 400 to 800 man days, you can have what appears to be a brand new system on par with your competition. Even if my numbers are wrong - an we all know that estimations are always wrong - you have to bear in mind that something quick can be done to give a second life to your product. Your costs of operations will not increase much after that. And your gain is to stay in the game.

## Re-attach

Now in the long run, this frankenstein system I just described has to morph into something better. Better for what? Well, to be flexible enough to add new features and solve new problems for your customers. 
The good news is that your UI is now well architected and you have a clean decoupling with the back-end. Adding new "segments" should be state-of-the-art as it can be done separately from the legacy. 
The cancer in your system is still the legacy system. But now, you have a test harness: this API layer. Progressively you could re-write the legacy system or partition it in sub-islands and rewrite the most critical ones.

## Don't repeat

You've learned one lesson: software decays, people leave the company, and new recruits don't like cleaning others' legacy.
Once you have relifted your product, the one thing you don't want to do is to stay happy and let the same debacle happen again in a couple of years. 

- You want your DevOpS team to spend time learning new technologies, testing new frameworks and approaches so that they can stay on top of their game and your product shall evolve as well
- You want someone in charge of your system architecture. This is often ignored or undervalued, especially when teams self-proclaim them "Agile". System architecture is vital to keep a clean foundation. And yes, they can contribute to scrums as well
- You also want your business (Product team) to understand the dynamics of product cycles to learn from their customers what works and what does not. Going back to my example of airline systems, it may sound cool that some workarounds exist but this shows to me that the product manager in charge could care less.
There are use cases that need to be treated the right way. Your product should also report on how it is used (and there are many easy tools that let you do that, such as Appdynamics or Newrelic).