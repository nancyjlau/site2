---
title: Notes on Autonomous Security
description: notes for autonomous cyber response workshop
slug: workshop-1
date: 2024-03-11 00:00:00+0000
categories:
    - notes
---

## Opening Remarks
- Need for automating incident response
	- Security analysts are overloaded w/ alerts and information
		- One such issue are obscure alerts
	- Human operators have slow response
	- Promise of AI for automating response
		- Fast, scalable
		- Novel defense strategies (similar to AlphaGo, AlphaZero)
## Reinforcement Learning for Autonomous Cyber Defense

**Reinforcement Learning**
- train agents to learn optimal sequential decision making skills to achieve goal under uncertainty
- real world environments, such as cyber, are dynamic, partial observable, and adversarial
- effective agents learn to generalize policy across different tasks and scnearios
	- How much generalization is required?
	- How much human trust is necessary?
## Toward Autonomous Cyber Defense (MITRE)

FARLAND
- https://arxiv.org/pdf/2103.07583.pdf
- https://arxiv.org/pdf/2310.13565.pdf

The goal of FARLAND is to mitigate cyber attacks at scale by pursuing autonomous network defense that is robust against evolving cyber-attacks and environments.

Challenges
- Emerging threat
	- Dealing with an AI enabled adversary with evasion and poisoning capabilities
- AI for security
	- Develop a machine learning approach to implement autonomous defense
- Security for AI

Motivating example: 
- Traditional red TTP (Tactics, Techniques, Procedures) for exfiltration
-  Red agent without blue actions

Applying RL to Cyberdefense
Key Idea 1: Train via a universe of tasks
- Network defense tasks as a collection of "games" with uncertain and possibly drifting rules.
- Define probability distributions over network environments that capture diverse adversarial TTPs
- Open-ended learning for autonomous cyber defense
	- Similarities with Open-ended Learning (OEL) and Automatic Domain Randomization (ADR) (OpenAI, 2019)

Fundamental Problem: Network Defense is not a single game with fixed rules

Key idea 2: Single Abstraction for Simulation & Emulation
Subgoals
	1. Validate policies learned via simulation through emulation
	2. Improve simulation models with data captured via emulation

Fixed vs dynamic task selection
-  Fixed task selection only trains at the most difficult level, encoded in the color map

Toward robustness
- The "universe of tasks" approach results in some tolerance to red agent behavior deviation
- In this case, the red agents "morph" their behavior with some probability using the RL algorithm PPO

OEL for autonomous cyberdefense
- Training RL-based defenders for increasingly realistic networks
- Broad universe of defense tasks to achieve robustness

Q&A
  - Factors considered: Numbers of red teams, hosts in networks, traffic to users, TTPs
  - Blue agents not only monitor but also reconfigure the network for intrusion detection and mitigation, taking active actions

How does the simulation/emulation interact with each other in FARLAND?
- The interaction between simulation and emulation can be thought of as a set of API actions that can be performed by each of the agents: blue (defending), gray (neutral), and red (attacking).
- These API actions map to different behaviors, such as sending a file inside the network. The actions performed in the emulation environment can then be remapped to corresponding actions in the simulation environment.
- The researchers use Software-Defined Networking (SDN) to effectively define and translate these actions between the simulation and emulation environments.
## Ups and Downs with Autonomous Cyber Response Research
- Goal: Transition from human analysts to fully autonomous systems

Human Analysts -> fully autonomous would be cool

Does RL Produce an Effective Defender?
- TTCP CAGE Challenge
- Using CyBORG to evaluate RL for cyber defense

CAGE Challenge 2: Models

- Building on the success of Proximal Policy Optimization (PPO)
- Approaches:
    - Highly tuned PPO
    - Transfer Learning
    - Action Masking
    - Hierarchical PPO
    - Ensemble
    - Multi-Ensemble

Competition reuslts
- 16 total entries from 8 teams

Real-world Misalignment
- Question: What if the simulator doesn't match the production environment?
- Production Network vs. Agent Training: Simulation
- Notes:
    - Tested the model's performance in real-world environments
    - Significant drop in performance, 2-3x worse compared to the models in the competition when applied to 3 real-world environments


Examining Transfer Learning in CyberBattle Simulation
- Additions:
    - Defender interface + noise
    - New tabular Q-learning agent
    - Baseline defense agents
    - New environments/networks
    - Additional defender actions
    - **Abstract observation spaces**

Challenges with using RL for Cyberdefense
1. Autonomous Simulation
	1. We need to know exactly what's on a network to interact with it. It would be great if we could do it passively and then in a simulator, but there isn't enough work for this to have promising uses
