# Reasoning LLMs

[Philip Dhingra](https://philipkd.com/)'s latest thoughts on reasoning LLMs.

# About me

I'm an independent AGI researcher and consultant based in San Francisco, and I co-work out of the Canopy Jackson Square office.

During the pandemic, I built a prototype for Chain-of-Thought prompting and then achieved SOTA for [ARC-AGI on Kaggle (+38% accuracy)](https://www.kaggle.com/competitions/abstraction-and-reasoning-challenge/discussion/234352). Afterwards, I [won a silver medal](https://www.kaggle.com/competitions/birdclef-2021/discussion/243343) in Cornell's BirdCLEF competition. You can read more [about me here](https://philipkd.com/) or check out [my LinkedIn](https://www.linkedin.com/in/philipkd/).

# Multi-query problem-solving

Sam Altman wants customers to run ChatGPT queries not just for minutes, but days, maybe even months, to solve hard math problems, such as the [Riemann Hypothesis](https://x.com/polynoamial/status/1834280969786065278), or to find new cancer drugs. However, the reception to OpenAI's latest model, o1-preview, has been lukewarm, at best. What went wrong?

Open-source researchers like myself are still trying to reverse-engineer o1, and so far, it looks like a bespoke version of either Tree-of-Thoughts (ToT) or one of the other "of-Thoughts" approaches. (see below) I believe ToT-style approaches can bear fruit if we focus on hard, not soft, feedback. Not every problem would apply here, but consider either Game of 24 or ARC-AGI (the subject of my research). With these "puzzles," you don't have to wait for the hidden test set to validate the model's predictions. With Go24, you can simply check whether the arithmetic operations get you to 24. With ARC-AGI, if you use a code-gen approach, like what [Ryan Greenblat did](https://redwoodresearch.substack.com/p/getting-50-sota-on-arc-agi-with-gpt), you can just run the code against the inputs and test for consistency.

At every reasoning step, you can mathematically verify whether ToT got it right. This way, the LLM builds true experience, as opposed to what it appears o1 is doing, which is using the LLM to analyze its own prompt outputs. o1 currently recapitulates some of the same garbage-in/garbage-out traps that lots of LLM research has fallen into over the last two years. Everybody thought that more parameters, better prompts, larger context windows, or multiple agents would provide categorical improvements to LLMs. But now we're in the winter of AI discontent, feeling like these gains are starting to "log out," i.e., proving to be sources of logarithmic—not exponential—gains.

But what if we could provide hard deterministic feedback for systems that are run outside the LLM, as opposed to the soft fuzzy feedback from the LLM itself? Couldn't we escape the garbage-in/garbage-out trap?

# The "of-Thoughts" family

We're two generations into the "of Thoughts" strategy for augmenting LLMs, and progress is moving fast. AI critics like Gary Marcus mock these as mere "prompt engineering" techniques, but when you start to get to the multi-query methods, as shown in Tree-of-Thoughts and [OpenAI's o1](https://openai.com/index/introducing-openai-o1-preview/), it's apparent we've only scratched the surface.

Here is a brief timeline (1 line = 1 month)

2022 Oct 31 - [Chain of Thoughts](https://openreview.net/forum?id=_VjQlMeSB_J) (first generation)  
.  
.  
.  
.  
.  
.  
2023 May 17 - [Tree of Thoughts](https://arxiv.org/abs/2305.10601) (start of second generation, [discussion](https://www.reddit.com/r/OpenAI/comments/13meqke/tree_of_thoughts_gpt4_problem_solving_improved/))  
.  
.  
.  
.  
2023 Oct 11 - [Diversity of Thoughts](https://arxiv.org/abs/2310.07088) ([discussion](https://www.reddit.com/r/ArtificialInteligence/comments/176hcd7/improve_reasoning_in_chatgpt_through_diversity_of/))  
.  
.  
2024 Jan 16 - [Boosting of Thoughts](https://openreview.net/forum?id=qBL04XXex6)  
.  
.  
.  
.  
.  
2024 Jun 6 - [Buffer of Thoughts](https://arxiv.org/abs/2406.04271)  
.  
.  
.  
.  
*present*
