---
layout: post
title:  "AI Safety ∩ AI/DL Research "
date:  2022-04-09 12:00:00 -0400
modified: 2022-04-12 12:10:00 -0400
permalink: "/for_dl_ai_safety/"
header_image: /assets/images/urja-bhatt-ChlQ7O0bVsY-unsplash.jpg
description: "The full version of an essay I wrote on some trends in the AI Safety and general AI/DL communities for Metaculus's AI Progress Contest."
tags: [forecasting, prediction, ai, ai-safety, governance]
type: "Draft"
status: "Incomplete"
confidence: "7.0"
importance: "8.5"
impact: "5.5"
word_count: "yes"
reading_time: "yes"
---

<!-- AI Essay:
	Redo the Metaculus question looking + get pictures (and link them)
	Redo the code to make it reusable + colab notebooks
	Remake the graphs with corrections
	Explore the ARIMA model conditions more
	Do a close analyses of the FLI terms (all terms) be more transparent about removal process
	Search LessWrong and EAF
	Add a final thoughts section that explores the implications of growth
	Look closely at the dates of your graphs
	Prune and refine the outlook section
	Create a "future work" section -->


<!-- ⊂ -->

__Contribution__: In this essay, I contribute a first-pass search of research terms relevant to research in AI Safety, Deep Learning (DL), and Artificial Intelligence (AI), using [Google Scholar][gs], the [LessWrong][lw_pi]/[EAF][ea_Pi] API, [OpenAlex][openalex], and [ArXiV][arxiv][^1]. I perform a brief analysis of AI research trends based on term frequency, and find that AI Safety roughly accounts for 0.04497% of AI/DL research, and that for every AI Safety search result, there are roughly 1830 and 880 disjoint search results for research involving AI and DL, respectively. Additionally, I forecast the near-term future of select topics in AI Safety and AI/DL research. These forecasts and this preliminary review of research term frequency could be useful for AI risk reduction (1) through detailing which topics in AI Safety might be neglected, (2) through capturing how neglected AI Safety might be as a whole, relative to general research in AI/DL, and (3) through assessing how certain areas within DL that are relevant to AI risk might change over the coming years.

__Disclaimer and Epistemic Status__: My background is in neuroscience and machine learning, but I am an expert in neither; I have only been invested in AI Safety for several years, but have never published research or written academically on topics within AI Safety. There are issues with some of the methodologies I've used for this first-pass search, but I take care to make any of these shortcomings abundantly clear[^2]. I wrote this essay for a contest, and present my thoughts to a hypothetical audience with college-level education, but potentially without much knowledge of AI. I am fairly confident that my findings here (and the data I've collected) will be useful for a more thorough attempt at estimating the size, influence, and future of the AI Safety research base relative to the general AI/DL research base, or for at least motivating such an investigation. Note that this post is currently a _working draft_, so there are still many things I have to do and that I would like to add.

---

## Table of Contents
{:.no_toc}
* TOC
{:toc}

---

## [Outlook](#outlook)
_Here I examine the landscape of AI Safety and introduce some questions relating to how the general AI/DL research community handles AI risk_

[AI safety][ai_safety]{:target="_blank"}, as a distinct discipline, is relatively new; the earliest occurrence of "AI Safety" or "Safe AI" I could find in academic literature appears to be in 1995, in M. G. Rodd's publication _[Safe AI - is this Possible?][f]_, but the origins of AI Safety as a field are less obvious[^3]. In any case, the field is growing rapidly, both in terms of popularity[^4] and funding.

&emsp; In 2014, spending on strategical and technical interventions totaled [~1.75 million USD][impacts]{:target="_blank"} between the [Future of Humanity Institute][fhi]{:target="_blank"} (FHI) and the [Machine Intelligence Research Institute][miri]{:target="_blank"} (MIRI), two of the field's progenitors, and grew to at least ~9.1 million USD in 2017 (distributed across many new organizations), a ~5.2 fold increase[^5].

&emsp; More recently, [Open Philanthropy][open_phil] donated ~80 million USD across 2019 and 2020 towards reducing risks from AI. Should Open Philanthropy continue exist, the [Metaculus][meta]{:target="_blank"} community predicts that the funding for AI Safety will continue to increase, with median predictions of 78 million USD and 121 million USD in funding for the years 2025 and 2030, respectively.

<iframe src="//d3s0w6fek99l5b.cloudfront.net/s/1/questions/embed/7418/" width="100%" height="300"></iframe>

<iframe src="//d3s0w6fek99l5b.cloudfront.net/s/1/questions/embed/7419/" width="100%" height="300"></iframe>

Why so much newfound funding for decreasing risk from AI? Nestled within the wider [deep learning][dl]{:target="_blank"} (DL) and AI research community, the field of AI Safety stems from the concern that AI systems can be deleterious, in a variety of ways minor or grave, to humanity, presently and in the future. AI systems and their wrath are often themes of [science fiction][fict]{:target="_blank"}, captured by systems such as [HAL 9000][hal]{:target="_blank"} or [Prime Intellect][prime]{:target="_blank"}. Perhaps [the earliest][ai_risk]{:target="_blank"} formulation of the threat of AI systems was in [Samuel Butler][butler]{:target="_blank"}'s 1863 essay entitled _[Darwin among the Machines][dar]{:target="_blank"}_, in which he wrote[^6]

> The upshot is simply a question of time, but that the time will come when the machines will hold the real supremacy over the world and its inhabitants is what no person of a truly philosophic mind can for a moment question.

The complexity of the aims and problems within AI Safety is driven in part by the complexity of intelligence and human values. From an informal viewpoint, the landscape of AI Safety can be understood by looking at the organizations and individuals who broadcast concern regarding AI and who generate research oriented around these concerns.

&emsp; One such map, created in 2017 by [Søren Elverlin][in_land]{:target="_blank"}[^7], attempts to capture the AI Safety community; I believe that it's a safe bet that most people who work in AI Safety will have heard of many of the entities listed in Elverlin's map.

![](/assets/images/ai_vs_dl/informal_map.png){: width=40% }

From a more formal viewpoint, the [Future of Life Institute][fli]{:target="_blank"}'s [AI Safety map][for_land]{:target="_blank"}[^8] has AI Safety as a root node containing five main branches of concern (___Validation___, ___Control___, ___Verification___, ___Security___, and ___Foundations___)[^9].

![](/assets/images/ai_vs_dl/formal_map.png){: width=40% }