2. Robust Transfer Learning
	1. Hard problem to solve
3. Enterprise Rewards
	- Working with a complex enterprise environment is time-consuming
	- Difficult to determine the best course of action

## Using LLMs to Automate Incident Response

LLM Experiment #1: Generating Bash Commands from Language

- Dataset: 2020 NLC2CMD NeurIPS Workshop data + evaluation metric
- Results:
    - Majority of off-the-shelf LLMs were not competitive
    - Fine-tuning helps, but not all fine-tuned models outperform the baseline
    - The winning model outperformed the baseline
Key takeaways:
- Good dataset and fine-tuning can help generate effective Bash commands

LLM Experiment #2: Classifying ATT&CK Techniques
Goal: Identify ATT&CK techniques in unstructured text

LLM Experiment #3: Automated Query Generation
- Goal: Help analysts perform threat hunting
- Approach: Used Retrieval Augmented Generation (RAG)
- Reception: Fairly positive

Challenges with Using LLMs for Security
1. Data, data, data
	- High quality finetuned data is much more important !!!
	-  Query classification, bash command generation
1. Measuring Performance
	1. How do we know if one bash command isn't the right bash command given natural language?
		- actual command vs generated command
			- Actual command vs. generated command: Hard to measure because sometimes the generated command achieves the same result as the actual command but in a different way

Discussion Points
- There's a gap between theoretical RL for autonomous cyber + real
	- Can we autonomously create accurate network maps/simulators?
	- Can we modify existing RL approaches for simulator inaccuracy?
	- How do we define reward functions for enterprise environments?
- Using LLMs shows promise — but there's more work needed
	- Doesn't escape the classic ML-needs-data problem
	- Coming up with solid evaluation criteria is *very hard*
	- *Can we ever feel confident enough to have LLMs operate autonomously?*
Q&A
- tried traditional n-gram style comparisons but got completely wrong commands that looked okay but were entirely incorrect; very hard to do
- fine tuning LLMs not very hard 
## Securing AI and Cyber Security Agents

Automating cyber incident response with AI **requires** robustness to adversarial environments
- Robustness in context: system security vs component security
- Are AI attacks really happening?
- Beyond prompt injection
- Planned Obsolescence

