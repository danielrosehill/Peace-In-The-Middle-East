# PIME Ideas - Cleaned Transcript

**Date:** 3 December 2025
**Source:** pime-ideas-notes.mp3
**Transcription:** Edited and organized

---

## Introduction

I'm recording some notes to give a little bit of an outline to this repository. I'm going back through some of the projects I've been working on for a while now, adding these notes and transcribing them to quickly provide some point-in-time information faster than I can type it, about what these exciting AI ideas are working towards.

Today is the 3rd of December 2025, the 14th day of the month of Kislev according to the Hebrew calendar.

---

## Project Overview

This is a repository called "Peace in the Middle East", a tongue-in-cheek name because that's something we all aspire towards. The peoples of this region aspire towards a more peaceful, prosperous, and stable Middle East.

The idea occurred to me because I was chatting with a guy called Mike Taylor who wrote a book - actually the first AI book I bought - an excellent O'Reilly publication called something like "Prompt Engineering for Generative AI." He has a startup called Ask Rally that brings to life an idea I've thought for a while is incredibly powerful: creating simulated panels based upon AI agents.

For example, you could bounce your ideas and philosophies off Aristotle or different representatives of different philosophical schools. They've made this idea more robust through interesting calibration mechanisms using actual real people to make the proxies more realistic and accurate.

---

## Repository Setup

Before setting up the panels (which require creating an audience and writing system prompts), I knew that wasn't feasible to do manually. So I created a repository with a few ideas for panels I thought would be really interesting. That was repository one: "Rally Panels" - that's for me to use when actually testing the platform.

Then I thought: this idea could be implemented for everything from municipal politics to social problems. Why not create a starting workspace for leveraging this approach on a really stubborn, thorny, intractable issue? The one that came to mind immediately was peace in the Middle East and the peace process here. I live in Jerusalem.

---

## Experiment Design Philosophy

I want to be very clear: this is just an idea to see if it might have any utility. I would never claim that all the people who've been trying to figure out the Middle Eastern peace process for 30 years are wasting their time and that I just figured it out with AI in a few hours. Clearly that's not going to happen.

But for the experiment to have any potential utility, I wanted to set it up in a way that encompassed the complexity of the problem.

### The Complexity of the Middle East

We have all these different groups, interdependencies, and webs:
- The influence of Iran upon proxies in Lebanon
- Internal tensions within Lebanon between the LAF trying to demilitarize
- Gaza: no one seems to have ideas for how to carry the ceasefire through to Hamas being demilitarized
- The international community seems stuck

From the vantage point of the majority of peaceful people in the region who want a more normal Middle East with more cooperation, more prosperity, and less war: could we simulate dialogue that is realistic?

---

## Agent Design: Avoiding Impersonation

The mechanism I was exploring: AI agents can have a system prompt that defines their behavior. I don't want to have Benjamin Netanyahu personified as an AI agent. That approach would risk being ethically problematic with impersonation complications.

Instead, like what Rally is trying to do, I want personalities that are described in the third person: "a Likud politician whose views are hawkish on this, dovish on that, policies are this." Creating agents that are shadows of the real political landscape in a certain geography.

---

## Summit Model

Summits connote a point-in-time political forum. This experiment would be useful if you could dip into it:
- "This development has happened. How does the summit react?"
- "Lebanon, what do you make of this?"
- "Jordan, do you have anything to say?"
- Then take minutes from it.

### Why UN-Style Procedures Work Well for AI

When thinking about how real political fora work - the UN forum, drafting resolutions, voting, gathering responses, documenting in official journals - I realized it's actually a very useful system for AI simulation because it's very rigid:

- **Resolutions as inputs**
- **Votes**: binary data (structured output)
- **Statements**: long-form text data
- **Summaries**: gathered in official journals

The whole process lends itself really well to geopolitical simulations.

---

## Use Cases

### Government/Foreign Affairs
If someone wanted to spin off this idea for a foreign affairs body or government: "If we propose this, how will other countries likely react?" Propose a resolution to the AI chamber, have them vote, create a podcast based upon three-minute speeches from each member. This could be a really cool mechanism for exploring blind spots in policy formulation debates.

### Personal Interest
As someone living in Jerusalem, not working on behalf of the state, what interests me is: how can we work around the extremists? How can we see a more prosperous Middle East?

Jerusalem is particularly pertinent - a city split between Palestinian East Jerusalem and Israeli West Jerusalem, with differences of allegiance to state, but nevertheless trying to find common ground.

