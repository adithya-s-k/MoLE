# MoLE(Mixture of Lora Experts)



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