Robustness in Context
System Security
- Reference architecture variations make it difficult to generalize conclusions and identify meaningful performance metrics
- Emergent behaviors from chained impacts (e.g., the Dominion effect/Google's C++)
- Industry needs skew towards this side of the spectrum
vs.
Component Security
- Experiment tests isolated components for the effect of systematic perturbations
- Identifies first-order effects
- Easier to describe performance metrics
- Academic research skews towards this side of the spectrum

Are AI Attacks Really Happening?
- The C-suite race to adopt AI to compliant safety standards when standards don't exist

What is happening?
- the court of public opinion

What is not happening?
- security research on traditional software has established voluntary protections from companies ("safe harbors"), clear norms from vulnerability disclosure policies, and legal protections from the DOJ
- trustworthiness and safety research on AI systems has few such protections

What is needed?
- closer collaboration between industry and academia
- industry-government working groups for policy to accurately address

https://sites.mit.edu/ai-safe-harbor

Beyond Prompt Injection 
- [backdoor attacks via machine unlearning](https://arxiv.org/abs/2201.09538)
	- unlike other attacks, legal obligations to comply with removal of training data effect
- [LLM agents can autonomously hack websites]([https://arxiv.org/abs/2402.06664](https://arxiv.org/abs/2402.06664 "https://arxiv.org/abs/2402.06664"))
	- (Note from me: I am aware of views like this of this paper https://struct.github.io/llm_auto_hax.html)
- Vulnerability vs. exploit: Blocking pattern-matched adversarial prompts does not fix the underlying problem

## Designing an AI Stack for Agent-Based Cybersecurity
- NSF AI institute for agent based cyber threat intelligence and operation (ACTION) 

Thrust AI - 1: Learning and reasoning with Domain Knowledge
Thrust AI - 2: Human-Agent Interaction
Thrust AI - 3: Multi Agent Collaboration

Thrust AI - 4: Strategic Gaming and Tactical Planning
- foundation of strategy games
- adversary modeling 

Thrust SEC - 1: intelligent agents for threat/vulnerability assessment
- malicious multi agent systems
- attack scenario simulation
- attack scenario assessment for attribution
- analysis and containment of multi step attack
## EIReLaND

SDN-RL Motivations
- Why SDNs?
	- programmable control planes enable dynamic network control
	- SDNs enable a global view of the network
- Why RL?
	- solving a clearly defined goal-oriented problem: stop malicious traffic while allowing benign traffic
	- network quality can be represented efficiently in a reward function
	- decisions made are often sequential, with the agents' actions affecting the state of the system
	- policy can be learned online with sequential samples
	- diverse range of attacks and sources that necessitate different responses

EIREeLaND Design
Observables
- IP addresses
- packet/flow sizes
- port numbers
- CPU, memory usage
- application-level observables

Delayed Rewards
- network events happen at sub microsec scale
- network statistics gathered on the order of seconds
- rewards are delayed (after every n seconds or n events)
- agents make multiple decisions before a reward is administered

EIReLaND Summary
- A hybrid simulation/emulation framework for software networking (SDN)-reinforcement learning (RL)-based network defense evaluation
	- OpenAl Gym + Ryu SDN Controller + ContainerNet
- We evaluated three exemplar network attack scenarios, in simulation and emulation
	- SYN flood (volumotiic DoS), SSH Bruteforce (app-level attacks), Range Header (CPU and memory exhaustion)
-  We utilized four interpretability techniques to explain how policy models make their decisions
	- Decision tree proxies, Input-space decision analysis, Input-space confidence, attribution analysis
-  Interpretability-based refinement: model retraining based on interpretability results
- Paper Proc International Workshop on Adaptive Cyber Defense, Aug 2023. https://www.csl.sri.com/users/gehani/papers/ACD-2023.EIReLaND.pdf
## Using ML in Security Operations Centers: Human and Data Perspectives 

Two Perspectives: Human and Data
- ML in SOC

Human: What do security practitioners think of ML?
	- what are the perceived benefits and challenges of using ML in SOC
	- how are existing ML explanation perceived in practical security operations? (IEEE S&P 2023)

Human Factors: What do Security Practitioners think of ML?
- Qualitative Study
- 18 security practitioners
	- 5 years of experience in security industry on average
	- recruited via connections & upwork (Freelance use)
- 60 minute online conference all
	- background
	- views on ML
	- views on explanations
"everybody's got ML practitioners" IEEE S&P 2023

Factors that Impact Tool Adoption

- usability - main key barrier 1  for adoption
- effectiveness - main key barrier 2 for adoption
- adaptability
- efficiency 
- security - surprisingly not a major concern

ML is Not **Effective** Enough to Use Alone
effectiveness: ability to correctly classify an event

- effectiveness is one of the most reported factors
- ML is not effective enough
	- False positives (FP) still holds back deployment
- in pratice ML is used alongside rule engines
	- rules: most, previously seen behaviors
	- ML: few, previously unseen behaviors

Both ML and Rules have **Usability** Issues
usability: ability to easily set up, understand, and contextualize a tool

- reasoning outputs
	- ML: difficult due to black box nature
	- Rules: can be complicated, difficult to read especially if they are written by others
- Debugging the tool
	- both ML and rules are difficult to debug
	- rely on historical data

ML **Explanations** are Useful, but can be improved
- ML explanations are used in two ways:
	- Determine model correctness
	- improve situational awareness
		- context: "what is the attacker doing"
		- insights: "what should i look out for"
- Need more actionable information
	- direct iactions, contextualize the threat
	- integrate with policies and playbook
	- high-level attacker summaries

Analysts -> ML model (classifier) <- ML Explanation

Data Perspectives: measuring Network Alerts
- dataset
	- real world data from SOC of NCSA (National Center for Supercomputing Applications)
	- network alerts:
		- 115 million network level alerts from Zeek
		- 4 years (2018-2022)
	- True compromises (ground-truth)
		- 227 incident reports of true compromises
		- 20 years (2002-2022)


Humans: (Still) the Bottleneck of Threat Investigation
- based on 227 incident reports
	- majority (65%) incidents need 2+ SOC analysts to work together for attack investigation
	- SOC has 9 people, only 4 of them are analysts (typical size of SOC team)
- most attacks (66%) are detected within the same day
	- but post-attack investigation takes 53.2 days on average
- evidence of attackers targeting off-hours of human analysts (nights and weekends, with fewer analysts on call)

The results call for (AI-assisted) help during investigations

Alerts Are Triggered for Complex Reasons
- alerts are excessive: 24k-134k alerts per day
True compromises: 0.01% of alerts associated
- how to prioritize them?
Attack Attempts: 27.37% alerts can be automatically handled by policies rules
- reduces manual efforts, but still not enough!

Benign Triggers: 48.91% alerts triggered correctly but justifiable by org interest
- safe to ignore, like old software/weak keys in legacy host, internal scan
- but identifying benign triggers quite extensive manual efforts

Unknown 23.72% (can be false alerts, attack attempts, or true attacks)

Implications
- most existing ML models for NID
	- either train on benign traffic for anomaly detection 
	- or train with benign and malicious traffic supervised attack classification

- beyond classifying malicious vs benign
	- isolating attack attempts and benign triggers

Moving Forward
- engage end users when designing ML sec tools
- higher-quality data to support ML dev
	- coupled with careful data processing/cleaning
- adapting ML for overtime changes
	- both benign and malicious patterns 

## Automated Fixing of Null Pointer Dereferences with Contextual Checks

> Null Pointer Dereference (NPD) occurs when a program attempts to access memory at a null pointer, and dereferencing a null pointer always causes the program to collapse.

Threats of Null Pointer Dereference (NPD)
- attacks can misuses for DoS 

How SOTA Approaches Address NPD?
- selecting repair locations
	- e.g. path congestion calculation in VFix
- Applying Repair Operations
	- general repair framework
However, the valuable contextual information is ignored by all SOTA approaches, resulting in incorrect patches

VFix: Value Flow Guided Precise Program Repair for Null Pointer Dereferences

Motivating Example 1
- Intraprocedural State Retrogressions
- SOTA approaches ignore the valuable intraprocedural inforamtion, such as memory freeing and lock releasing

Motivating Example 2
Intraprocedural State Propagation (Function Argument Resetting)
- Failing to reset variable r could lead to an incorrect program status

Motivating Example 3
Intraprocedural State Propagation (Call Chain Assessment)
Function type modification and call chain assessment are required to fix this NPD issue

Our Contribution
We propose CONCH to genearte accurate patches for NPD errors by considering the contextual info, including Intraprocedual State Retrogression,Function Argument Reasoning, and Call

Conch Design
NPD Program -> Context Graph -> Initial patch -> Final Patch 

NPD Context Graph Construction
3 steps to construct NPD context graph
- contextual Intraprocedural CFG Construction

Path-sensitive Fixing Position Selection
- one null one error
- multi null one error
- one null multi error
- multi null multi error

Intraprocedural State Retrogression 
- return statement construction
- global variable 
## Cyber Psychology

Human
- phishers and cyber attackers
- end user
- human cyber analysis

Key advancement to science of cybersecurity: Creation of Computational Cognitive Models and the integration of those models 

DDMLab Methods

- microworld decision games
	- used for experimentation
	- humans make decisions and data is collected from them to create computational models
	- instance space learning 

Cybersecurity Games and TestBeds
- phishing detection
- honeypot game
- insiderattack game
- HackIT (decoying and masking)

Instance Based Learning (IBLT)
- image from Instance based learning in dynamic decision making *Cognitive Science*

IBLT mathematical mechanisms
- ACT-R's activation equation
- proability of retrieval
- Blended value 

Designing Effective Masking Stategies for Cyberdefense
- a masking defense strategy during reconnaissance
deceiving cyber adversaries: a game theoretic approach in the proceedings of the 17th 


Masking Defense Strategy and Attacker's Task
- a "rational"  attacker should launch the 'ayayagw' exploit instead of the "Ubuntu8" exploit on the system shown as "freeBSD"

Schlendker et al (2018) provide a Game theoretic algorithm an their simulation results show the effectiveness of the algorithm against human attackers

Using the CyberVAN testbed
- created Honeyd files to mask the OS and ports of TCs with OCs
- participants (attackers) were provided login details and allowed to nmap before they launched attacks

Human attackers were more successful against the Optimal masking than random strategies

Human attacks exhibit "Risk aversion" -> Bias toward certainty

Thakoodor et al (2020) proposed 2 algos
1. Optimal: Weak Stackelberg Equilibria (WSE)
2. "Risk Averse" masking strategy based on Prospect Theory (PT)

Would PT strategy be more effective against human attackers?

Experiment 2
Methods
- used "WSE" and "PT" matrices 

Attacker's success rate was lower with PT masking than WSE

IBL Model of the attacker 

Takeaways:
- in theory, optimal masking stategies may appear effective but when tested against *human* attackers are not successful 
- algos assume attacker rationality
- algos that account for attacker's biases can be more effective 

IBL model predictions and human defense
Team Defense Game (TDG) for HAT
- more complex scenario: larger network, deception (misinform) activities, and green agents

User Interface for TDG
Human-Automation Interdependence
- humans needed to validate intentions before model executed
Experiment involving 3 types of partners:
- IBL model
- Heuristic
- Random

Takeaways:
- An IBL model can predict human behavior in the IDG against Beeline and meander
- The IBL model, like humans improve their performance against Beeline with practice
- The IBL model can be a more effective partner in a Human-Automation Team than strategic and random partners