---

## Inclusive Representation

It was important for the design to include everyone. In the Middle East, that's a lot of people.

### State Actors
Typically at diplomatic forums, you have permanent representation to the UN - a diplomatic mission staffed by diplomats. The Prime Minister might address the body but isn't living at UN headquarters.

In our fake agent world, we don't have that constraint. The diplomatic mission can actually be the executive branch: Prime Minister, President, Foreign Affairs, all the head honchos, the judiciary. We could listen in on their internal debates without eavesdropping. The Israeli delegation could be "thinking" and we'd see how the various inputs were processed.

We'd have:
- Actual modeling on real diplomacy
- Diplomats engaging with the policy forum
- Closed-door discussions between state representatives

### Other Groups
- Minorities in the Middle East
- Archetypal personas (tech optimists who think prosperity will end violence)
- Radicalized elements: Hamas, Islamic Jihad, Hezbollah, IRGC, Qatar
- Syria: rebels, loyalists (the Israel-Syria dynamic is super complex)
- Within Israel: differences between IDF, Foreign Affairs, and government
- Saudi Arabia

---

## Technical Considerations

### Up-to-Date Information is Critical
This is where experiments like this fall down rapidly. You need up-to-the-day knowledge because dynamics move so quickly. The knowledge base of the agent pool has to be up to date.

From an AI engineering standpoint, this is tricky. The best solution is that the LLM backbone of the agentic experiment has to have real-time capability baked in.

You can add real-time information through tools like Tavily or Perplexity, but that's very impractical when an assembly of 50 sub-agents votes on a resolution. None inherently have real-time information, so every single one needs to use the MCP - which means 50 parallel MCP calls. It gets messy.

### Model Selection
It's tricky to determine what's best:
- Generating a lot of text
- Need cost efficiency
- But compared to the cost of hypothetically bringing these groups together, it's peanuts

**Cost-constrained environment**: Hard to find a model that's cheap for text, good for reasoning, and has real-time or near real-time info. OpenRouter is my go-to for having a bunch of models available.

**Non-cost-constrained environment**: Use the very best models. For reasoning combined with agentic capabilities, I'd regard Anthropic's models - 4.5 Opus - as the gold standard. Built-in real-time data, good reasoning, good agentic stuff.

---

## Previous Experiment: Agent UN

I did one run of an "Agent UN" - an idea that occurred to me one morning (like a lot of these GitHub repositories). I started with the UN General Assembly, then said why not just do the UN Security Council - fewer states.

For the UN Security Council:
- Looked up who's on the UNSC
- Looked up their internal procedures
- From an agentic standpoint, it's perfect source material: tightly defined voting procedure, veto procedure
- Kind of easy to replicate in code using LangChain or Claude Code

When you don't even have to write Python scripts, it makes it so much easier to iterate and try stuff.

---

## Example Use Case: Rebuilding Gaza

Let's talk about the process of rebuilding Gaza - a very important topic and acute issue. Hugely complex:
- Hamas forcing their way back into power
- Elements of the population resistant to it
- US nudging for ceasefire but not putting boots on the ground
- International community asked to deploy but not enthused
- PA observing from afar

We would need a very broad pool of agents. And this is why Hamas has to be at this table, even if... Israel and Hamas only talk to each other in real life via Egypt or intermediaries. That could be baked into the experiment design:
- **Rule**: The Israeli delegation and Hamas do not communicate directly
- **If Hamas and Israel are to dialogue**: Use Egypt as the intermediating agent

---

## Next Steps & Analysis

We might choose a few different panels:
- One very wide panel
- One very narrow panel

Ask them to agree on a resolution. Is there any way that can happen? Very tall order. Then proposals.

### The Analysis Layer

We start with a massive glob of text - each participant writes an essay, much as happens in the UN with long speeches. Then the second phase: we've gathered this corpus of text and opinions from synthetic personalities. How do we translate that into actionable or useful information?

This is where agentic frameworks can be brilliant, processing all that context:
- "This is what we got from the virtual sitting of the forum today"
- "Can you identify any novel ideas here?"
- "Is there anything in what the various parties have said where you can see opportunity for peaceful alignment and consensus?"
- "Anything that hasn't been floated before?"
- "Compare what the summit thought about with what's being reported in media from Reuters and reputable sources"
- "Can you see anything the real world just didn't consider?"

That would be amazing.

---

*End of notes.*
