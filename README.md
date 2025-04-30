# Finetune_LLM_with_RLHF


RLHF (Reinforcement Learning from Human Feedback) is an important component of the current training method of advanced language models. It helps include people’s feedback when finetuning models, ultimately making the model more valuable and secure.

## Ways to train base model

### 1. Prompting

Prompting is a technique that improves the performance of LLMs by providing the model with a prompt specific to the task.

For example, suppose you wanted an LLM to give you cooking advice. In that case, you might want to add something such as “Act as a professional Michellene chef” at the beginning of your query. The LLM would then use this prompt to “act as an experienced cook.”

Prompting is a simple way to improve the performance of LLMs. However, it requires a prompt design and is less effective for tasks requiring additional information and lexicon than the pre-trained LLM was trained upon.

### 2. Fine-tuning

Fine-tuning is a technique that improves the performance of LLMs by training them on particular datasets — examples of the desired input and output.

For example, you want to fine-tune an LLM to translate English to Arabic. In that case, you need to provide a dataset of English-Arabic translation pairs.

Fine-tuning is usually more effective than prompting for tasks that require the LLM to learn a lot of new data and information. However, it requires more data and computational resources.

### 3. Fine-tuning + RLHF

Fine-tuning with reinforcement learning from human feedback (RLHF) is a technique that improves the performance of LLMs by training them on particular datasets of labeled data ranked by human evaluators. Such data includes examples of the desired input and output for the task and feedback from human evaluators on the production quality.

Fine-tuning with RLHF is usually more effective than fine-tuning alone, especially for tasks requiring an LLM to learn human values and preferences. However, it requires even more data, computational resources, and human effort.

## RLHF Pipeline
Our RLHF pipeline involves taking a pre-trained model and refining it through supervised training. Afterward, the updated model is further refined using proximal policy optimization.

The RLHF pipeline can be summed up as a 3-step training process:

1. **Refined training of the pre-trained model through supervision**

    We either generate or select prompts (potentially from a dataset or database) and request humans to produce high-quality responses. We utilize this data collection to finetune the pre-existing base model in a guided manner.

2. **Development of a model for providing rewards**

    We utilize the finetuned model via supervised training to construct a reward model for the next step. This involves generating multiple responses for each prompt and having individuals rank them according to preference.

     To transform the model from RLHF pipeline step 1 to a reward model, we replace its output layer (the next-token layer) with a regression layer with a single output node.

3. **Additional refinement using proximal policy optimization (PPO)**
    We employ the reward model (v2) to finetune further the previous model that underwent supervised finetuning (v1).

    We adjust the v1 model using proximal policy optimization (PPO) guided by the reward scores obtained from the reward model we established in RLHF pipeline step 2.

