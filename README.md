# MoLE(Mixture of Lora Experts)
MoLE is a novel approach to fine-tuning large language models (LLMs) for multiple tasks simultaneously, leveraging the concept of specialized LoRA adapters that dynamically adapt the base model's behavior based on task requirements. MoLE is designed to enhance the versatility and performance of pre-trained LLMs by incorporating task-specific/language-specific adapters. These adapters are automatically selected and merged with the base model during inference, guided by a task classifier trained during the fine-tuning process.

<table>
  <tr>
    <td width="40%">
      <img src="https://github.com/adithya-s-k/MoLE/assets/27956426/312a0a83-b253-48fe-87ac-c419670a3428" alt="MoLE Architecture">
    </td>
    <td width="50%">
      <h2>Key Components</h2>
      <h3>Base Model</h3>
      <p>The MoLE architecture starts with a pre-trained base LLM (such as Llama | Mistal | Gemma) that serves as a foundation for all tasks. This base model captures general language understanding and can be fine-tuned for specific tasks.</p>
      <h3>Lora Adapters</h3>
      <p>Lora adapters are specialized modules tailored for individual tasks. Each Lora adapter encapsulates task-specific knowledge and is designed to seamlessly integrate with the base model to enhance its capabilities for the given task.</p>
      <h3>Task Classifier</h3>
      <p>During the fine-tuning process, MoLE trains a task classifier that determines the most appropriate Lora adapter for a given input. This classifier learns to identify task categories and selects the corresponding Lora adapter to apply at runtime.</p>
    </td>
  </tr>
</table>


## Workflow

1. **Fine-tuning**: The base model is fine-tuned on a diverse set of tasks.
2. **Lora Selection**: A task classifier is trained concurrently to predict which Lora adapter to use for each task.
3. **Inference**: During inference, the task classifier identifies the task category of the input, and MoLE seamlessly integrates the corresponding Lora adapter with the base model to generate task-specific outputs.

## Benefits

- **Task Specialization**: MoLE enables the base model to adapt dynamically to diverse tasks without catastrophic forgetting.
- **Improved Performance**: By leveraging task-specific Lora adapters, MoLE achieves enhanced performance across multiple tasks.
- **Scalability**: The modular design of MoLE allows for easy integration of new tasks through the addition of custom Lora adapters.

## Getting Started

To use MoLE for your own tasks, follow these steps:

1. **Prepare Data**: Organize your dataset with labeled examples for each task.
2. **Fine-tuning**: Fine-tune the base LLM using MoLE, specifying the tasks of interest.
3. **Integration**: Implement task-specific Lora adapters and train the task classifier.
4. **Inference**: Deploy MoLE for inference, where it automatically selects and applies the appropriate Lora adapter based on input tasks.


## Installation
Clone the repo:
```
git clone https://github.com/adithya-s-k/MoLE
cd MoLE
```
Create a virtual environment using virtualenv or conda depending on your preferences. We require Python 3.10 or above:
```
conda create -n mole-venv python=3.10 && conda activate mole-venv
```
Install the dependencies. For the default installation, you just need:
```
pip install .
```
If you want to push your results to the Hugging Face Hub, don't forget to add your access token to the environment variable HUGGING_FACE_HUB_TOKEN. You can do this by running:
```
huggingface-cli login
```


## Training Parameters

```yaml
# model arguments
base_model: 
tokenise_model:
model_type: 

# classifer arguments
bert_classifier: true
embedding_classifier: true


# tasks arguments
tasks:
    name_of_task_1:
        dataset_name:
        dataset_subset:
        dataset_split:
        prompt_formate:
        num_epochs: 1
        steps: 
    name_of_task_2:
        dataset_name:
        dataset_subset:
        dataset_split:
        prompt_formate:
        num_epochs: 1
        steps: 

# lora arguments
adapter: qlora #either lora or qlora
lora_r: 32
lora_alpha: 16
lora_dropout: 0.05
lora_target_linear: true
lora_target_modules:
  - gate_proj
  - down_proj
  - up_proj
  - q_proj
  - v_proj
  - k_proj
  - o_proj

# training arguments
gradient_accumulation_steps: 4
micro_batch_size: 2
optimizer: adamw_bnb_8bit
lr_scheduler: cosine
learning_rate: 0.0002

# wandb arguments to track training
wandb_project:
wandb_entity:
wandb_watch:
wandb_name:
wandb_log_model:
    
```


## Contributing

We welcome contributions to MoLE! If you have ideas for improvements or would like to extend MoLE with new features, please open an issue or submit a pull request on our GitHub repository.
