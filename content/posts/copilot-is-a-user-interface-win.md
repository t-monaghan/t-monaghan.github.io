---
date : '2025-03-08T09:38:05+11:00'
title : 'Copilot is a user interface win'
---

Listening to Dario Amodei talk about AI as a product on the Hard Fork podcast helped foment some questions that have been following me around. I’m keen to use this post to start exploring these thoughts I’ve had around AI product usability, confidence and the future of AI service providers.

Here’s the quote from Dario that stirred this all up for me:

> *“I think one area where the models will be good enough is if you’re just trying to use this as a replacement for Google Search or as a quick information retrieval … but I don’t think those are the interesting uses of the model. And I’m actually not sure a lot of the economic value is there.”*

This had me consider just how complex the questions I ask these models are.

In my day to day work I interact with LLMs via GitHub Copilot, and I would say that in my experience Copilot serves me best when I’m asking these simple queries that Dario is dismissing. For example, I’m often clarifying the syntax of a language or looking for what might be a more idiomatic usage of a certain library. The value Copilot provides me for these queries is instant: a simple, text response right next to my work. Here the information meets me where I stand and I don’t have to reach out and navigate the web.

This product could feasibly be built without the use of AI, and the differentiator isn’t necessarily driven by AI functionality, but rather in the UI and reliability of the integration. I’d even bet that a Copilot “like” product built without AI would have more contemporary sources in a way the current LLM models do not. I remember trying to get Copilot to make suggestions in regards to Go’s structured logging package early last year. This experience had me pulling my hair, the library was freshly released and as a result the recommendations were consistently incorrect. This was due to the LLM’s training being done prior to the release of this package and it’s documentation. This is not an uncommon experience for me.

In these cases it was obvious the AI did not have the context it needs to proceed, but it was very willing to confidently lead me down the wrong path. Here I was wishing that the models would prod me for more context, but they never did. I have not noticed a step-change improvement in this area, in spite of the current conversation around LLMs and reasoning.

Considering the technology that underlies an LLM, how could it possibly prod me for more context? To achieve this it would require a sense of confidence in it’s answer. If this sense of confidence were available to LLMs, they would surely be designed to optimise for this, making use of this confidence in a way that allows for the kind of revolutionary growth which I haven’t noticed since GPT-3.

I’m curious about the future of the current LLM providers. I’m wondering if they will continue to operate as service focused companies in the long term, or pull the rug out from under those that depend on these services to reduce competition in their products’ market. Those that are best delivering these products are the service providers, but if we don’t see a diversification in LLM products, why should the big providers continue to provide services to their competitors? The current market seems to have the makings of a maelstrom. Microsoft, heavily invested in OpenAI, offering Anthropic’s Claude via Github Copilot.

Could this be the new norm of collaboration between large competing providers? I doubt it. My instinct is that if we don’t see serious product diversification the big players will insulate themselves against the risk of providing the best models to those who challenge their product.

Thanks for reading, I’d be keen to hear any thoughts you might have on this subject. If there’s something you’d like to share you can leave a comment on [my LinkedIn post for this piece](https://www.linkedin.com/posts/tfmonaghan_copilot-is-a-user-interface-win-activity-7304316665767284737-VdGF/).
{{< callout type="custom" emoji="🕖" title="Hard Fork Podcast" text="Here is the episode of Hard Fork that contains the quote from above, the question that Kevin Roose asks that prompts this response from Dario occurs at 19 minutes and 10 seconds" style="background-color: transparent; border: 3px dotted#9fe368;" >}}
\
{{< youtube YhGUSIvsn_Y >}}
\
{{< callout text="Post Script: As I was preparing to post this I came across some discussion that resonated with my thoughts on this topic." >}}

The discussion started with [this piece written by Thane Ruthenis](https://www.lesswrong.com/posts/tqmQTezvXGFmfSe7f/how-much-are-llms-actually-boosting-real-world-programmer) questioning the impact LLMs have had on real-world programmer productivity, [and a comment in the discussion](https://news.ycombinator.com/item?id=43304384) of this article on Hacker News. Below is a portion of the comment that helped crystallise some of what’s been floating around in my head.

> *"… another vibes coding anecdote about another CRUD app or a bash script with tricky awk is just not really what (the article) is asking about. That is just evidence that LLMs have finally fixed search, which is great, but not the subject that we’re all the most curious about."*

I also want to thank Jason O’Neil who I have the great pleasure of working with for proof reading this for me. I
was inspired to start a practice of writing after reading his blog which you can find at https://jasononeil.au/.
