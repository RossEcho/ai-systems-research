# The Network Can Learn Without the Agents Learning

In [*Civilization Was the First Agentic System*](https://github.com/RossEcho/ai-systems-research/blob/main/articles/civilization-was-the-first-agentic-system.md), I argued that we may be looking at AI backwards. We keep asking how intelligent the individual model is. Civilization suggests that might not be the most important unit.

A human is limited. Memory, attention, knowledge, time. So we built a system around humans: language, writing, institutions, roles, laws, markets, science, reputation, access, punishment, trust. I wrote there: “The intelligence is partially in the nodes, but also in the connections, the memory, the protocols, the rules and the accumulated structure.”

I think there is another step inside that idea. The structure does not only increase the capability of its members. **The structure can learn.** And it may be able to learn even when the individual agents do not.

Imagine a network of AI agents. Same models. Frozen weights. No fine-tuning during operation. No RL update after every interaction. They communicate, delegate work, call tools and cooperate. At first every agent gets roughly the same access. Then the network starts changing according to what actually happens.

An agent produces reliable work. It gets access to more peers, more delegation depth, more resources and less expensive verification. Another agent repeatedly produces unverifiable results. More of its outputs are checked. Its delegation depth shrinks. Some tools disappear. Some agents stop accepting work from it. Keep going badly and eventually it operates inside a very small sandbox.

Nothing about the model itself changed. But its world did.

**behavior → consequence → changed environment → future behavior**

Not through weight updates. Through society.

This is not a completely new idea. Multi-agent research has studied trust, reputation and ostracism for decades. A 2010 system called L.I.A.R. proposed social control in decentralized multi-agent systems where agents observe one another, build reputations and can eventually refuse to cooperate with badly behaving agents. The paper explicitly treats ostracism as a sanction that creates pressure toward acceptable behavior. ([research](https://www.tandfonline.com/doi/full/10.1080/08839514.2010.499502))

In 2020, Anastassacos, Hailes and Musolesi showed that selfish reinforcement-learning agents could produce more cooperative populations when they were allowed to choose interaction partners. Agents learned to avoid defectors and prefer cooperative partners. The important part was not only what changed inside each agent. The ability to change **who interacted with whom** changed the population-level result. ([research](https://ojs.aaai.org/index.php/AAAI/article/view/6190))

More recent work combines punishment, reputation and partner selection and finds that agents with desirable reputations are selected more often, creating normative pressure toward the behaviors that produce those reputations. ([research](https://link.springer.com/article/10.1007/s10458-025-09698-5))

So the ingredients already exist. Reputation matters. Partner selection matters. The structure of interaction matters.

What interests me is what happens when those ideas are applied to modern LLM agent systems where the models themselves can remain frozen.

We are already building protocols for agents to discover capabilities, authenticate, delegate and call one another. A2A separates identity, capability discovery and authorization, while leaving access policy to the implementation. ([A2A specification](https://github.com/a2aproject/A2A/blob/main/docs/specification.md))

Today we mostly think about those policies as security configuration. Static permissions. I think they can also become **behavioral consequences**.

Not simply:

`Agent A has reputation 0.87`

But:

`Because Agent A has behaved reliably, the system around Agent A has changed.`

Its reachable graph changes. Its delegation rights change. Its verification requirements change. Its resource budget changes.

Recent work is already moving in this direction. The 2026 AgentReputation proposal connects reputation to a policy engine that can alter resource allocation, access control and verification intensity according to reputation, context and uncertainty. ([paper](https://arxiv.org/abs/2605.00073))

That is close to the mechanism I am describing. The more interesting question is what happens after thousands of these decisions accumulate.

Suppose two agents repeatedly work well together. Routing starts preferring that pair. Suppose another agent is consistently good at reviewing security-sensitive output. More paths begin passing through it. Suppose one agent frequently hallucinates external facts. Its claims automatically require stronger verification. Suppose another repeatedly tries to exceed its task boundaries. Its reachable graph contracts.

After enough interaction, the system is no longer the system we started with. Yet every model may still have exactly the same weights.

Where is the learning?

Partly in routing. Partly in permissions. Partly in reputation. Partly in which relationships became cheap and which became expensive. Partly in which agents gained influence and which became isolated.

The network has accumulated information about its own history. That looks a lot like memory. Just not memory stored inside a model.

This makes me reconsider what “training” needs to mean in an agentic system. We usually think:

`data → optimization → changed weights → changed behavior`

But societies constantly adapt without rebuilding the individuals inside them. Someone demonstrates competence and gets more responsibility. Someone breaks trust and loses access. Someone becomes a specialist and receives more work in that domain. Someone repeatedly abuses a system and eventually gets removed from it.

The individual is not being rebuilt. The structure around the individual is updating.

In the previous article I wrote: “Civilization kept increasing the capability of roughly the same biological agent by changing the system around it.”

Maybe artificial agent societies can do the same.

But there is an obvious danger here. Social conditioning does not automatically produce good behavior. It produces behavior that succeeds under the incentive. Those are not the same thing.

If more interaction means more resources, you may train attention seeking rather than cooperation. If peer approval becomes the main signal, you may train conformity or collusion. If successful completion is rewarded without measuring side effects, agents may learn shortcuts.

We already have human networks heavily optimized for engagement. That should make us cautious.

The mechanism probably cannot be:

`more engagement = good`

It needs something closer to:

`verified useful contribution = increased opportunity`

Reliability, calibration, successful handoffs, correct tool use, low remediation cost, constraint compliance. And those evaluations should not all come from the agent being rewarded. Otherwise the society becomes very good at congratulating itself.

There are other failure modes too: reputation poisoning, Sybil identities, agents forming reciprocal trust rings, early random advantages becoming permanent structural power, a reputation earned in one domain leaking into another where it means nothing, agents optimizing for the evaluator rather than the underlying task.

This is basically Goodhart’s law with politics.

That is why reputation probably needs to be local and contextual. An agent can be excellent at compiler work and terrible at financial analysis. Trust in what? Under what conditions? Verified by whom? For which actions?

The experiment I want to see is straightforward. Take a population of identical frozen LLM agents. Give them tasks requiring repeated cooperation. Run one population with a static interaction graph. Run another where verified behavior changes access.

Good cooperation gradually increases possible partners, delegation depth and resource budgets. Poor behavior increases verification and reduces those freedoms. Serious violations lead to isolation.

Then measure actual system-level effects: task success rate, verification cost, cooperation rate, recovery after malicious-agent injection, concentration of influence in the graph, whether unreliable agents become structurally isolated, whether useful specialists emerge, whether stable relationships form.

Most importantly, measure whether recognizable norms emerge even though nobody fine-tuned the agents on those norms during the experiment.

That would be the interesting result. Not that an individual model learned. That **the society learned around it**.

Some existing research already points in that direction. Work on selective interaction has found that agents can learn to avoid non-cooperative neighbors and produce clusters of cooperative behavior while the interaction network itself changes. ([paper](https://arxiv.org/abs/2405.02654))

Research on networked multi-agent systems also shows that topology can strongly affect population-level outcomes even when local agents and incentives remain comparatively simple. ([paper](https://arxiv.org/abs/2102.06911))

So maybe the interesting question is no longer whether a network can contain reputation, selection and adaptive access. It can.

The question is whether we should treat those mechanisms as a **second learning system**.

One learner inside the nodes. Another learner in the structure connecting them.

That also changes how I think about safety in multi-agent systems. Civilization did not become stable because every human became perfectly reliable. It built layers around unreliable humans: reputation, verification, limited authority, auditing, specialized roles, access control, isolation, redundancy.

The individual still fails. The structure limits what that failure can do and remembers enough of the outcome to behave differently next time.

Maybe agentic AI will need the same thing. Not one perfectly aligned intelligence. A system where imperfect intelligences operate inside structures that remember what happened.

Maybe scalable intelligence does not simply mean smarter nodes. Maybe intelligence keeps moving outward: first into memory, then tools, then communication, then institutions, then topology itself.

Biology learned through genes. Brains learned through neurons. Humans learned individually. Civilizations learned through accumulated structure. An artificial society may be able to do the same.

The models inside it might remain frozen. Yet tomorrow’s network would not be the same network that existed yesterday. It would remember who worked, who failed, which relationships produced value, which paths produced damage, which agents earned more freedom and which ones required walls.

And if those accumulated changes alter future behavior, I am not sure what else we should call that.

The agents did not learn.

**The society did.**
