# Rebuttal Update

## Q1, Reviewer do3r: Prove the instruction is a true semantic anchor rather than a positional artifact.
**Modality instruction** is the **semantic instruction** used to guide MLLMs for modality following. But $S_constrain$ is only used to constrain the output format, **which is not a semantic instruction in modality following setting**. To decouple semantic roles from positional bias, we performe a causal attention analysis to compare the attention flow from modality cues to either modality instruction or $S_{constrain}$ across varying prompt positions. Preliminary experiments indicate that placing the modality instruction at the very beginning of the prompt severely degrades the prefermances of Text Following. Therefore, we move the modality instruction to the middle of the prompt and conduct a control study by **swapping the relative order of the modality instruction and $S_{constrain}$**. 

The results are provided in **modality_pre_constraint.pdf** and **modality_post_constraint.pdf**. We observe that regardless of the instruction's position, **blocking attention from modality cues to the modality instruction results in a significant decline for modality-following**. In contrast, **blocking attention to $S_{constrain}$ has almost no impact**. These findings explicitly rule out positional bias, confirming that the modality instruction functions as a genuine semantic anchor rather than a mere positional artifact.


## W1, Reviewer 3Qm7: The causal attention results by varying the ratio of original test data.

1. The causal attention results by varying the ratio of test data (Figure 2)
We provide Figure2_qwen_0.2.pdf, Figure2_qwen_0.4.pdf, Figure2_qwen_0.6.pdf, Figure2_qwen_0.8.pdf, and Figure2_qwen_1.0.pdf to demonstrate the impact of different test data ratios on the causal attention results presented in Figure 2 of the submitted manuscript.
2. The causal attention results by varying the ratio of test data (Figure 3a)
We provide Figure3_qwen_0.2.pdf, Figure3_qwen_0.4.pdf, Figure3_qwen_0.6.pdf, Figure3_qwen_0.8.pdf, and Figure3_qwen_1.0.pdf to observe the influence of changing test data ratios on the results shown in Figure 3 (a) of the submitted manuscript.

These results visualize the stability of the identified information flow pathways across varying data scales.

## W1, Reviewer 7J4R: The contribution of MLP for the token of following modality and the competitor modality at the last generated position.
Text_Following.pdf representates the MLP contribution for data of Following Text modality and Vision_Following.pdf representates the MLP contribution for data of Following Vision modality.
MLP contribution refers to calculating the logit difference between the last token before and after passing through MLP and the LLM unembedding space.

## Q2, Reviewer obWf: The results removing the binary distribution constraint in Eq. 6 to quantify the results of the attention mask.
We remove the binary distribution constraint in Eq. 6 to quantify the results of the attention mask detailed in qwen_no_binary.pdf, and compared it with Fig 3(a). We find that after removing the binary distribution constraint, there was a significant decrease for I_NSSD within Layers 0-2 for Text Following. Upon further analysis, we find that blocking starting layer causes an increase in the probability of tokens beyond the modality following space, which interfered with the judgment of modality following. 

## W1 & Q1, Reviewer obWf: The results of causal attention analysis for InternVL3-14B
we conducted causal attention analysis on InternVL3-14B. The results (Fig2_InterVL3-14B.pdf and Fig3_InterVL-14B.pdf) show that the **fundamental mechanistic conclusions of instruction anchors remain highly consistent with 7B models**. This demonstrates the generalizability of our findings to larger-scale MLLMs. 
