# Rebuttal Update

## Q1, Reviewer do3r: Prove the instruction is a true semantic anchor rather than a positional artifact.

Modality instruction is a **semantic instruction** for guiding modality following, whereas $S_{constrain}$ only restricts output format and plays no semantic role in this setting. In the original input, modality instruction precedes $S_{constrain}$. To verify its semantic role, we conducted three control studies:

**Exp 1:** We swapped the input order of modality instruction and $S_{constrain}$ and performed causal attention analysis to compare the importance of attention flow from modality cues to **either modality instruction or $S_{constrain}$** for modality following. Results in the **modality_pre_constraint.pdf**, **modality_post_constraint.pdf** show that 
**cutting the attention flow from modality cues to modality instruction causes a significant drop in middle layers, while cutting the attention flow to $S_{constrain}$ has almost no effect**, regardless of the position of the modality instruction.

**Exp 2:** To further rule out positional interference, we introduced a longer general system prompt $S_{sys}$, "You are a helpful and honest assistant who strictly follows all user instructions and provides accurate responses ..." after the modality instruction to **increase distance between modality instruction and the final token**. Results of casual attention analysis (**modality_begin.pdf**) confirm the same pattern: cutting attention flow from modality cues to modality instruction hurts performance of modality following; but cutting attention flow to other instructions ($S_{sys}$ and $S_{constrain}$) does not.

**Exp 3:** Based on Exp 2, we placed the modality instruction between $S_{sys}$ and $S_{constrain}$ to **further isolate the modality instruction**. Then causal attention analysis shows results similar to **Exp 2** in the **modality_middle.pdf**.

These findings explicitly rule out positional bias, confirming that the modality instruction functions as a genuine semantic anchor rather than a mere positional artifact.

Note, in modality_begin.pdf and modality_middle.pdf, $\\nrightarrow$ Constraint Inst represents that we cut the attention flow from modality cues to system prompt and original constraint.


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