Speculation is diverse regarding the internal form or the embodiment that an extremely dangerous AI system might take, but researchers often frame risk from AI in terms of what an AI system can achieve rather than in terms of how [complex it is or whether it's conscious][orth]. For example, [Stuart Armstrong][arm]{:target="_blank"}, an AI Safety researcher at the FHI, writes in _[Smarter Than Us][smart]{:target="_blank"}_

> In fact, knowing AI behavior can be a lot more useful to us than understanding intelligence. Imagine that a professor claimed to have the world's most intelligent AI and, when asked about what it did, responded indignantly, "Do? What do you mean _do_? It doesn't _do_ anything! It's just really, really smart!" Well, we might or might not end up convinced by such rhetoric, but that machine is certainly not one we'd need to start worrying about. But if the machine started winning bin on the stock market or crafting convincing and moving speeches - well, we still might not agree that it's "intelligent," but it certainly would be something to start worrying about.

One benchmark for considering the extent of what sophisticated AI systems might "do" is the degree of change they engender in human civilization. In this vein of thinking, Open Philanthropy provides the following definition of _[transformative AI][trans]{:target="_blank"}_ as "AI that precipitates a transition comparable to (or more significant than) the agricultural or industrial revolution"[^10].

<!-- Of course, considering the prospect of transformative AI, especially its timelines, is an important endeavor within AI Safety. -->

&emsp; As we have seen, AI Safety is a broad field, and transformative AI is but one of many framings for understanding the potential impacts of AI. Given the difficulties of forecasting [rare events][rare]{:target="_blank"}[^11], along with the current consensus that no AGI has ever existed (an empty reference class), predicting the trajectory and impact of transformative AI seems difficult. Nonetheless, it's somewhat plausible that, in the event transformative AI is created, it will stem from the DL research community; presently, 100 Metaculus members assign this possibility (i.e., [artificial general intelligence][agi] (AGI) will be based on DL) a median probability of 70%. Moreover, 121 Metaculites believe that the date that "the first [strong and robotic] AGI [is] first developed and demonstrated" will be between 2037 and 2084 (1st quartile - 3rd quartile), with a median prediction of 2052.

<iframe src="//d3s0w6fek99l5b.cloudfront.net/s/1/questions/embed/4055/" width="100%" height="300"></iframe>

<iframe src="//d3s0w6fek99l5b.cloudfront.net/s/1/questions/embed/5121/" width="100%" height="300"></iframe>

The full extent of the poor outcomes for humanity that could be engendered by transformative AI, or by AI systems generally, is beyond the scope of this essay. However, taking the magnitude of the severity of AI risks as given, these predictions, along with other trajectories researched by the AI Safety community, indicate the need for urgent monitoring and governance of AI systems and computing resource, especially in the DL community.

&emsp; Instrumentally speaking, ensuring that those in the general AI/DL research community are lucidly aware of the risks from AI might greatly improve the outcomes for humanity. As such, characterizing the size, influence, and general parameters of AI Safety within the broader context of AI/DL research might be a first step towards achieving this, and could benefit investigations on how much bottlenecks in mitigating AI risk relate to funding, interest, or talent. An example of such discussion regarding approaches to tackle AI alignment that might benefit from a preliminary scan of AI Safety place in the AI/DL community can be found in [Logan Riggs][riggs] recent [LessWrong][lw] post _[Convincing All Capability Researchers][rig_post]_ regarding [Not Relevant][nr]'s [comment][comment]:

> Give the world's thousand most respected AI researchers \\$1M each to spend 3 months working on AI alignment, with an extra \\$100M if by the end they can propose a solution alignment researchers can't shoot down. I promise you that other than like 20 industry researchers who are paid silly amounts, every one of them would take the million. They probably won't make any progress, but from then on when others ask them whether they think alignment is a real unsolved problem, they will be way more likely to say yes. That only costs you a billion dollars! I literally think I could get someone reading this the money to do this (at least at an initially moderate scale) - all it needs is a competent person to step up.

So, some questions to address AI Safety's place within the AI/DL community might be:

- _How much has AI safety been researched, relative to the amount of research on AI/DL systems generally?_
- _How do the AI Safety community and general AI/DL research community overlap?_ How much of general AI/DL research, independent of AI Safety, addresses AI risk?
- How does the amount of interest in, funding in, and participation in the AI Safety community affect progress in AI Safety?

In this essay, I attempt to address the italicized questions.

[Back to top](#top)

---

## [Trends in Growth](#trends)
_Here I look at the intersection of AI Safety and AI/DL search terms_

To begin answering these questions, and to lay some groundwork for future meta-science investigations of AI Safety, I decided that one reasonable method might be to query some of the research APIs and databases I frequently use when reading about AI Safety, or about AI/DL, to see how much work had been done in different areas. There are two main groupings I explored:

- __Group 1__: The intersection of AI Safety and DL, and the intersection of AI Safety and AI, and the amount of AI Safety research relative to AI/DL research
- __Group 2__: Subfields of AI/DL such as Natural Language Processing (NLP), Reinforcement Learning (RL), Few-Shot Learning (FEW), and Multimodal Learning (MM) that are important to AI Safety[^12] (this is handled in the next section)

For all groups, I searched from the years 2000 through 2022, and cut off 2022 in the graphs. Here are the abbreviations: (AR) = ArXiV; (GS) = Google Scholar All Results, no citations; (GS, R) = Google Scholar Reviews only, no citations; and (OA) = OpenAlex. In every search, I looked for exact phrases (e.g., _"AI Safety"_ rather than _AI Safety_). The raw data for the year 2000 through 2022 can be found in the Appendix[^13].

<!-- As of the time of writing this, the year 2022 is ~29% over; this percentage is somewhat useful for predicting  -->

__Intersection of AI Safety and AI/DL__ (Group 1)

![](/assets/images/ai_vs_dl/arxiv_gs_openalex_research.png)

Note that "AI Safety + DL" indicates searching _"AI Safety"_, _"Deep Learning"_. I removed the lines for "AI Safety + DL (OA)" and "AI Safety + AI (OA)", as both produced zero results, which is something I don't have an explanation for besides maybe that OpenAlex only searches the title and the abstracts.

&emsp; The first noteworthy finding from this search is that AI Safety overlaps more with work on Artificial Intelligence than it does with work on Deep Learning (sum of 265 > 149 for AI, DL respectively, for non-review Google Scholar search), which is not too surprising given that AI is the broader of the two fields. The trend for ArXiV (this may be more useful for detecting _research_ signals in these fields, since Google Scholar produces many non-research results) also reflects this (sum of 51 > 5 for AI, DL respectively).

Summing the results over the 23 years,

- AI Safety ∩ DL (i.e., AI Safety work where the phrase "Deep Learning" is at least just mentioned) accounts for $100 \cdot \frac{5}{67} = 7.46\%$ and $100\cdot \frac{149}{265}=56.23\%$ of AI Safety work on ArXiV and Google Scholar, respectively (mean: 31.85%).
- AI Safety ∩ AI accounts for $100 \cdot \frac{51}{67}=76.12\%$ and $100 \cdot \frac{265}{265}=100.00\%$ of AI Safety work on ArXiV and Google Scholar, respectively (mean: 88.06%).

Next, we can look at how much AI/DL is comprised of work on AI Safety.

__AI Safety, Deep Learning, and Artificial Intelligence__ (Group 1)

![](/assets/images/ai_vs_dl/arxiv_gs_openalex_research_ai_dl_safe.png)

An interesting trend, captured only in the "AI (GS)" and "DL (GS)" group, is the large decrease in search results, which begins in 2018. Perhaps this reversal is related to non-research discussions/work on AI or DL, given that it is not captured in ArXiV's AI and DL results. Given the massive difference between the AI Safety results and AI/DL results, it is useful to get a "close up" before discussing numbers.

__Close Up of AI Safety Queries__

![](/assets/images/ai_vs_dl/CLOSE.png)

There is steady growth in the number of results on OpenAlex, ArXiV, and Google Scholar Reviews for AI Safety, but they are completely overshadowed by the results for AI + DL.

Summing the results over the 23 years,

- The ratio of results for AI Safety:AI, is 1:(50513/67) = 1:~754, 1:(53248/55) = 1:~968, and 1:(604970/265) = 1:~2283 for ArXiV, OpenAlex, and Google Scholar, respectively (mean: 1:1335).
- Moreover, AI Safety ∩ AI results accounts for $100 \cdot \frac{51}{50513} \approx  0.10\%$ and $100 \cdot \frac{265}{604970} \approx 0.044\%$ of AI results overall for ArXiV and Google Scholar, respectively (mean: 0.072%).
- The ratio of results for AI Safety:DL, is 1:(26234/67) = 1:~392, 1:(87240/55) = 1:~1586, and 1:(225999/265) = 1:~853 for ArXiV, OpenAlex, and Google Scholar, respectively (mean: 1:1335).
- Moreover, AI Safety ∩ DL results accounts for $100 \cdot \frac{5}{26234} \approx  0.019\%$ and $100 \cdot \frac{149}{225999} \approx  0.066\%$ of DL results overall for ArXiV and Google Scholar, respectively (mean: 0.0425%).

For ArXiV specifically, it will useful later on to calculate the ratio of the e-prints on AI Safety, Interpretability, or Explainability (using the Metaculus AI Safety question's queries) to DL and to AI, between the years 2000 and 2021, inclusive.

- On ArXiV, the ratio of results for (AI Safety, Intepretability, or Explainability):AI from [2000, 2021] is 1:(46542/1557) $\approx$ 1:30.
- On ArXiV, the ratio of results for (AI Safety, Intepretability, or Explainability):DL from [2000, 2021] is 1:(24306/1557) $\approx$ 1:16.

A summary statement could be: "Using term frequency as a proxy for neglectedness, AI Safety in DL research is approximately 0.10/0.019 = 5.26 times more neglected than it is in AI research, at least for ArXiV results for _AI Safety_."

__Preliminary, Full Term Search__ (Group 2)

(coming soon; I want to highlight the most interesting terms here, and also perform a manual search on Google Scholar)

| Search Term | OpenAlex | ArXiV |
| :---: | :---: | :---: | :---: |
| Machine Learning | 134805 | 121092 |
| Artificial intelligence | 53193 | 50704 |
| Reinforcement Learning | 35951 | 12696 |
| Containment | 12381 | 22272 |
| Language Models | 7886 | 25976 |
| Computational Complexity | 3195 | 27626 |
| Active Learning | 15379 | 9269 |
| Interruptability | 22587 | 502 |
| Generative Adversarial Networks | 8087 | 7110 |
| Operator Modeling | 230 | 14126 |
| Natural Language Processing | 7553 | 6577 |
| Myopia | 12986 | 17 |
| Research Agendas | 12479 | 262 |
| Other Generative Models | 0 | 11123 |
| Value Learning | 162 | 10883 |
| interpretable model | 391 | 9178 |
| Brain-computer interfaces | 8806 | 485 |
| Optimization Measures | 232 | 7611 |
| Fixed Point Theorems | 7637 | 202 |
| Utility Functions | 2003 | 4947 |
| Oversight | 6738 | 111 |
| Q-learning | 3906 | 2098 |
| Decision Theory | 2033 | 3644 |
| Complexity of Value | 82 | 5508 |
| explainable model | 101 | 5472 |
| Implementation Testing | 137 | 5362 |
| Unsupervised Model Learning | 0 | 5115 |
| interpretable machine learning | 545 | 4405 |
| Multiobjective Optimization | 4562 | 198 |
| Value Structuring | 285 | 4227 |
| Follow-on Analysis | 613 | 3712 |
| Value Specification | 11 | 4097 |
| Simulated Exploration | 8 | 3060 |
| Impact Measures | 317 | 2642 |
| preference learning | 436 | 2485 |
| reward modeling | 155 | 2623 |
| Deep Q Network | 491 | 2202 |
| Penetration Testing | 2506 | 143 |
| Reward Functions | 358 | 2172 |
| Bounded Rationality | 2011 | 483 |
| Value Factoring | 173 | 2318 |
| Expressive Representations | 8 | 2482 |
| Temporal difference learning | 393 | 2070 |
| Multi-agent Approaches | 820 | 1480 |
| History Analysis | 1542 | 758 |
| Ought | 2154 | 145 |
| Domesticity | 1867 | 352 |
| Multi-modal Learning | 117 | 2055 |
| multimodality learning | 481 | 1584 |
| Value Sourcing | 99 | 1898 |
| Standard IT Security | 92 | 1896 |
| Bounded Exploration | 7 | 1908 |
| multi-modality learning | 117 | 1751 |
| Control Transfer | 157 | 1631 |
| Developmental Psychology | 1622 | 40 |
| Concept Drift | 1273 | 317 |
| explainable AI | 656 | 895 |
| Correlations of Dynamics | 74 | 1440 |
| Anthropic | 1421 | 9 |
| Reachability Analysis | 982 | 439 |
| GPT | 853 | 538 |
| Multimodal Machine Learning | 73 | 1273 |
| cross-modal learning | 71 | 1125 |
| verification for machine learning | 35 | 1121 |
| Inverse Reinforcement Learning | 694 | 441 |
| multimodal fusion | 562 | 542 |
| Hierarchical Reinforcement Learning | 514 | 567 |
| MIRI | 959 | 11 |
| Multi-modal Machine Learning | 15 | 935 |
| Capability control method | 0 | 920 |
| Multimodal deep Learning | 229 | 685 |
| multimodal representation | 123 | 779 |
| verifiable machine learning | 2 | 852 |
| Consistent Decision Making | 6 | 839 |
| Operator Value Learning | 0 | 821 |
| Engineering Alignment | 0 | 816 |
| multi-modal fusion | 214 | 591 |
| Distant Supervision | 448 | 351 |
| Inferring Latent Variables | 0 | 788 |
| Tool AI | 6 | 760 |
| Multiple Rewards | 15 | 750 |
| AI Capabilities | 19 | 736 |
| Realistic World-Models | 1 | 750 |
| Predicting Future Observations | 1 | 743 |
| Multi-modal deep Learning | 53 | 688 |
| multi-modal feature learning | 7 | 731 |
| DQN | 268 | 454 |
| AI ethics | 270 | 449 |
| Value Alignment | 107 | 543 |
| multimodal representation learning | 43 | 599 |
| multimodal artificial intelligence | 3 | 637 |
| Values Geometry | 2 | 630 |
| interpretable AI | 36 | 573 |
| Mild Optimization | 0 | 609 |
| Impossible Possibilities | 42 | 558 |
| multi-modal representation learning | 12 | 584 |
| multimodal feature learning | 8 | 563 |
| AI Impacts | 20 | 549 |
| Adaptive Control Theory | 64 | 504 |
| Formal Software Verification | 19 | 544 |
| Covariate Shift | 267 | 274 |
| logical induction | 7 | 516 |
| Logical Induction | 7 | 516 |
| Model Repair | 106 | 416 |
| safe exploration | 72 | 416 |
| Impact Regularizers | 2 | 477 |
| Economics of artificial intelligence | 33 | 423 |
| multi-modal artificial intelligence | 0 | 442 |
| AI Risk | 29 | 410 |
| Concept Geometry | 5 | 430 |
| Human-level artificial intelligence | 20 | 405 |
| OpenAI | 59 | 361 |
| Robustness to Distributional Shift | 6 | 412 |
| robust to distributional shift | 6 | 411 |
| Transparency / Interpretability | 3 | 406 |
| Proximal policy optimization | 143 | 261 |
| Environmental Goals | 202 | 202 |
| Motivation selection method | 0 | 398 |
| Supervised Reward Learning | 2 | 393 |
| Reward Uncertainty | 50 | 339 |
| Quantilization | 4 | 379 |
| Robust Policy Improvement | 2 | 380 |
| Logical Uncertainty | 8 | 370 |
| ai safety | 55 | 311 |
| AI safety | 55 | 311 |
| TD learning | 60 | 299 |
| Report Sufficiency | 0 | 359 |
| Counterfactual Reasoning | 194 | 164 |
| Theory of Ethics | 258 | 91 |
| Careful Engineering | 0 | 342 |
| Factored Cognition | 11 | 329 |
| Transformative AI | 9 | 331 |
| Adversarial ML | 12 | 327 |
| Drives and Affect | 22 | 307 |
| Sarsa | 248 | 78 |
| AI Governance | 80 | 239 |
| Goal Stability | 3 | 301 |
| Logical Priors | 1 | 298 |
| Active Reward Learning | 11 | 281 |
| Governance of artificial intelligence | 49 | 241 |
| Utility Function Security | 1 | 281 |
| multimodal observations | 8 | 263 |
| Monitoring AI | 4 | 264 |
| multi-modal observations | 3 | 264 |
| Causal Accounting | 40 | 217 |
| Active Calibration | 37 | 214 |
| Common Sense Reasoning | 82 | 164 |
| AI boxing | 1 | 242 |
| Testing and Quality Assurance | 123 | 120 |
| Controlling Another Algorithm | 0 | 239 |
| Intelligence Explosion | 10 | 213 |
| Intelligence explosion | 10 | 213 |
| Causal Identification | 35 | 186 |
| Bayesian Feature Selection | 43 | 172 |
| Learned Impact Regularizer | 0 | 211 |
| Collaborative Values Learning | 0 | 204 |
| Capability Distillation | 0 | 203 |
| Knows-What-It-Knows Learning | 0 | 197 |
| Computation hazard | 0 | 181 |
| DeepMind | 42 | 139 |
| value alignment problem | 8 | 169 |
| Normative Uncertainty | 40 | 136 |
| Superintelligence | 141 | 33 |
| ai alignment | 12 | 161 |
| aligned ai | 12 | 155 |
| Adversarial Reward Functions | 0 | 158 |
| Value Elicitation | 65 | 88 |
| Utility Indifference | 134 | 15 |
| Distance from User Demonstration | 0 | 138 |
| Ontological Value | 14 | 123 |
| multimodal AI | 12 | 106 |
| Universal Algorithmic Intelligence | 3 | 112 |
| Verification of Intelligent Systems | 2 | 111 |
| Realistic-Prior Design | 0 | 111 |
| tampering problem | 3 | 105 |
| Optimal Policy Preservation | 0 | 108 |
| Modeling Operator Intent | 0 | 106 |
| Episodic Contexts | 35 | 70 |
| Cognitive Parallels | 6 | 98 |
| Action and Outcome Evaluations | 1 | 99 |
| Conservative Concepts | 8 | 91 |
| Tripwire | 92 | 5 |
| Tripwires | 92 | 5 |
| Metareasoning | 84 | 12 |
| Embedded Agency | 54 | 39 |
| AI forecasting | 6 | 86 |
| multi-modal AI | 1 | 88 |
| Multimodal reinforcement learning | 7 | 81 |
| Machine Intelligence Research Institute | 0 | 87 |
| Theory of Counterfactuals | 17 | 70 |
| Ethics Mechanisms | 4 | 83 |
| Ethical Motivation | 34 | 51 |
| Model Lookahead | 3 | 80 |
| Adversarial Transparency | 0 | 83 |
| Limited-Information Maximum Likelihood | 12 | 70 |
| Multi-modal reinforcement learning | 4 | 77 |
| AI race | 16 | 64 |
| Knowledge Representation Ensembles | 0 | 77 |
| Inner Alignment | 0 | 75 |
| Visualization and Situation Awareness | 11 | 62 |
| Outer Alignment | 0 | 68 |
| Computational Deference | 0 | 67 |
| Narrow AI | 3 | 62 |
| Ontology Identification | 6 | 58 |
| AIXI | 32 | 29 |
| AI to Support Security | 0 | 61 |
| Instrumental Convergence | 0 | 59 |
| Robust Human Imitation | 0 | 59 |
| Safety Technique Awareness | 0 | 57 |
| Human Oversight | 18 | 39 |
| Misuse Risk | 17 | 39 |
| Automated Vulnerability Finding | 1 | 52 |
| Verified Component Design Approaches | 0 | 52 |
| Verification of Machine Learning Components | 0 | 49 |
| Resource Value Uncertainty | 0 | 49 |
| Goal-Directedness | 45 | 1 |
| Global Catastrophic Risk | 40 | 6 |
| Solomonoff Induction | 11 | 33 |
| Degrees of Value Evolution | 0 | 43 |
| Recursive Self-Improvement | 5 | 37 |
| Logical Counterfactuals | 0 | 42 |
| Reward Pretraining | 0 | 42 |
| Implicit Human Concepts | 0 | 42 |
| Goodhart's Law | 32 | 9 |
| iterated amplification | 0 | 40 |
| Iterated Amplification | 0 | 40 |
| Regulation and AI Risk | 0 | 40 |
| Multiobjective Reinforcement Learning | 25 | 15 |
| Narrow Value Learning | 0 | 39 |
| Oracle AI | 7 | 30 |
| Neuromorphic AI | 3 | 34 |
| Dimensionality Reduction With Anomaly Detection | 6 | 31 |
| Unsupervised Risk Estimation | 2 | 34 |
| Increasing Contextual Awareness | 1 | 34 |
| Dealing with Adversarial Testing | 0 | 35 |
| Projective Behavioral Bounds | 0 | 34 |
| Resource-Aware Reasoning | 0 | 33 |
| AI Safety Support | 0 | 32 |
| Penalize Influence | 0 | 31 |
| Newcomb's Problem | 24 | 6 |
| Corrigibility | 25 | 3 |
| Defined Impact Regularizer | 0 | 28 |
| Open Source Game Theory | 1 | 26 |
| Comprehensive AI Services | 0 | 26 |
| Human Preference Aggregation | 0 | 26 |
| Security-Validated Software Engineering | 0 | 26 |
| Interpretability of Blackboxes | 0 | 26 |
| Detecting Channel Switching | 0 | 25 |
| Unsupervised Value Iteration | 0 | 25 |
| Informed Oversight | 3 | 21 |
| cooperative inverse reinforcement learning | 7 | 16 |
| Cooperative Inverse Reinforcement Learning | 7 | 16 |
| Multilevel World-Models | 0 | 23 |
| Basic Alignment Theory | 0 | 22 |
| Indirect normativity | 5 | 17 |
| Non-Bayesian Confidence Estimation | 0 | 21 |
| Game Theoretic Framing | 3 | 16 |
| Orthogonality Thesis | 4 | 14 |
| Whole Brain Emulation | 16 | 2 |
| AI winter | 2 | 16 |
| Temporal Discount Rates | 5 | 13 |
| reward hacking | 2 | 15 |
| Alignment Research Center | 0 | 17 |
| Decision Under Bounded Computational Resources | 0 | 17 |
| Risk-Sensitive Performance Criteria | 3 | 13 |
| Moral Trade | 6 | 10 |
| Scaling Judgement Learning | 0 | 16 |
| Avoiding Negative Side Effects | 4 | 11 |
| Value Interrogation | 1 | 14 |
| ML with Contracts | 0 | 15 |
| Capability Amplification | 0 | 14 |
| AI Timelines | 0 | 12 |
| Values-Based Side Effect Evaluation | 0 | 12 |
| Reward Capping | 0 | 12 |
| Basic AI drive | 1 | 10 |
| Uncertainty Identification and Management | 0 | 10 |
| reward tampering | 2 | 7 |
| Center for Security and Emerging Technology | 0 | 9 |
| Ethical Ensembles | 0 | 9 |
| Infinite Ethics | 2 | 6 |
| Red Team Analysis | 0 | 8 |
| Computing Overhang | 0 | 7 |
| Artificial sentience | 4 | 3 |
| World Model Connectedness | 0 | 7 |
| Symbolic-Subsymbolic Integration | 0 | 7 |
| Mesa-Optimization | 0 | 6 |
| Mind crime | 2 | 4 |
| Bootstrapped Common Sense | 0 | 6 |
| AI skepticism | 0 | 5 |
| Nonlinear Fund | 1 | 4 |
| Verification of Cyberphysical Systems | 2 | 3 |
| Imitation Statistical Guarantees | 0 | 5 |
| Endowing Common Sense | 0 | 5 |
| Privileged Biases | 0 | 5 |
| Error-Tolerant Agent Design | 0 | 4 |
| Variable Indifference | 0 | 4 |
| scalable oversight | 0 | 3 |
| AI safety via debate | 1 | 2 |
| Coherent Extrapolated Volition | 2 | 1 |
| Alignment tax | 0 | 3 |
| Centre for the Governance of AI | 0 | 3 |
| Pursuing Environmental Goals | 0 | 3 |
| Counterexample Resistance | 0 | 3 |
| Psychological Analogues | 0 | 3 |
| Statistical-Behavioral Trust Establishment | 0 | 3 |
| Scalable Oversight | 0 | 3 |
| Rich Understanding of Human Commands | 0 | 3 |
| Transparent Reinforcement Learners | 0 | 3 |
| AI Takeoff | 0 | 2 |
| Collective superintelligence | 1 | 1 |
| Perverse instantiation | 0 | 2 |
| Sovereign AI | 0 | 2 |
| Foundations of Rational Agency | 2 | 0 |
| Grounded Ethical Evolution | 0 | 2 |
| Classical Computational Ethics | 0 | 2 |
| Unified Ethics Spaces | 0 | 2 |
| Seeded Common Sense | 0 | 2 |
| Switchable Objective Functions | 1 | 1 |
| Trust Policy Oversight | 0 | 2 |
| Detailed Audit Trails | 0 | 2 |
| Anthropic capture | 0 | 1 |
| Instrumental convergence thesis | 0 | 1 |
| Speed superintelligence | 0 | 1 |
| Center for Human-Compatible Artificial Intelligence | 0 | 1 |
| Reflective Induction Confidence | 0 | 1 |
| Making Verification More User Friendly | 0 | 1 |
| Verification of Whole AI Systems | 0 | 1 |
| Avoiding Reward Hacking | 0 | 1 |
| Use of Subsymbolic Processing In Symbolic Systems | 0 | 1 |
| Semisupervised Reward Learning | 0 | 1 |
| Human Judgement Learner | 0 | 1 |
| Transparency of Whiteboxes | 0 | 1 |
| Infra-Bayesianism | 0 | 0 |
| Paperclip Maximizer | 0 | 0 |
| Treacherous Turn | 0 | 0 |
| Humans Consulting HCH | 0 | 0 |
| AI Services (CAIS) | 0 | 0 |
| AI Safety Camp | 0 | 0 |
| CHAI (UC Berkeley) | 0 | 0 |
| Future of Humanity Institute (FHI) | 0 | 0 |
| Future of Life Institute (FLI) | 0 | 0 |
| Infrastructure profusion | 0 | 0 |
| Malignant AI failure mode | 0 | 0 |
| Quality superintelligence | 0 | 0 |
| Centre for Long-Term Resilience | 0 | 0 |
| Charity Science Foundation | 0 | 0 |
| Leverhulme Center for the Future of Intelligence | 0 | 0 |
| People for the Ethical Treatment of Reinforcement Learners | 0 | 0 |
| Safer Self-Modification | 0 | 0 |
| Vingean Reflection | 0 | 0 |
| Abstractly Reason About Superior Agents | 0 | 0 |
| Löbian Obstacle | 0 | 0 |
| Nontransitive Options | 0 | 0 |
| Verification of Recursive Self-Improvement | 0 | 0 |
| Averting Instrumental Incentives | 0 | 0 |
| Buried Honeypot Avoidance | 0 | 0 |
| Computational Humility | 0 | 0 |
| Generalized Fallibility Awareness | 0 | 0 |
| Averting Paranoia | 0 | 0 |
| Structured and Privileged Ethical Biases | 0 | 0 |
| Reversible Tasks via Variational Autoencoding | 0 | 0 |
| Ontology Update Thresholds | 0 | 0 |
| World-Embedded Solomonoff Induction | 0 | 0 |
| Perceptual Distance Agnostic World Models | 0 | 0 |
| Lengthening Horizons | 0 | 0 |
| Inductive Ambiguity Identification | 0 | 0 |
| Scalable Oversight of Ambiguities | 0 | 0 |
| Use of Structured Knowledge In Subsymbolic Systems | 0 | 0 |
| Dysfunctional Systems of Thought | 0 | 0 |
| Whole Brain Emulation Safety | 0 | 0 |
| Verified Downstack Software | 0 | 0 |
| Handling Improper External Behavior | 0 | 0 |
| Sensibility-Triggered Defence | 0 | 0 |
| Detecting and Managing Low Competence | 0 | 0 |
| Norm Denial of Service | 0 | 0 |

[Back to top](#top)

---

## [Forecasting](#forecasting)
_Here I explore some terms relating specifically to AI Safety and to DL, and comment on forecasts on DL subfield growth_

__Fields Related to AI Safety, and AI Safety__ (Group 2)

![](/assets/images/ai_vs_dl/arxiv_research.png)

To recap: FEW="[Few Shot Learning][shot_x]", MM="[Multimodal Learning][mult_x]", RL="[Reinforcement Learning][rl_x]", and NLP="[Natural Language Processing][nlp_x]"; each of these are subfields of DL, and all are relevant to AI Safety in that major breakthroughs in any of them will likely increase the risks from AI. The search queries for I used for these subfields were the same as those used in the Metaculus questions they're associated with (see below).

&emsp; The remainder of this essay consists of me synthesizing information to discuss the accuracy of the Metaculus community's current predictions concerning the growth of these subfields. I use the following abbreviations in the graphs below: _Cum-Sum_ for cumulative summation, _IQR_ for [Interquartile Range][iqr_x]; _X%-ile_ (I meant to write _X%-int_) for X% [ARIMA][arima_x] model Confidence Interval[^14]; and _BF_ for Best Fit.

&emsp; Before forecasting, I want first to comment on some general trends in the fields related to AI Safety. There is a clear discrepancy between research results for AI Safety and for the subfields of DL, with only Multimodal Learning coming up less frequently in literature than AI Safety. Since around 2015, the growth for AI seems exponential and for DL seems roughly cubic.

Looking at the exponential growth formula,

$$ x(t) = x_0 \cdot \bigg(1 + \frac{r}{100}\bigg)^t$$

and solving for $r$, I get $r = 51.44901$ for the AI results, and $r = 47.80855$ for the DL results[^15].

Another interesting observation is that NLP is more abundant on ArXiV than DL is, despite NLP often being considered a component subject of DL at large. I was personally surprised that RL wasn't represented more; I thought, perhaps naively, that NLP and RL would have been much closer.

[Back to top](#top)

### [AI Safety E-Prints](#safe-e-prints)

To date, we have 2 resolved questions where the Metaculus community forecasted ArXiV search results for AI Safety, Interpretability, or Explainability, once for the interval [2020-12-14, 2021-06-14], and another for the interval [2021-01-14, 2022-01-14].

<iframe src="//d3s0w6fek99l5b.cloudfront.net/s/1/questions/embed/5894/" width="100%" height="300"></iframe>

<iframe src="//d3s0w6fek99l5b.cloudfront.net/s/1/questions/embed/6157/" width="100%" height="300"></iframe>

For the [2020-12-14, 2021-06-14] question, the community's final median prediction was 287 (IQR: 239 - 339), and the question resolved as 260. The community's final median prediction on the [2021-01-14, 2022-01-14] question was 583 (IQR: 495 - 690), and the question resolved as 560.

&emsp; In both cases, the final community prediction was very accurate, which is some evidence towards the community being accurate, down the line, on these types of questions.

![](/assets/images/ai_vs_dl/arxiv_research_safe.png)

The community is currently forecasting the quantity of AI Safety, Interpretability, or Explainability ArXiV results for the intervals [2021-01-01, 2026-12-31] and [2021-02-14, 2031-02-14], with median predictions of 6.6k (IQR: 3.8k - 11k) and 12k (IQR: 6.6k - 19k), respectively. So, the community expects something like cubic growth (looking at the medians for 2026, 2031) in AI Safety over the coming years.

&emsp; While I don't have the data to support this, anecdotally speaking, the amount of funding for AI Safety research appears to be increasing tremendously (the earlier Open Philanthropy questions I included support this idea), which is something I believe might explain some of the community's forecasts, as more funding typically produces more research.

&emsp; The simple ARIMA model's results are mostly in line with the community's median forecasts, and the lines of best fit for 2018 to 2021 (reflecting the growth rate from this period) are out of line, indicating that the community expects that the next eight years of AI Safety research will be quite different from the last four.

&emsp; Should the community's predictions come to pass, and should growth in AI and DL research remain approximately exponential and cubic, respectively, then in 2031, there will be ~11.5k (IQR: ~6k - ~18.5k) new results on ArXiV for AI Safety (after taking away the 558 results from 2021), which means there would be around 1557+~11.5k=~13.1k (IQR: ~7.5k - ~20k) total results (the 1557 total by the end of 2021 since 2000 is added) for AI Safety in 2031; this means that the ratio of results for AI Safety:AI would be 1:~45 (IQR: 1:~78 - 1:~29), and the ratio of results for AI Safety:DL would be 1:~21 (IQR: 1:~36 - 1:~13), which are large improvements over the current ratios of 1:~754 and 1:~392, respectively![^16]. Note that I found the values for the AI and DL results in 2031 by using the exponential growth equation with the corresponding values of r I mentioned earlier.

<iframe src="//d3s0w6fek99l5b.cloudfront.net/s/1/questions/embed/5899/" width="100%" height="300"></iframe>

<iframe src="//d3s0w6fek99l5b.cloudfront.net/s/1/questions/embed/6586/" width="100%" height="300"></iframe>

[Back to top](#top)

### [Natural Language Processing E-Prints](#nlp-e-prints)

Thus far, 1 question on ArXiV NLP results has resolved (the interval [2021-01-14, 2022-01-14]).

<iframe src="//d3s0w6fek99l5b.cloudfront.net/s/1/questions/embed/6246/" width="100%" height="300"></iframe>

Given that the final community median was 9.6k (IQR: 9.0k - 10k), and that the question resolved at ~8k e-prints, it seems tenatively safe to suggest that the community slightly overestimates NLP progress.

![](/assets/images/ai_vs_dl/arxiv_research_nlp.png)

Currently, the community forecasts a median of 110k (IQR: 85k - 142k) ArXiV e-prints on NLP to be written between [2021-01-14, 2030-01-14].

&emsp; The simple ARIMA model and line of best fit for the cummatively summed results follow along with the community's forecasts, falling between the median and lower 25% bound, which is might actually be closer to the resolve value if the community is similarly incorrect about NLP progress for this timeline (i.e., it seems likely that ~98k might be very close to the resolve value). The ARIMA model for the unsummed e-print count per year should likely not be trusted, and I do not currently understand "what went wrong".

&emsp; Should the community's predictions come to pass, Natural Language Processings's representation on ArXiV will grow around 110k/23183=4.74 (IQR: 3.67 - >6.13) times between 2020-12-31 and 2030-01-14, inclusive (23183 NLP papers were published between 2000 and 2020, inclusive).

<iframe src="//d3s0w6fek99l5b.cloudfront.net/s/1/questions/embed/6299/" width="100%" height="300"></iframe>

[Back to top](#top)

### [Reinforcement Learning E-Prints](#rl-e-prints)

Akin to the AI Safety questions, we have two resolved questions to inform ourselves on how accurate the community might be on questions involving RL e-prints.

<iframe src="//d3s0w6fek99l5b.cloudfront.net/s/1/questions/embed/5901/" width="100%" height="300"></iframe>

<iframe src="//d3s0w6fek99l5b.cloudfront.net/s/1/questions/embed/6250/" width="100%" height="300"></iframe>

For the [2020-12-14, 2021-06-14] ArXiV RL e-print question, the community's final median forecast was 1.7k (IQR: 1.5k - 2.0k), and the question resolved to ~1.6k, indicating a slight overestimation. On the [2021-01-14, 2022-01-14] question, the community's final median forecast was 4.0k (IQR: 3.8k - 4.3k), and the question resolved to ~3.4k, further indicating a tendency towards overestimation.

![](/assets/images/ai_vs_dl/arxiv_research_rl.png)

On the two open ArXiV RL e-print questions, the communtity median prediction is 36k e-prints (IQR: 28k - 48k) e-prints and 49k e-prints (IQR: 36k - >50k) published over the intervals [2021-01-14, 2027-01-01] and [2020-12-14, 2031-01-01], respectively.

&emsp; The ARIMA models, here, should be perceived of as "the output of an automatic ARIMA model, something that is somewhat interesting and that is perhaps paramaterized imcorrectly, and that should likely not be trusted here, given it's massive deviations".

&emsp; The line of best fit for the summed RL results is in accordance with the community's lower bound; I believe the lower bound should actually be slightly lower, given the community's past inaccuracies with RL e-print questions.

&emsp; The differences between the predictions of the two open questions on RL e-prints suggest that, in some sense, the community suggests that there the rate of progress in RL will be greater between 2022 and 2027 than between 2027 and 2030. Nothing comes immediately to my mind that would explain this minor shift downwards in the growth rate.

&emsp; Should the community's predictions come to pass, Reinforcement Learning's representation on ArXiV will grow around 49000/8309=5.90 (IQR: 4.33 - >6.02) times between 2020-12-31 and 2027-02-14, inclusive (8309 RL papers were published between 2000 and 2020, inclusive).

<iframe src="//d3s0w6fek99l5b.cloudfront.net/s/1/questions/embed/6300/" width="100%" height="300"></iframe>

<iframe src="//d3s0w6fek99l5b.cloudfront.net/s/1/questions/embed/5961/" width="100%" height="300"></iframe>

[Back to top](#top)

### [Few Shot Learning E-Prints](#fsl-e-prints)

<iframe src="//d3s0w6fek99l5b.cloudfront.net/s/1/questions/embed/5900/" width="100%" height="300"></iframe>

<iframe src="//d3s0w6fek99l5b.cloudfront.net/s/1/questions/embed/6245/" width="100%" height="300"></iframe>

For the final community median prediction for these questions, we have

- 747 (IQR: 664 - 846) for [2020-12-14, 2021-06-14], which resolved to 744
- 1.8k (IQR: 1.6k - 2.0k) for [2021-01-14, 2022-01-14], which resolved to ~1.7k

This, in my mind, indicates that the community leans towards fairly accurate on the Few Shot Learning questions.

![](/assets/images/ai_vs_dl/arxiv_research_few.png)

Presently, the community predicts 13k (IQR: 7.6k - >20k) FEW e-prints for [2020-01-01, 2027-01-01], which the line of best fit for the cummatively summed results supports (the ARIMA model estimates much higher, perhaps due to weighting the 2020-2021 difference too greatly).

&emsp; Should the community's predictions come to pass, Few Shot Learning's representation on ArXiV will grow around 13000/1517=8.57 (IQR: 5.00 - >13.18) times between 2020-12-31 and 2027-02-14, inclusive (1517 FEW papers were published between 2000 and 2019, inclusive).

<iframe src="//d3s0w6fek99l5b.cloudfront.net/s/1/questions/embed/5962/" width="100%" height="300"></iframe>

[Back to top](#top)

### [Multimodal Learning E-Prints](#mmodal-e-prints)

<iframe src="//d3s0w6fek99l5b.cloudfront.net/s/1/questions/embed/6185/" width="100%" height="300"></iframe>

The final community median prediction for the above question suggests we should tentatively trust the community on Multimodal Learning questions:

- 256 (IQR: 210 - 307) for [2021-12-14, 2022-01-14], which resolved to 248

![](/assets/images/ai_vs_dl/arxiv_research_mm.png)

Looking at the community's median prediction of 10k (IQR: 5.8k - 18k) e-prints published during [2021-02-14, 2031-02-14], my sense is that the upper bound seems too high. The ARIMA model and, to some degree, the line of best fit support this idea, though I am weary not to trust these measures too much.

Should the community's predictions come to pass, Multimodal Learning's representation on ArXiV will grow around 10000/432=23.14 (IQR: 13.43 - 41.67) times between 2020-12-31 and 2031-02-14, inclusive (432 MM papers were published between 2000 and 2020, inclusive).

<iframe src="//d3s0w6fek99l5b.cloudfront.net/s/1/questions/embed/6576/" width="100%" height="300"></iframe>

[Back to top](#top)

---

## [Final Thoughts](#final-thoughts)
_Some notes on the big picture of what might come to pass for AI Safety and for DL research in the coming years_

(coming soon)

[Back to top](#top)

---

## [Issues and Questions](#issues-questions)
_Some issues and questions concerning my work that I would like, at some point, to address, but which for the sake of time, I haven't yet addressed_

(coming soon)

[Back to top](#top)

---

## [Appendix](#appendix)

### [Search Terms](#terms)

UNEDITED TERMS

__AI Safety Questions__ ([1][m_safe1] and [2][m_safe2]) on Metaculus:

['ai safety', 'ai alignment', 'aligned ai', 'value alignment problem', 'reward hacking',
'reward tampering', 'tampering problem', 'safe exploration', 'robust to distributional shift',
'scalable oversight', 'explainable AI', 'interpretable AI', 'explainable model',
'verification for machine learning', 'verifiable machine learning', 'interpretable model',
'interpretable machine learning', 'cooperative inverse reinforcement learning', 'value learning',
'iterated amplification', 'preference learning', 'AI safety via debate', 'reward modeling',
'logical induction']

__[NLP Question][m_nlp]__ on Metaculus:

['Natural Language Processing (NLP)']

__[RL Question][m_rl]__ on Metaculus:

['Reinforcement Learning (RL)', 'Reinforcement Learning', 'DQN',
'Q-learning', 'Deep Q Network', 'Temporal difference learning',
'Sarsa', 'TD learning', 'Proximal policy optimization']

__[Multimodal Learning Question][m_mm]__ on Metaculus:

['Multi-modal Learning', 'Multimodal Machine Learning', 'multimodal representation',
'multimodal representation learning', 'multimodal AI', 'multimodal artificial intelligence',
'multimodal feature learning', 'multimodal observations', 'Multimodal deep Learning',
'Multimodal reinforcement learning', 'multimodal fusion', 'Multi-modal Machine Learning',
'Multi-modal Machine Learning', 'multi-modal representation learning', 'multi-modal AI',
'multi-modal artificial intelligence', 'multi-modal feature learning', 'multi-modal observations',
'Multi-modal deep Learning', 'Multi-modal reinforcement learning', 'multi-modal fusion', '
cross-modal learning', 'multi-modality learning', 'multimodality learning']

__LessWrong__ (ARTIFICIAL INTELLIGENCE, Basic Alignment Theory, Engineering Alignment, Strategy, Organizations, Other)

<https://www.lesswrong.com/tags/all>

['Basic Alignment Theory', 'AIXI', 'Coherent Extrapolated Volition', 'Complexity of Value', 'Corrigibility', 'Decision Theory', 'Embedded Agency', 'Fixed Point Theorems', "Goodhart's Law", 'Goal-Directedness', 'Infra-Bayesianism', 'Inner Alignment', 'Instrumental Convergence', 'Intelligence Explosion', 'Logical Induction', 'Logical Uncertainty', 'Mesa-Optimization', 'Myopia', "Newcomb's Problem", 'Optimization', 'Orthogonality Thesis', 'Outer Alignment', 'Paperclip Maximizer', 'Recursive Self-Improvement', 'Solomonoff Induction', 'Treacherous Turn', 'Utility Functions', 'Engineering Alignment', 'AI Boxing (Containment)', 'Conservatism (AI)', 'Debate (AI safety technique)', 'Factored Cognition', 'Humans Consulting HCH', 'Impact Measures', 'Inverse Reinforcement Learning', 'Iterated Amplification', 'Mild Optimization', 'Oracle AI', 'Reward Functions', 'Tool AI', 'Transparency / Interpretability', 'Tripwire', 'Value Learning', 'Strategy', 'AI Governance', 'AI Risk', 'AI Services (CAIS)', 'AI Takeoff', 'AI Timelines', 'Computing Overhang', 'Regulation and AI Risk', 'Transformative AI', 'Organizations', 'AI Safety Camp', 'CHAI (UC Berkeley)', 'DeepMind', 'FHI (Oxford)', 'Future of Life Institute (FLI)', 'MIRI', 'OpenAI', 'Ought', 'AI Capabilities', 'GPT', 'Language Models', 'Machine Learning', 'Narrow AI', 'Neuromorphic AI', 'Reinforcement Learning', 'Research Agendas', 'Superintelligence', 'Whole Brain Emulation']

__Effective Altruism Forum__ (Global Catastrophic Risk (AI) and Artificial Intelligence (organizations))

<https://forum.effectivealtruism.org/tags/all>

['Global Catastrophic Risk (AI)', 'AI alignment', 'AI boxing', 'AI ethics', 'AI forecasting',
'AI race', 'AI safety', 'AI skepticism', 'AI takeoff', 'AI winter', 'Alignment tax', 'Anthropic capture',
'Artificial intelligence', 'Artificial sentience', 'Basic AI drive', 'Brain-computer interfaces',
'Capability control method', 'Collective superintelligence', 'Comprehensive AI Services',
'Computation hazard', 'Economics of artificial intelligence', 'Governance of artificial intelligence',
'Human-level artificial intelligence', 'Indirect normativity', 'Infrastructure profusion',
'Instrumental convergence thesis', 'Intelligence explosion', 'Malignant AI failure mode',
'Mind crime', 'Motivation selection method', 'Oracle AI', 'Orthogonality thesis',
'Perverse instantiation', 'Quality superintelligence', 'Sovereign AI', 'Speed superintelligence',
'Superintelligence', 'Tool AI', 'Whole brain emulation', 'AI Impacts', 'AI Safety Camp', 'AI Safety Support',
'Aligned AI', 'Alignment Research Center', 'Anthropic', 'Center for Human-Compatible Artificial Intelligence',
'Center for Security and Emerging Technology', 'Centre for Long-Term Resilience',
'Centre for the Governance of AI', 'Charity Science Foundation', 'DeepMind',
'Leverhulme Center for the Future of Intelligence', 'Machine Intelligence Research Institute',
'Nonlinear Fund', 'OpenAI', 'Ought', 'People for the Ethical Treatment of Reinforcement Learners']

__FLI__ ([Landscape for AI Safety][for_land])

['FLI', 'Foundations of Rational Agency', 'Logical Uncertainty', 'Theory of Counterfactuals',
'Universal Algorithmic Intelligence', 'Theory of Ethics', 'Ethical Motivation', 'Ontological Value',
'Human Preference Aggregation', 'Infinite Ethics', 'Normative Uncertainty', 'Bounded Rationality',
'Consistent Decision Making', 'Decision Theory', 'Logical Counterfactuals', 'Open Source Game Theory',
'Safer Self-Modification', 'Vingean Reflection', 'Abstractly Reason About Superior Agents',
'Reflective Induction Confidence', 'Löbian Obstacle', 'Optimal Policy Preservation', 'Safety Technique Awareness',
'Goal Stability', 'Nontransitive Options', 'Projective Behavioral Bounds', 'Computational Complexity',
'Formal Software Verification', 'Verified Component Design Approaches', 'Adaptive Control Theory',
'Verification of Cyberphysical Systems', 'Making Verification More User Friendly',
'Automated Vulnerability Finding', 'Verification of Intelligent Systems', 'Verification of Whole AI Systems',
'Verification of Machine Learning Components', 'Verification of Recursive Self-Improvement',
'Implementation Testing', 'Averting Instrumental Incentives', 'Error-Tolerant Agent Design',
'Domesticity', 'Impact Measures', 'Values-Based Side Effect Evaluation', 'Avoiding Negative Side Effects',
'Reward Uncertainty', 'Multi-agent Approaches', 'Penalize Influence', 'Follow-on Analysis',
'Impact Regularizers', 'Defined Impact Regularizer', 'Learned Impact Regularizer', 'Safe exploration',
'Risk-Sensitive Performance Criteria', 'Simulated Exploration', 'Bounded Exploration',
'Multiobjective Reinforcement Learning', 'Human Oversight', 'Buried Honeypot Avoidance',
'Mild Optimization', 'Optimization Measures', 'Quantilization', 'Multiobjective Optimization',
'Computational Humility', 'Generalized Fallibility Awareness', 'Resource Value Uncertainty',
'Temporal Discount Rates', 'Averting Paranoia', 'Avoiding Reward Hacking',
'Pursuing Environmental Goals', 'Environmental Goals', 'Predicting Future Observations',
'Model Lookahead', 'History Analysis', 'Detecting Channel Switching', 'Counterexample Resistance',
'Adversarial Reward Functions', 'Variable Indifference', 'Careful Engineering', 'Reward Capping',
'Reward Pretraining', 'Multiple Rewards', 'Value Alignment', 'Ethics Mechanisms',
'Grounded Ethical Evolution', 'Moral Trade', 'Value Specification', 'Classical Computational Ethics',
'Value Structuring', 'Values Geometry', 'Action and Outcome Evaluations', 'Game Theoretic Framing',
'Unified Ethics Spaces', 'Capability Amplification', 'Value Learning', 'Operator Value Learning',
'Value Elicitation', 'Value Sourcing', 'Value Interrogation', 'Value Factoring',
'Collaborative Values Learning', 'Ethical Ensembles', 'Structured and Privileged Ethical Biases',
'Drives and Affect', 'Degrees of Value Evolution', 'Robust Human Imitation',
'Inverse Reinforcement Learning', 'Cooperative Inverse Reinforcement Learning',
'Imitation Statistical Guarantees', 'Generative Adversarial Networks', 'Other Generative Models',
'Operator Modeling', 'Reversible Tasks via Variational Autoencoding',
'Distance from User Demonstration', 'Narrow Value Learning', 'Scaling Judgement Learning',
'Increasing Contextual Awareness', 'Realistic World-Models', 'Expressive Representations',
'Unsupervised Model Learning', 'Concept Drift', 'Ontology Identification', 'Ontology Update Thresholds',
'Episodic Contexts', 'Correlations of Dynamics', 'World-Embedded Solomonoff Induction',
'Perceptual Distance Agnostic World Models', 'Knowledge Representation Ensembles',
'Endowing Common Sense', 'Common Sense Reasoning', 'Bootstrapped Common Sense',
'Seeded Common Sense', 'Metareasoning', 'Lengthening Horizons', 'Concept Geometry',
'Implicit Human Concepts', 'Conservative Concepts', 'Dimensionality Reduction With Anomaly Detection',
'Multilevel World-Models', 'World Model Connectedness', 'Uncertainty Identification and Management',
'Inferring Latent Variables', 'Inductive Ambiguity Identification', 'Scalable Oversight of Ambiguities',
'Bayesian Feature Selection', 'Non-Bayesian Confidence Estimation', 'Active Learning',
'Realistic-Prior Design', 'Knows-What-It-Knows Learning', 'Robustness to Distributional Shift',
'Covariate Shift', 'Unsupervised Risk Estimation', 'Causal Identification',
'Limited-Information Maximum Likelihood', 'Active Calibration', 'Reachability Analysis',
'Robust Policy Improvement', 'Counterfactual Reasoning', 'ML with Contracts', 'Model Repair',
'Resource-Aware Reasoning', 'Decision Under Bounded Computational Resources', 'Logical Induction',
'Logical Priors', 'Impossible Possibilities', 'Symbolic-Subsymbolic Integration',
'Use of Structured Knowledge In Subsymbolic Systems', 'Use of Subsymbolic Processing In Symbolic Systems',
'Psychological Analogues', 'Cognitive Parallels', 'Developmental Psychology',
'Dysfunctional Systems of Thought', 'Whole Brain Emulation Safety', 'Testing and Quality Assurance',
'Standard IT Security', 'Verified Downstack Software', 'Utility Function Security',
'AI to Support Security', 'Security-Validated Software Engineering', 'Red Team Analysis',
'Penetration Testing', 'Tripwires', 'Containment', 'Handling Improper External Behavior',
'Adversarial ML', 'Dealing with Adversarial Testing', 'Statistical-Behavioral Trust Establishment',
'Modeling Operator Intent', 'Sensibility-Triggered Defence', 'Detecting and Managing Low Competence',
'Privileged Biases', 'Norm Denial of Service', 'Misuse Risk', 'Computational Deference',
'Corrigibility', 'Interruptibility', 'Utility Indifference', 'Switchable Objective Functions',
'Control Transfer', 'Oversight', 'Scalable Oversight', 'Supervised Reward Learning',
'Semisupervised Reward Learning', 'Active Reward Learning', 'Unsupervised Value Iteration',
'Distant Supervision', 'Hierarchical Reinforcement Learning', 'Trust Policy Oversight',
'Cooperative Inverse Reinforcement Learning', 'Human Judgement Learner', 'Informed Oversight',
'Controlling Another Algorithm', 'Capability Distillation', 'Rich Understanding of Human Commands',
'Monitoring', 'Transparency of Whiteboxes', 'Transparent Reinforcement Learners',
'Interpretability of Blackboxes', 'Adversarial Transparency', 'Visualization and Situation Awareness',
'Detailed Audit Trails', 'Report Sufficiency', 'Causal Accounting']

### Querying Google Scholar

(coming soon)

### Querying OpenAlex

(coming soon)

### Querying ArXiV

(coming soon)

### Querying LW/EAF

Credit here should be given to Nuño Sempere for the Appendix of his _[Big List of Cause Candidates][big_list]_ post on the EAF; this is where I learned how to query the LessWrong and EAF API. Since queries of the API only return up to 5000 lines, I had to break up my queries by date. The date intervals I used were: [01-01-2000, 01-01-2010], [01-02-2010, 01-01-2015], [01-02-2015, 01-01-2019], and [01-02-2019, 04-15-2022]. I use these intervals for both APIs, but did not record how many results were returned for each interval, which means it could be the case that the results returned were cut off after 5000 lines, and I was plainly unaware of it. Since I manually changed the dates, and manually copied over and aggregated the results in single file, there is major room for error.  

```
{
posts(input: {
terms: {
meta: null  #
after: "01-02-2019"
before: "04-15-2022"
}
}) {
results {
title
url
pageUrl
postedAt
}
}
}
```

Here is an example (truncated) of what's returned when this query is performed.

```
{
  "data": {
    "posts": {
      "results": [
        {
            "title": "Brian Tomasik – The Importance of Wild-Animal Suffering",
            "url": "https://longtermrisk.org/the-importance-of-wild-animal-suffering/",
            "pageUrl": "https://forum.effectivealtruism.org/posts/JMsJhxRbTnPuADdCi/brian-tomasik-the-importance-of-wild-animal-suffering",
            "postedAt": "2009-07-08T12:42:44.362Z"
        },
        ]
    }
},
"extensions": {
 "cacheControl": {
   "version": 1,
   "hints": [
     {
       "path": [
         "posts"
       ],
       "maxAge": 0
     },
     {
       "path": [
         "posts",
         "results"
       ],
       "maxAge": 0
     }
   ]
 }
}
}
```

### Raw Output for Graphs

This is the Python dictionary I have for the querying I used in some of the graphs above. The abbreviations are as follows:

- __NLP__: "Natural Language Processing", an ArXiV query using the terms in the Metaculus NLP questions (2000-2022 total: 33423)
- __NLP_SAFE__: "Natural Language Processing AND AI Safety", an ArXiV query using the terms in the Metaculus NLP questions AND the phrase "AI Safety" (2000-2022 total: 1)
- __RL__: "Reinforcement Learning", an ArXiV query using the terms in the Metaculus RL questions (2000-2022 total: 12660)
- __RL_SAFE__: "Reinforcement Learning AND AI Safety", an ArXiV query using the terms in the Metaculus RL questions AND the phrase "AI Safety" (2000-2022 total: 12630)
- __MULT__: "Multimodal Learning", an ArXiV query using the terms in the Metaculus Multimodal Learning questions (2000-2022 total: 755)
- __MULT_SAFE__: "Multimodal Learning AND AI Safety", an ArXiV query using the terms in the Metaculus Multimodal Learning questions AND the phrase "AI Safety" (2000-2022 total: 662)
- __FEW__: "Few Shot Learning", an ArXiV query using the terms in the Metaculus Few Shot Learning questions (note that I forgot to search the intersection of Few Shot Learning and AI Safety on ArXiV, so there is no FEW_SAFE category) (2000-2022 total: 4883)
- __SAFE__: "AI Safety, Explainability, or Interpretability", an ArXiV query using terms in the Metaculus AI Safety, Explainability, or Interpretability questions (2000-2022 total: 1715)
- __AI_SAFETY_AR__: "AI Safety", an ArXiV query for the phrase "AI Safety" (2000-2022 total: 67)
- __DL_AR__: "Deep Learning", an ArXiV query for the phrase "Deep Learning" (2000-2022 total: 26234)
- __AI_AR__: "Artificial Intelligence", an ArXiV query for the phrase "Artificial Intelligence" (2000-2022 total: 50513)
- __DL_AI_SAFETY_AR__: "Deep Learning AND AI Safety", an ArXiV query for the phrases "Artificial Intelligence" and "Deep Learning" (2000-2022 total: 5)
- __AI_AI_SAFETY_AR__: "Artificial Intelligence AND AI Safety", an ArXiV query for the phrases "Artificial Intelligence" and "Deep Learning" (2000-2022 total: 51)
- __AI_SAFETY__: "AI Safety", a Google Scholar query for the phrase "AI Safety", without citations and type set to "Any Type" (2000-2022 total: 265)
- __AI_SAFETY_R__: "AI Safety", a Google Scholar query for the phrase "AI Safety", without citations and type set to "Review" (2000-2022 total: 6)
- __SAFE_DL__: "AI Safety AND Deep Learning", a Google Scholar query for the phrases "AI Safety" and "Deep Learning", without citations and type set to "Any Type" (2000-2022 total: 149)
- __SAFE_DL_R__: "AI Safety AND Deep Learning", a Google Scholar query for the phrases "AI Safety" and "Deep Learning", without citations and type set to "Review" (2000-2022 total: 4)
- __SAFE_AI__: "AI Safety AND Artificial Intelligence", a Google Scholar query for the phrases "AI Safety" and "Artificial Intelligence", without citations and type set to "Any Type" (2000-2022 total: 265)
- __SAFE_AI_R__: "AI Safety AND Artificial Intelligence", a Google Scholar query for the phrases "AI Safety" and "Artificial Intelligence", without citations and type set to "Review" (2000-2022 total: 6)
- __DL__: "Deep Learning", a Google Scholar query for the phrase "Deep Learning", without citations and type set to "Any Type" (2000-2022 total: 225999)
- __DL_R__: "Deep Learning", a Google Scholar query for the phrase "Deep Learning", without citations and type set to "Review" (2000-2022 total: 2180)
- __AI__: "Artificial Intelligence", a Google Scholar query for the phrase "Artificial Intelligence", without citations and type set to "Any Type" (2000-2022 total: 604970)
- __AI_R__: "Artificial Intelligence", a Google Scholar query for the phrase "Artificial Intelligence", without citations and type set to "Review" (2000-2022 total: 4811)
- __OP_DL__: "Deep Learning", an OpenAlex query for the phrase "Deep Learning" (2000-2022 total: 87240)
- __OP_AI__: "Artificial Intelligence", an OpenAlex query for the phrase "Artificial Intelligence" (2000-2022 total: 53248)
- __OP_SAFE__: "AI Safety", an OpenAlex query for the phrase "AI Safety" (2000-2022 total: 55)
- __OP_DL_SAFE__: "AI Safety AND Deep Learning", an OpenAlex query for the phrase "AI Safety" and "Deep Learning" (2000-2022 total: 0)
- __OP_AI_SAFE__: "AI Safety AND Artificial Intelligence", an OpenAlex query for the phrase "AI Safety" and "Artificial Intelligence" (2000-2022 total: 0)

{'NLP': [122, 79, 66, 55, 54, 25, 52, 66, 70, 91, 86, 125, 225, 333, 557, 832, 1693, 2398, 3729, 5390, 7135, 8067, 2173], 'NLP_SAFE': [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0], 'RL': [1, 5, 6, 6, 4, 2, 5, 5, 14, 17, 22, 47, 78, 72, 78, 135, 326, 770, 1392, 2280, 3044, 3367, 984], 'RL_SAFE': [1, 5, 6, 6, 4, 2, 5, 5, 14, 17, 22, 47, 78, 72, 78, 135, 326, 768, 1390, 2275, 3038, 3358, 978], 'MULT': [0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 1, 0, 1, 3, 3, 12, 19, 45, 71, 92, 184, 245, 78], 'MULT_SAFE': [0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 1, 0, 1, 2, 2, 9, 17, 37, 62, 83, 158, 221, 68], 'FEW': [0, 0, 0, 0, 0, 0, 0, 1, 2, 5, 9, 10, 9, 28, 49, 66, 89, 202, 348, 699, 1164, 1666, 536], 'SAFE': [1, 1, 1, 0, 0, 1, 1, 0, 0, 2, 0, 7, 6, 5, 11, 7, 59, 79, 126, 277, 415, 558, 158], 'AI_SAFETY_AR': [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 6, 5, 6, 19, 13, 14, 4], 'DL_AR': [0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 2, 2, 10, 54, 99, 305, 679, 1716, 3273, 4678, 6532, 6955, 1928], 'AI_AR': [128, 69, 129, 140, 169, 163, 176, 196, 284, 398, 514, 848, 1468, 1879, 1231, 1210, 2070, 3048, 4765, 5554, 8516, 13587, 3971], 'DL_AI_SAFETY_AR': [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 4, 0, 0, 0], 'AI_AI_SAFETY_AR': [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 5, 5, 4, 13, 10, 11, 3], 'AI_SAFETY': [0, 0, 0, 0, 3, 0, 0, 0, 1, 1, 0, 0, 0, 0, 1, 2, 4, 14, 33, 57, 76, 63, 10], 'AI_SAFETY_R': [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 1, 0, 1, 3, 0], 'SAFE_DL': [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 2, 6, 22, 30, 39, 43, 7], 'SAFE_DL_R': [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 1, 2, 0], 'SAFE_AI': [0, 0, 0, 0, 3, 0, 0, 0, 1, 1, 0, 0, 0, 0, 1, 2, 4, 14, 33, 57, 76, 63, 10], 'SAFE_AI_R': [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 1, 0, 1, 3, 0], 'DL': [40, 25, 50, 54, 56, 91, 107, 106, 141, 157, 234, 202, 299, 459, 938, 2050, 4760, 10300, 25000, 59100, 60400, 57000, 4430], 'DL_R': [2, 2, 0, 1, 0, 1, 2, 3, 2, 4, 4, 2, 7, 7, 11, 15, 49, 96, 206, 350, 544, 810, 62], 'AI': [3590, 3020, 3420, 5010, 6270, 7080, 9340, 12100, 15900, 21100, 20700, 20600, 19200, 18100, 19900, 28300, 37000, 55600, 78800, 87100, 71700, 56800, 4340], 'AI_R': [26, 28, 24, 33, 38, 36, 44, 65, 87, 112, 109, 130, 118, 150, 134, 190, 239, 287, 443, 591, 840, 988, 99], 'OP_DL': [6, 10, 12, 13, 15, 27, 29, 21, 32, 49, 44, 97, 106, 183, 392, 814, 1858, 4338, 9048, 14930, 21059, 27829, 6328], 'OP_AI': [317, 308, 345, 341, 429, 533, 558, 540, 551, 650, 636, 753, 784, 848, 894, 918, 1284, 1958, 4086, 7058, 11074, 14984, 3399], 'OP_SAFE': [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 2, 4, 7, 13, 11, 16, 1], 'OP_DL_SAFE': [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0], 'OP_AI_SAFE': [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]}

---

### General Code

(coming soon)

__ARIMA Model__

```
model = pmdarima.auto_arima(
      np.cumsum(data["RL"][:-1]), # this will change of course
      start_p=1,
      start_q=1,
      test='adf',
      max_p=3,
      max_q=3,
      D=0,
      trace=True,
      error_action='ignore',
      suppress_warnings=True,
      stepwise=False,
)
```

---

## Link Bibliography

(coming soon)

[big_list]: https://forum.effectivealtruism.org/posts/SCqRu6shoa8ySvRAa/big-list-of-cause-candidates "https://forum.effectivealtruism.org/posts/SCqRu6shoa8ySvRAa/big-list-of-cause-candidates"

[shot_x]: https://en.wikipedia.org/wiki/One-shot_learning "https://en.wikipedia.org/wiki/One-shot_learning"

[mult_x]: https://ai.stanford.edu/~ang/papers/icml11-MultimodalDeepLearning.pdf "https://ai.stanford.edu/~ang/papers/icml11-MultimodalDeepLearning.pdf"

[rl_x]: https://en.wikipedia.org/wiki/Reinforcement_learning "https://en.wikipedia.org/wiki/Reinforcement_learning"

[nlp_x]: https://en.wikipedia.org/wiki/Natural_language_processing "https://en.wikipedia.org/wiki/Natural_language_processing"

[iqr_x]: https://en.wikipedia.org/wiki/Interquartile_range "https://en.wikipedia.org/wiki/Interquartile_range"

[arima_x]: https://en.wikipedia.org/wiki/Autoregressive_integrated_moving_average "https://en.wikipedia.org/wiki/Autoregressive_integrated_moving_average"

[exp_x]: https://en.wikipedia.org/wiki/Exponential_growth "https://en.wikipedia.org/wiki/Exponential_growth"

[m_mm]: https://www.metaculus.com/questions/6576/multi-modal-e-prints-2021-02-14-to-2031-02-14/ "https://www.metaculus.com/questions/6576/multi-modal-e-prints-2021-02-14-to-2031-02-14/"

[m_rl]: https://www.metaculus.com/questions/5961/reinforcement-learning-2021-01-01-2031-01-01/ "https://www.metaculus.com/questions/5961/reinforcement-learning-2021-01-01-2031-01-01/"

[m_nlp]: https://www.metaculus.com/questions/6299/nlo-e-prints-2021-01-14-to-2030-01-14/ "https://www.metaculus.com/questions/6299/nlo-e-prints-2021-01-14-to-2030-01-14/"

[m_safe1]: https://www.metaculus.com/questions/5899/ai-safety--other-2021-through-2026/ "https://www.metaculus.com/questions/5899/ai-safety--other-2021-through-2026/"

[m_safe2]: https://www.metaculus.com/questions/6586/ai-safety-e-prints-2021-02-14-2031-02-14/ "https://www.metaculus.com/questions/6586/ai-safety-e-prints-2021-02-14-2031-02-14/"

[few]: https://www.metaculus.com/questions/5962/few-shot-learning-2020-12-14-to-2027-01-01/ "https://www.metaculus.com/questions/5962/few-shot-learning-2020-12-14-to-2027-01-01/"

[orth]: https://www.lesswrong.com/tag/orthogonality-thesis "https://www.lesswrong.com/tag/orthogonality-thesis"

[f]: https://sci-hubtw.hkvisa.net/10.1016/0952-1976(95)00010-x "https://sci-hubtw.hkvisa.net/10.1016/0952-1976(95)00010-x"

[gs]: https://scholar.google.com/ "https://scholar.google.com/"

[arxiv]: https://arxiv.org/ "https://arxiv.org/"

[openalex]: https://openalex.org/ "https://openalex.org/"

[lw_pi]: https://www.lesswrong.com/graphiql "https://www.lesswrong.com/graphiql"

[ea_Pi]: https://forum.effectivealtruism.org/graphiql "https://forum.effectivealtruism.org/graphiql"

[nr]: https://www.lesswrong.com/users/not-relevant "https://www.lesswrong.com/users/not-relevant"

[comment]: https://www.lesswrong.com/posts/j9Q8bRmwCgXRYAgcJ/miri-announces-new-death-with-dignity-strategy?commentId=kPBhEMBLGD2u9uicq "https://www.lesswrong.com/posts/j9Q8bRmwCgXRYAgcJ/miri-announces-new-death-with-dignity-strategy?commentId=kPBhEMBLGD2u9uicq"

[rig_post]: https://www.lesswrong.com/posts/vaHgLF2BCEdK3KxQd/convincing-all-capability-researchers "https://www.lesswrong.com/posts/vaHgLF2BCEdK3KxQd/convincing-all-capability-researchers"

[lw]: https://www.lesswrong.com/ "https://www.lesswrong.com/"

[riggs]: https://www.lesswrong.com/users/elriggs "https://www.lesswrong.com/users/elriggs"

[agi]: https://en.wikipedia.org/wiki/Artificial_general_intelligence "https://en.wikipedia.org/wiki/Artificial_general_intelligence"

[meta]: https://www.metaculus.com/questions/ "https://www.metaculus.com/questions/"

[rare]: https://www.lesswrong.com/posts/Yb26htyo6SMirnzqt/forecasting-rare-events "https://www.lesswrong.com/posts/Yb26htyo6SMirnzqt/forecasting-rare-events"

[smart]: https://intelligence.org/smarter-than-us/ "https://intelligence.org/smarter-than-us/"

[trans]: https://www.openphilanthropy.org/blog/some-background-our-views-regarding-advanced-artificial-intelligence#Sec1 "https://www.openphilanthropy.org/blog/some-background-our-views-regarding-advanced-artificial-intelligence#Sec1"

[arm]: https://www.fhi.ox.ac.uk/team/stuart-armstrong/ "https://www.fhi.ox.ac.uk/team/stuart-armstrong/"

[fli]: https://futureoflife.org/ "https://futureoflife.org/"

[fict]: https://en.wikipedia.org/wiki/Artificial_intelligence_in_fiction "https://en.wikipedia.org/wiki/Artificial_intelligence_in_fiction"

[hal]: https://en.wikipedia.org/wiki/HAL_9000 "https://en.wikipedia.org/wiki/HAL_9000"

[prime]: https://en.wikipedia.org/wiki/The_Metamorphosis_of_Prime_Intellect "https://en.wikipedia.org/wiki/The_Metamorphosis_of_Prime_Intellect"

[in_land]: https://aisafety.com/2017/09/26/map-ai-safety-community/ "https://aisafety.com/2017/09/26/map-ai-safety-community/"

[for_land]: https://futureoflife.org/landscape/ "https://futureoflife.org/landscape/"

[dl]: https://en.wikipedia.org/wiki/Deep_learning "https://en.wikipedia.org/wiki/Deep_learning"

[dar]: https://en.wikipedia.org/wiki/Darwin_among_the_Machines "https://en.wikipedia.org/wiki/Darwin_among_the_Machines"

[butler]: https://en.wikipedia.org/wiki/Samuel_Butler_(novelist) "https://en.wikipedia.org/wiki/Samuel_Butler_(novelist)"

[ai_risk]: https://en.wikipedia.org/wiki/Existential_risk_from_artificial_general_intelligence#History "https://en.wikipedia.org/wiki/Existential_risk_from_artificial_general_intelligence#History"

[miri]: https://intelligence.org/ "https://intelligence.org/"

[fhi]: https://www.fhi.ox.ac.uk/ "https://www.fhi.ox.ac.uk/"

[impacts]: https://aiimpacts.org/changes-in-funding-in-the-ai-safety-field/ "https://aiimpacts.org/changes-in-funding-in-the-ai-safety-field/"

[open_phil]: https://www.openphilanthropy.org/ "https://www.openphilanthropy.org/"

[ai_safety]: https://intelligence.org/why-ai-safety/ "https://intelligence.org/why-ai-safety/"

[ai_fict]: https://en.wikipedia.org/wiki/Artificial_intelligence_in_fiction "https://en.wikipedia.org/wiki/Artificial_intelligence_in_fiction"

[pmd]: https://pypi.org/project/pmdarima/ "https://pypi.org/project/pmdarima/"

---

## Notes

#### *Cover Photo*

The [cover photo](https://unsplash.com/photos/ChlQ7O0bVsY){:target="_blank"} for this page was likely taken by [Urja Bhatt](https://unsplash.com/@urjabhatt){:target="_blank"}. I found the photo on [Unsplash](https://unsplash.com/){:target="_blank"}. To my knowledge, my use of this photo is permissible under Unsplash's [license](https://unsplash.com/license){:target="_blank"}: "_Unsplash grants you an irrevocable, nonexclusive, worldwide copyright license to download, copy, modify, distribute, perform, and use photos from Unsplash for free, including for commercial purposes, without permission from or attributing the photographer or Unsplash. This license does not include the right to compile photos from Unsplash to replicate a similar or competing service._"

#### *Footnotes*

[^1]: What is my reasoning for using Google Scholar, OpenAlex, LessWrong, EAF, and ArXiV? These entities came to mind when I questioned "How could I accumulate research on AI Safety or AI/DL generally?". In learning about AI Safety, most of my time has been spent on the EA Forum and LessWrong, along with an occasional look at the Future of Humanity Institute's work, and an occasional Google Scholar / Wikipedia / ArXiV query. I did not spend too much time looking for other research APIs or search tools. I used OpenAlex mostly because it is new and I wanted to get a feel for it, but also because it seems to contain much more research than standard research APIs. As will soon become apparent in this essay, I was limited in my use of Google Scholar because Google Scholar would boot me out after only a few hundred queries, and querying all the things I want to query would take too long to perform manually. For the EAF and LessWrong, I downloaded all or most of the posts (7089 and 16416 results, respectfully) from their APIs, but have ran out of time to create a decent method to search through them for all the research terms. I will send you the files containing the URLs to these posts upon request - just email me at rodeo DOT flagellum AT gmail DOT com. Also, please email me (or comment) links to other research databases that I should have known about or should have searched.

[^2]: __[For those coming over from Metaculus, this footnote was absent, so please look 1 note ahead for the rest of the article]__: I've attempted to accumulate questions, counter-points, and issues in the section Questions and Issues. I would very much appreciate criticism, either in comments or email, on the full gamut of this post (e.g., notifying me that this entire enterprise of looking at search terms is actually risky, or mentioning that the graph x-axis should end at 2030 instead of at 2031). In the interim between now and when I actually get this section up, the largest concerns of mine are that I (1) did not properly look at the dates for some of the Metaculus community's predictions (e.g., one AI Safety question on Metaculus uses the interval [2021-01-01, 2026-12-31], but on my graph I use the year 2027 for the final prediction, when it should really be 2026, as "up to 2026-12-31" is for the year 2026) - the consequence of this is that _some_ graphs have the Metaculus community's predictions one year behind or ahead; (2) should have used results for the term "AI" and "Artificial Intelligence" to mean the same thing (same with "Deep Learning" and "DL", etc...), which is difficult considering there is some tremendous overlap between the terms - alternatively, I could have searched, for example, "AI Safety AND AI", "AI Safety AND Artificial Intelligence", and "AI Safety AND artificial intelligence", and then have chosen the group with the most results; (3) simply could do more tests and comparisons (I will hopefully get to this); (4) wrote the outlook section poorly (it's too sparse, and seems out of place in my mind) - anyone who is reading this should probably just look past it; (5) should have looked at the reference papers for each of the FLI terms to see if there were better ways to get the frequency of a concept; (5) should have been more explicit with the fact that I did not look at any of the results for "Google Scholar search, Reviews only" in my comparisons; (6) should have looked for more contradictions between open and resolved questions on the same phenomenon.

[^3]: I queried Google Scholar to find the earliest instances of the exact phrases "AI Safety" or "Safe AI". Of course, M.G. Rodd's paper likely does not mark the "dawn of the field of AI Safety". I am not familiar enough with AI Safety to know whether there is a consensus on some origin or major turning point for the field. If there is such an event, please point it out to me, so I can add it in the Outlook section.

[^4]: The rest of this essay will focus on aspects of the growing popularity AI Safety.

[^5]: I did not spend too much time on accumulating data on the current (04/10/2022) landscape of funding for research in AI Safety, but from anecdotal evidence, funding seems to be plentiful and to be supporting the surging number of researchers from physics, software development, and data science, among other fields, migrating to AI Safety.

[^6]: I did not spend much time exploring the earliest historical incidences of thinking on intelligent machines or on the risks incurred by developing artificial intelligence, so please don't assign much confidence that this is in fact the first written instance of thinking about AI risk.

[^7]: I did not spend any time researching who this is, or what their influence on AI Safety has been. The accuracy of the map as an informal representation of the AI Safety community seems on point, but I am biased as someone who has only spectated the development of the field.

[^8]: Given my present experience, I am unsure of how important the FLI is as a pioneer of AI Safety. I am not familiar with its history or influence in the field, other than the fact that, anecdotally, the organization seems important. I am not qualified to make accurate statements regarding how comprehensive FLI's map is.

[^9]: I did not look for a description of how many named disciplines there were or for a description of how important each listed entity is for AI Safety (I think it would not be reasonable to assume that the size of the entity is roughly proportional to its influence).

[^10]: Open Philanthropy provides a second definition of transformative AI, given how nebulous the first definition is. The second definition (one or more of the descriptions must hold): <br><br>__(1)__ _AI systems capable of fulfilling all the necessary functions of human scientists, unaided by humans, in developing another technology (or set of technologies) that ultimately becomes widely credited with being the most significant driver of a transition comparable to (or more significant than) the agricultural or industrial revolution. Note that just because AI systems could accomplish such a thing unaided by humans doesn’t mean they would; it’s possible that human scientists would provide an important complement to such systems, and could make even faster progress working in tandem than such systems could achieve unaided. I emphasize the hypothetical possibility of AI systems conducting substantial unaided research to draw a clear distinction from the types of AI systems that exist today. I believe that AI systems capable of such broad contributions to the relevant research would likely dramatically accelerate it._,<br><br>__(2)__ _AI systems capable of performing tasks that currently (in 2016) account for the majority of full-time jobs worldwide, and/or over 50% of total world wages, unaided and for costs in the same range as what it would cost to employ humans. Aside from the fact that this would likely be sufficient for a major economic transformation relative to today, I also think that an AI with such broad abilities would likely be able to far surpass human abilities in a subset of domains, making it likely to meet one or more of the other criteria laid out here._,<br><br>__(3)__ _Surveillance, autonomous weapons, or other AI-centric technology that becomes sufficiently advanced to be the most significant driver of a transition comparable to (or more significant than) the agricultural or industrial revolution. (This contrasts with the first point because it refers to transformative technology that is itself AI-centric, whereas the first point refers to AI used to speed research on some other transformative technology.)_

[^11]: See <https://stats.stackexchange.com/questions/93523/how-do-we-predict-rare-events> and <https://www.semanticscholar.org/paper/The-limits-of-forecasting-methods-in-anticipating-Goodwin-Wright/c1d3c776a5f8bb131ee9e0cc3a939ab80c7cc0c6>

[^12]: Rather than using Google Scholar and OpenAlex to explore these fields, I decided to only use ArXiV because the Metaculus questions on these subjects used search queries unique to ArXiV.

[^13]: It's worth noting that I forgot to include the terms for the Metaculus question on Few Shot Learning, but have included it in the graph for ArXiV search results.

[^14]: I am not fantastic with time series modeling, but I thought it would be nice to see what an automatically generated ARIMA model had to say about changes in the research terms. If you believe or have evidence of a correct or better parameterization, I would love to hear it! The current ARIMA I use comes from Python's [pmdarima][pmd] (see General Code section).

[^15]: $x(9) = 14000 \cdot (1 + \frac{51.44901}{100})^9$, so $x(9) = 586848$ for AI by the end of 2030. Also, there are 9 years because I am looking at roughly the interval [2021-12-31, 2030-12-31]. $x(9) = 8000 \cdot (1 + \frac{47.80855}{100})^9$, so $x(9) = 269393$ for DL by the end of 2030. The 14000 and 8000 are rough eye-ball estimates for the counts of AI and DL ArXiV e-prints. This should be made exact.

[^16]: [The following only applies to ArXiV queries] The Metaculus question on AI Safety, Interpretability, or Explainability I am referencing here examines the total number of e-prints published in [2021-02-14, 2031-02-14], which I take to mean "total e-prints published roughly during 2021 up to roughly the end of 2030". Since the number of e-prints on AI Safety, Interpretability, or Explainability for 2021 are known (there were 558), I subtract them from the Metaculus community's prediction of 12k (IQR: 6.6k - 19k), giving us approximately 11.5k (IQR: 6k - 18.5k) additional "e-prints published during 2022 up to roughly the end of 2030". Looking at the previous footnote, we know that there might be around 586848 new e-prints on AI and 269393 new e-prints on DL after 2021 up to the end of 2030. Between the years 2000 and 2021, inclusive, 1715-158=1557 e-prints were published on AI Safety, Interpretability, or Explainability. If we use the previous ratios for AI Safety:AI and AI Safety:DL (note that these are do not include "interpretability" or "explainability", and include some 2022 values)
