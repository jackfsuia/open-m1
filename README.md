# open-m1
A roadmap to reproduce OpenAI o1, Combining PRM RL and a RLHF-like RL to train the model to learn infinite CoT (Chain of Thought).
# A roadmap
**Step 1: A good base model.** Find a good math base model M0. For example, deepseek-math-base. The larger it is, the more likely for its emergence of self-backtrack and self-refine abilitis.

**Step 2: Format training.** Finetune M0 to produce solutions in a newline delimited step-by-step format [1] for PRM training. The result is model M1.

**Step 3: PRM reinforcement learning.** Now model M1 can produce formatted CoT. Train a PRM like [1]. Use it to do the reinforcement learning for M1, of which object is maximizing the expectation of step rewards. Then this model is used to train PRM again... run as many iterations as possible. The result is model M2.

**Step 4: Inference.** During inference of model M2, if time is out, the program adds a "\n Therefore the answer is " to force it to produce the final answer [2]. Then one another model will produce a summary for this whole output.

# Reference
[1] Hunter Lightman, Vineet Kosaraju, Yura Burda, Harri Edwards, Bowen Baker, Teddy Lee, Jan Leike, John Schulman, Ilya Sutskever. Let’s Verify Step by Step.

[2] Nat McAleese, Rai Michael Pokorny, Juan Felipe Ceron Uribe, Evgenia Nitishinskaya, Maja Trebacz, Jan Leike. LLM Critics Help Catch LLM Bugs.
