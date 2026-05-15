---
layout: post
title: "Federation over text: Insight sharing over multi-agent for reasoning"
date: 2026-05-14
categories: meta
tags: [paper, agentic ai]
---

Good morning, 

I am going to join JPMorgan Chase in june as a machine learning engineer intern and my work i think is going to be focused on multi-agentic systems. They asked me to be upto date with langchain and langgraph and to read about trusts. 

I came across a linkedIn post about the upcoming chicago data night and the presenter is going to talk about her latest work which focuses on memory across multi-agents, will be interesting to read the paper. I am going to use claude to help me understand the paper. 

Key points from abstract - 
1. federation of local reasoning processes of multiple agents 
2. Need to look up traditional distributed learning. This is what claude says - workers compute gradients locally, then synchronize — typically by averaging gradients across all workers (via an all-reduce operation) — so every replica ends up with the same updated weights.
3. I have never understood the word "metacognitive"
4. Claude explained federated learning and about averaging weights across models, seems too simple to work actually. 
5. I was confused about task-level coordination and knowledge-level aggregation and this is what claude explained - "A useful contrast: task-level coordination is like a committee solving a case. Knowledge-level aggregation is like writing the textbook the next committee will read." The textbook would be about a certain domain right, otherwise it would be like having a separate reasoning model. 
6. The model reflects on whether the reasoning process contains reusable techniques and what key skills can be extracted, this is done by prompting the question and the solution for analysis. Is the model smart enough to answer with multiple methods to reach the same answer ? is this relevant ? 

--- I think these points are more like questions i am asking claude at this point ---

7. Isn't insight library just providing curated context to the LLM ? and its being compared with llms having no context 
8. Does the curated context need to be generated using federation over text, how does it compare with just giving one llm all the problems and then inputting the same prompts ? 