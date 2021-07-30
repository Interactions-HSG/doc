# Terminology and Tooling in Mutli-agent System (MAS)

Author: Iori Mizutani ([@iomz](https://github.com/iomz))

MAS [is a computerized system composed of multiple interacting intelligent agents](https://en.wikipedia.org/wiki/Multi-agent_system) to solve problems that cannot be solved by a monolithic approach.

The definition of intelligent agents varies between different approaches such as methodic, functional, procedural approaches, algorithmic search, or reinforcement learning.

In this note, I attempt to summarize the terminology and tooling used in one of the MAS approaches; procedural reasoning systems (PRS) based on the belief-desire-intention (BDI) model.

## AgentSpeak
AgentSpeak [[1]](#rao1996agentspeak) is a programming language to formalize BDI architecture for (cognitive) autonomous agents as anabstraction of one of the implemented PRS, and falls in the [logic programming](https://en.wikipedia.org/wiki/Logic_programming) paradigm with [horn-clauses](https://en.wikipedia.org/wiki/Horn_clause).
The file extention of AgentSpeak is `.asl` as in AgentSpeak(L).
Due to the nature of horn-clauses, it is difficult to learn the [operators](http://jason.sourceforge.net/api/jason/asSyntax/package-summary.html) and the [triggering events notations](http://jason.sourceforge.net/api/jason/asSemantics/Event.html#trigger) as shown below.

![Types of triggering events (from [2])](https://user-images.githubusercontent.com/26181/127559545-e6d66fde-ac21-4ada-865a-f28568c37145.png "Types of triggering events (from [2])")


## [Jason](https://github.com/jason-lang/jason)
Jason is an interpreter implemented in Java and the language interpreted by Jason is an "extended version" of AgentSpeak [[2]](#bordini2007programming) – the extension includes user-defined components (e.g., [__internal actions__](http://jason.sourceforge.net/api/jason/stdlib/package-summary.html)) programmed in Java.
For this reason, Jason is often used to also refer to the extended language.
Jason initially stood for "Java-based Agentspeak interpreter used with Saci for multi-agent distribution Over the Net", but it is not based only on SACI anymore.

It is important to notice that the user-defined components in Jason are bound to the Java ecosystem and this constrains AgentSpeak in terms of JVM, tools, IDEs, etc.
[`python-agentspeak`](https://github.com/niklasf/python-agentspeak) is an alternative for AgentSpeak interpreter, and customized actions can be written as [Python code in an analogous way to Jason](https://github.com/niklasf/python-agentspeak/blob/master/agentspeak/ext_stdlib.py), for example.
Meanwhile, [Embedded-BDI](https://github.com/Embedded-BDI/embedded-bdi) translates AgentSpeak code to a corresponding C++ header using the Jason parser.

## [JaCaMo](http://jacamo.sourceforge.net/)
JaCaMo is a MAS framework that is rooted in the [JaCa programming model](http://jacamo.sourceforge.net/?page_id=40) which is designed and programmed as a set of agents which work and cooperate inside a common __environment__.
In JaCa, Jason is adopted to program the agents, and CArtAgo as the framework to program the __endogeneous__ environments (which are mapped to the __exogeneous__ (physical) environments) for those agents.
The autonomous BDI agents in JaCaMo MAS are organized by Moise.
Hence, JaCaMo is a hierachical MAS framework consisting of three levels: organization (Moise) -> agents (Jason) -> environments (CArtAgO).
All the (major) implementations for the three levels are in Java, so the researchers and developers need to be familiar with Java.
JaCaMo also provides a platform (i.e., the Swing-based GUI called "MAS Console" with the Eclipse plugin) for the development of multi-agent systems integrating the three levels, but also as a command-line script to execute `.jcm` files which contain [coordination](http://jacamo.sourceforge.net/tutorial/coordination/) parameters.

## Artifiact
__Artifacts__ in the context of JaCaMo are the basic computational bricks defining the environment structure and behavior, representing those resources and tools that agents can create, discover, perceive, and use at runtime.
Each artifact provides __operations__ and __observable properties__ defining an artifact’s _usage_ interface, used by agents to observe and operate on artifacts.
Operation execution could generate updates to the observable properties and specific __observable events__. [[3](#boissier2013multi-agent)]
Together with agents, Agents & Artifacts (A&A) is based on interdisciplinary studies involving [Activity Theory](https://www.interaction-design.org/literature/book/the-encyclopedia-of-human-computer-interaction-2nd-ed/activity-theory#:~:text=Activity%20theory%20is%20a%20conceptual,world%20(%E2%80%9Cobjects%E2%80%9D).) and [Distributed Cognition](http://edutechwiki.unige.ch/en/Distributed_cognition#:~:text=Distributed%20cognition%20refers%20to%20a,agent%20could%20not%20achieve%20alone.) as main conceptual background frameworks.
Concretely, an example of an artifact is a Java class instance implemented with CArtAgO's [`Artifact` abstract class](https://sourceforge.net/p/cartago/code/HEAD/tree/cartago/trunk/src/main/cartago/Artifact.java).

## Manual
__Manual__, formally artifact manual, represents the description of the operations, observable properties, and observable events provided by an artifact.
These can be mapped well with the interaction affordances in the [W3C Web of Things Thing Description](https://www.w3.org/TR/wot-thing-description/).

## [CArtAgO](http://cartago.sourceforge.net/)
CArtAgO stands for Common ARTifact _infrastructure_ for AGents Open environments and is used to program the virtual, endogeneous environments for the agents in a MAS. 
CArtAgO programs artifacts for the endogenous environments whose topology is described as __workspaces__, where arbitrary agents can join and work together with each other.
Each workspace contains a dynamic set of artifacts and multiple workspaces can form a __workspace environment__.
CArtAgO is meant to be orthogonal to the specific agent model or platform adopted to define agent architecture and behavior.
However, [the actualization of CArtAgO](https://sourceforge.net/p/cartago/code/HEAD/tree/cartago/trunk/src/main/cartago/) is a Java library that allows developers to program the artifacts of the endogenous environments in Java.

## MOISE
Originally, the MOISE (Model of Organization for multI-agent SystEms) is structured along with three levels: (i) the behaviors that an agent is responsible for when it adopts a role (individual level), (ii) the interconnections between roles (social level), and (iii) the aggregation of roles in large structures (collective level). [[4](#hannoun2000moise)]
These __organizational specifications (OS)__ are to be used both by the agents to reason about their organization and by an organization platform that enforces that the agents follow the specification.
The population of agents functioning under an OS is called __organizational entity (OE)__.
Later, MOISE+ [[5](#huebner2002model)] was developed to build (i) as __roles__, (ii) as __(role) relations__, and (iii) as __groups__ with concepts such as inheritance, compatibility, cardinality, and sub-groups.
[The Moise implementation](https://github.com/moise-lang/moise) is a Java library that adopts MOISE+ to describe the OS/OE for MAS.

## [FIPA](http://fipa.org)
The Foundation for Intelligent Physical Agents (FIPA) is an international organization that is developing specifications for interoperability among intelligent agents.
The [FIPA Request Interaction Protocol](http://fipa.org/specs/fipa00026/SC00026H.html), for example, is a standard for request interactions among agents.
It is noteworthy that this _protocol_ standard only defines the flow of interactions as a meta-model.
The [separate specifications](http://www.fipa.org/specs/fipa00067/) define the _message transport services_, and [HTTP can be the transport protocol](http://www.fipa.org/specs/fipa00084/SC00084F.html#_Toc26670761), for example.

## [Yggdrasil](https://github.com/Interactions-HSG/yggdrasil)
Yggdrasil is a platform for Hypermedia MAS [[6](#ciortea2018engineering)] built with [Vert.x](https://vertx.io/), a tool-kit for building reactive applications on the JVM.
The Hypermedia MAS provides the concrete interactions among heterogeneous agents in a distributed  _hypermedia environment_.
The environment in a MAS is a __first-class abstraction__ with dual roles: (i) the environment provides the surrounding conditions for agents to exist, and (ii) the environment provides an exploitable design abstraction for building MAS applications. [[7](weyns2007environment)]
To this end, IRIs of the W3C WoT TDs are instantiated as _Browser artifacts_ in the hypermedia environment in Yggdrasil which can then be interacted by agents as they would interact with artifacts in a CArtAgO workspace.
TD's protocol bindings allow the operations to be seamlessly mapped in the exogenous environments, and thus a hypermedia MAS realizes an agent-oriented organization of cyber-physical systems.

## References

[<a name="rao1996agentspeak">1</a>] Rao, Anand S. "AgentSpeak (L): BDI agents speak out in a logical computable language." European workshop on modeling autonomous agents in a multi-agent world. Springer, Berlin, Heidelberg, 1996.

[<a name="bordini2007programming">2</a>] Bordini, Rafael H., Jomi Fred Hübner, and Michael Wooldridge. Programming multi-agent systems in AgentSpeak using Jason. Vol. 8. John Wiley & Sons, 2007.

[<a name="boissier2013multi-agent">3</a>] Boissier, Olivier, et al. "Multi-agent oriented programming with JaCaMo." Science of Computer Programming 78.6 (2013): 747-761.

[<a name="hannoun2000moise">4</a>] Hannoun, Mahdi, et al. "MOISE: An organizational model for multi-agent systems." Advances in Artificial Intelligence. Springer, Berlin, Heidelberg, 2000. 156-165.

[<a name="huebner2002model">5</a>] Hübner, Jomi Fred, Jaime Simao Sichman, and Olivier Boissier. "A model for the structural, functional, and deontic specification of organizations in multiagent systems." Brazilian Symposium on Artificial Intelligence. Springer, Berlin, Heidelberg, 2002.

[<a name="ciortea2018engineering">6</a>] Ciortea, Andrei, Olivier Boissier, and Alessandro Ricci. "Engineering world-wide multi-agent systems with hypermedia." International Workshop on Engineering Multi-Agent Systems. Springer, Cham, 2018.

[<a name="weyns2007environment">7</a>] Weyns, Danny, Andrea Omicini, and James Odell. "Environment as a first class abstraction in multiagent systems." Autonomous agents and multi-agent systems 14.1 (2007): 5-30. 
