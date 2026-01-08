# Reasoning LLMs

[Philip Dhingra](https://philipkd.com/)'s latest thoughts on reasoning LLMs.

# About me

I'm an independent AGI researcher and consultant based in San Francisco.

In late 2019, I built an early prototype for Chain-of-Thought prompting. In 2021, I achieved state-of-the-art (SOTA) for [ARC-AGI-1 on Kaggle (+38% accuracy)](https://www.kaggle.com/competitions/abstraction-and-reasoning-challenge/discussion/234352). Shortly thereafter, I [won a silver medal](https://www.kaggle.com/competitions/birdclef-2021/discussion/243343) in Cornell's BirdCLEF competition. And finally, in 2025, I worked with the ARC Prize Foundation to help build their third dataset, ARC-AGI-3, which is comprised entirely of video games.

You can read more [about me here](https://philipkd.com/) or check out [my LinkedIn](https://www.linkedin.com/in/philipkd/).

# "Thinking" LLMs

Sam Altman wants customers to run ChatGPT queries not just for minutes, but days, maybe even months, to solve hard math problems, such as the [Riemann Hypothesis](https://x.com/polynoamial/status/1834280969786065278). This goal translated into what was the formerly code-named "Strawberry" model, which eventually became the o1 model. In 2024, everybody knew what o1 was, but now, in 2026, the name has been forgotten. GPT 5.2 seamlessly switches to "thinking" mode on a case-by-case basis. At this point, nobody thinks much about the difference between "thinking" and "normal" use of chatbots.

But to restate it, in broad terms, thinking mode is comprised of three layers:
* A base language model trained on a large corpus, such as the Internet
* Fine-tuned reasoning traces
* Prompt engineering (e.g., "of-Thoughts", "majority voting", etc.)

But first, a little background ...

# The "of-Thoughts" family

We're two generations into the "of-Thoughts" strategy for augmenting LLMs. Chain-of-thoughts (CoT), if you will recall, is a technique where, if you ask a chatbot to "think step-by-step," it somehow gives you better answers.

A brief timeline:

* 2022 Oct 31 - [Chain of Thoughts](https://openreview.net/forum?id=_VjQlMeSB_J) (first generation)  
* 2023 May 17 - [Tree of Thoughts](https://arxiv.org/abs/2305.10601) (start of second generation, [discussion](https://www.reddit.com/r/OpenAI/comments/13meqke/tree_of_thoughts_gpt4_problem_solving_improved/))  
* 2023 Oct 11 - [Diversity of Thoughts](https://arxiv.org/abs/2310.07088) ([discussion](https://www.reddit.com/r/ArtificialInteligence/comments/176hcd7/improve_reasoning_in_chatgpt_through_diversity_of/))  
* 2024 Jan 16 - [Boosting of Thoughts](https://openreview.net/forum?id=qBL04XXex6)  
* 2024 Jun 6 - [Buffer of Thoughts](https://arxiv.org/abs/2406.04271)  

But in 2025, there were hardly any interesting "of-Thoughts" papers. What happened?

All attention went towards "post-training" ... 

# Post-training

Shortly after OpenAI released o1, a Chinese competitor, DeepSeek, released R1, which showed that thinking mode could be done much more efficiently than how the American LLMs were doing it. They introduced something called GRPO, or Group Relative Policy Optimization, which fine-tunes LLMs with reinforcement learning. But first, a brief history of fine-tuning.

The first way they fine-tuned LLMs was called supervised fine-tuning, which is similar to how the base LLMs are trained. LLMs start with *unsupervised* training on a large corpus, such as the open Internet, but at that point, they can only predict the next token at the end of a string of text. Model providers then add chat histories of desirable inputs and outputs to the training mix to steer or "fine-tune" dumb predictors into sounding like conversational agents.

RLHF, or Reinforcement Learning with Human Feedback, came next, and is similar to SFT, except you have this army of human testers who rate responses. In SFT, you provide transcripts to steer language prediction towards some desired response. In RLHF, you reward points if a transcript has some desirable properties. It's a subtle, but important, distinction.

GRPO is of the latter framework, and all the improvements in 2025 to thinking mode were in the form of fine-tuning "reasoning traces." So just as SFT and RLHF were trying to turn dumb sentence-finishers into clever-sounding conversational partners, GRPO tries to make CoT processes smarter. CoT, as mentioned above, makes chatbots smarter by spelling out their thinking before giving an answer. These are "reasoning traces."

RLHF, SFT, and GRPO are all instances of "post-training." But there is another CoT-like step that happens after all this post-training, which is prompt engineering. For example:

* If someone asks about problems that have verifiable rewards, such as math, then you make a call to some external tool, such as a calculator.
* You can also initiate thinking mode multiple times in parallel and then have a separate LLM pick what it thinks is the best chain.
* Or you can run a scratch pad or "buffer" to collect temporary thoughts and then have thinking chains based on those thoughts.

As I alluded to earlier, research into the prompt engineering side of things seems to have stalled in 2025, with all attention shifting to fine-tuning reasoning traces. I'm not sure why this happened, but one possibility is that when you fine-tune reasoning traces, you do that all offline, whereas prompt engineering incurs costs while the user is interacting with the chatbot. Or, you can throw millions of dollars of compute into fine-tuning and get incremental gains here and there, whereas with prompt engineering, there's no "dollars-in, smarter-thinking-out."

# AI code assistants

Code generation is another aspect of LLM reasoning that I'm curious about. Here's a rough timeline:

(1 line = 1 quarter)

[2021 Oct 29](https://en.wikipedia.org/wiki/GitHub_Copilot#cite_ref-:0_1-1) - GitHub Copilot plugin released using Codex, a [descendant of GPT-3](https://github.blog/news-insights/product-news/github-copilot-x-the-ai-powered-developer-experience/)  
2022 Q1  
.  
.  
.  
2023 Q1  
.  
.  
2023 Oct 15 - Cursor, which uses GPT-4, has its first post on [Hacker News](https://news.ycombinator.com/item?id=37888477)
2024 Q1
.  
.  
.  
2025 Q1
2025 May - Claude Code becomes generally available
.  
.  
(present)