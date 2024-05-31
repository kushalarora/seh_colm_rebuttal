This repository contains two files.
1. **seh_paper_w_decoding_algorithm.pdf**: This is the updated paper, which contains a simple entropy-aware sampling algorithm (Section 4). This operationalizes the stable entropy hypothesis and proposes an algorithm that can leverage SEH to build a mostly greedy decoding algorithm.
2. **stable_entropy_analysis_colm_rebuttal.ipynb**: This is a Jupyter notebook containing the experiments requested by the reviewers. 


The experiments presented are:
1. The existence of the stable entropy baseline and stable entropy zone under a Gemma-2B, one of the latest model from Google. These stable entropy baseline and zone plots are generated with three datasets.
   - Wikipedia: This is the same dataset from the paper, but results presented with Gemma-2B
   - CC News: News dataset with longer sequences which plots stable entropy baseline upto 800 tokens.
   - WritingPrompts: Story generation dataset with long stories, which shows the stable entropy behavior exists for non-news and non-wiki domains.
2. The average (negative) log probabilities for all three as requested by Reviewer hKRX. 
3. The correlational plots for the story generation and longer Wikipedia text completion setting.

 
 ### Correlational experiments:

 #### Story Generation:
We evaluated Gemma on the story generation task with the writing prompts dataset. This addresses reviewer 8MM8 concern that wikipedia text completion might be a bit memorization-focused task. 
In this, we use the Gemma-2B model to generate the story for a given prompt using the following template.

```
Write a story based on the given writing prompt:
Prompt: {instruction} 
Story:
```

We limit the prompts to 256 tokens and generate up to a maximum length of 1024 tokens. We evaluate four decoding approaches: temperature sampling, typical sampling, top-k sampling, and top-p sampling. 

The hyperparameters evaluated are:
- Temperatures: 0.001 0.01 0.1 0.5 0.7 1.0 1.2 1.5
- Top-p (p): 0.15 0.25 0.4 0.5 0.75 0.85 0.9 0.95
- Typical (tau): 0.15 0.25 0.4 0.5 0.75 0.85 0.9 0.95
- Top-k: 5 10 25 50 75 100 500 1000

We observe a similar correlational pattern between Mauve and the entropy violation ratio (EVR), and the repeat\_score@5 and the entropy lower-bound violation ratio (ELVR) as observed with the original Wikipedia text completion experiments from the paper


#### Longer Wikipedia Text Completion Experiment:
We also repeat our Wikipedia completion experiments with prompts up to 256 tokens and generate up to a length of 1024 tokens. This was requested by reviewer k4JZ. We again observe similar correlations as observed in the original experiments indicating our findings hold for newer models and longer sequence lengths. We test the same decoding algorithms and same hyperparameters as above. 

The correlation coefficients are:

EVR vs Mauve: -0.9864
ELVR vs RepeatScore@5: 0.98922




  
