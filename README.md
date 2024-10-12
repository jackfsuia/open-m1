# open-m1
A roadmap to reproduce OpenAI o1, Combining PRM RL and a RLHF-like RL to train the model to learn infinite CoT (Chain of Thought).
# A roadmap
**Step 1: A good base model.** Find a good math base model M0. For example, deepseek-math-base. The larger it is, the more likely for its emergence of self-backtrack and self-refine abilitis.

**Step 2: Format training.** Finetune M0 to produce solutions in a newline delimited step-by-step format [1]. The result is model M1.

**Step 3: Reinforcement learning with PRM.** Now model M1 can produce formatted infinite CoT. Use a PRM (Process Reward Model) to do the reinforcement learning, which is maximizing the expectation of step rewards. The used dataset should be a math dataset. This might take a long time, since we want the dataset as large as possible, and every generated solution consists of infinite steps of CoT. The result is model M2.

**Step 4: RLHF-like reinforcement learning.** Now model M2 can produce a more reasonable infinite CoT than M1, but still not have too many right answers in its CoT. Now we choose the same dataset, to do RLHF. For one generated solution, if there's no right answer in any of its steps, the reward is 0. If there are one or more than one steps that have the right answer, we cut off the solution till the latest right answer step, and add an END token to its tail, the reward is 1. The result is model M3.

**Step 5: Inference.** During inference of model M3, if time is out, the program adds a "\n Therefore the answer is " to force it to produce the final answer [2]. Then one another model will produce a summary for this whole output.
# Reference
[1] Hunter Lightman, Vineet Kosaraju, Yura Burda, Harri Edwards, Bowen Baker, Teddy Lee, Jan Leike, John Schulman, Ilya Sutskever. Let’s Verify Step by Step.

[2] Nat McAleese, Rai Michael Pokorny, Juan Felipe Ceron Uribe, Evgenia Nitishinskaya, Maja Trebacz, Jan Leike. LLM Critics Help Catch LLM Bugs.
