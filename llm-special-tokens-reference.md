# LLM Special Tokens & ChatML Reference

A comprehensive reference guide for special tokens, control tokens, and chat markup used across major Large Language Model families.

## What Are Special Tokens?

Special tokens are reserved sequences in LLM vocabularies that serve as control signals rather than representing natural language. They tell the model things like:

- Where messages start and end
- Who is speaking (system, user, assistant)
- When to invoke tools or functions
- Where images or other media are located
- When to engage reasoning/thinking modes

These tokens are added to the model's vocabulary during training and have learned semantic meanings. They're essentially "function calls" baked into the tokenizer.

---

## ChatML / OpenAI Style

The most common format, used by OpenAI models and many open-source models (Qwen, Yi, OpenChat, etc.)

| Token | Purpose | Example |
|-------|---------|---------|
| `<\|im_start\|>` | Message block start | `<\|im_start\|>user` |
| `<\|im_end\|>` | Message block end | `Hello!<\|im_end\|>` |
| `<\|system\|>` | System role marker | |
| `<\|user\|>` | User role marker | |
| `<\|assistant\|>` | Assistant role marker | |
| `<\|endoftext\|>` | End of generation (EOS) | |
| `<\|endofprompt\|>` | End of prompt input | |

### ChatML Format Example

```
<|im_start|>system
You are a helpful assistant.
<|im_end|>
<|im_start|>user
Hello, how are you?
<|im_end|>
<|im_start|>assistant
I'm doing well, thank you for asking!
<|im_end|>
```

---

## Llama / Meta Style

Used by Llama 2, Llama 3, and derivative models.

### Llama 2 / Alpaca Style

| Token | Purpose |
|-------|---------|
| `<s>` | Start of sequence (BOS) |
| `</s>` | End of sequence (EOS) |
| `[INST]` | Instruction start |
| `[/INST]` | Instruction end |
| `<<SYS>>` | System prompt start |
| `<</SYS>>` | System prompt end |
| `<unk>` | Unknown token |

### Llama 2 Format Example

```
<s>[INST] <<SYS>>
You are a helpful assistant.
<</SYS>>

Hello, how are you? [/INST] I'm doing well, thank you! </s>
```

### Llama 3 Style

| Token | Purpose |
|-------|---------|
| `<\|begin_of_text\|>` | Sequence start |
| `<\|end_of_text\|>` | Sequence end |
| `<\|start_header_id\|>` | Role header start |
| `<\|end_header_id\|>` | Role header end |
| `<\|eot_id\|>` | End of turn |

### Llama 3 Format Example

```
<|begin_of_text|><|start_header_id|>system<|end_header_id|>

You are a helpful assistant.<|eot_id|><|start_header_id|>user<|end_header_id|}

Hello, how are you?<|eot_id|><|start_header_id|>assistant<|end_header_id|>

I'm doing well, thank you!<|eot_id|>
```

---

## DeepSeek Style

Used by DeepSeek-V2, DeepSeek-V3, DeepSeek-R1, and related models.

| Token | Purpose |
|-------|---------|
| `<｜begin▁of▁sentence｜>` | Sequence start (note: special Unicode) |
| `<｜end▁of▁sentence｜>` | Sequence end |
| `<｜User｜>` | User turn marker |
| `<｜Assistant｜>` | Assistant turn marker |
| `<think>` | Start reasoning/thinking block |
| `</think>` | End reasoning/thinking block |

### DeepSeek-R1 Thinking Example

```
<｜User｜>What is 15 * 23?<｜Assistant｜><think>
Let me calculate this step by step.
15 * 23 = 15 * 20 + 15 * 3
= 300 + 45
= 345
</think>
The answer is 345.
```

---

## Mistral Style

| Token | Purpose |
|-------|---------|
| `<s>` | Start of sequence |
| `</s>` | End of sequence |
| `[INST]` | Instruction start |
| `[/INST]` | Instruction end |
| `[AVAILABLE_TOOLS]` | Tool definitions start |
| `[/AVAILABLE_TOOLS]` | Tool definitions end |
| `[TOOL_CALLS]` | Tool call output |
| `[TOOL_RESULTS]` | Tool results input |

---

## Tool & Function Calling Tokens

Used across various models for agentic capabilities.

| Token | Purpose | Models |
|-------|---------|--------|
| `<\|tool\|>` | Tool role marker | ChatML-based |
| `<\|function\|>` | Function role | ChatML-based |
| `<\|function_call\|>` | Signal function invocation | ChatML-based |
| `<tool_call>` | Function call wrapper start | Qwen, DeepSeek |
| `</tool_call>` | Function call wrapper end | Qwen, DeepSeek |
| `<tool_response>` | Function output start | Qwen, DeepSeek |
| `</tool_response>` | Function output end | Qwen, DeepSeek |
| `<tools>` | Tool definitions block start | Qwen, DeepSeek |
| `</tools>` | Tool definitions block end | Qwen, DeepSeek |
| `[TOOL_CALLS]` | Tool call marker | Mistral |

### Tool Calling Example (Qwen/DeepSeek)

```
<|im_start|>user
What's the weather in Tokyo?
<|im_end|>
<|im_start|>assistant
<tool_call>
{"name": "get_weather", "arguments": {"location": "Tokyo"}}
</tool_call>
<|im_end|>
<|im_start|>tool
<tool_response>
{"temperature": 22, "condition": "sunny"}
</tool_response>
<|im_end|>
<|im_start|>assistant
The weather in Tokyo is sunny with a temperature of 22°C.
<|im_end|>
```

---

## Code & Fill-in-the-Middle (FIM) Tokens

Used for code completion and infilling tasks.

| Token | Purpose | Models |
|-------|---------|--------|
| `<fim_prefix>` | Code before cursor | StarCoder, CodeLlama |
| `<fim_middle>` | Where to generate | StarCoder, CodeLlama |
| `<fim_suffix>` | Code after cursor | StarCoder, CodeLlama |
| `<\|fim_prefix\|>` | FIM prefix (pipe style) | Qwen-Coder |
| `<\|fim_middle\|>` | FIM middle (pipe style) | Qwen-Coder |
| `<\|fim_suffix\|>` | FIM suffix (pipe style) | Qwen-Coder |
| `<PRE>` | Prefix marker | Some models |
| `<SUF>` | Suffix marker | Some models |
| `<MID>` | Middle marker | Some models |

### FIM Example

```
<fim_prefix>def hello_world():
    message = <fim_suffix>
    print(message)
<fim_middle>"Hello, World!"
```

---

## Vision & Multimodal Tokens

Used by Vision-Language Models (VLMs).

| Token | Purpose | Models |
|-------|---------|--------|
| `<image>` | Image placeholder | LLaVA, DeepSeek-VL |
| `<\|image\|>` | Image marker (pipe style) | Various |
| `<\|vision_start\|>` | Vision content start | Qwen-VL |
| `<\|vision_end\|>` | Vision content end | Qwen-VL |
| `<\|vision_pad\|>` | Vision padding | Qwen-VL |
| `<\|image_pad\|>` | Image padding | Various |
| `<\|grounding\|>` | Enable bounding box output | DeepSeek-OCR |
| `<\|ref\|>` | Reference marker | Grounding models |
| `<\|box\|>` | Bounding box marker | Grounding models |
| `<\|quad\|>` | Quadrilateral marker | OCR models |

### Vision Example (DeepSeek-OCR)

```
<image>
Free OCR.
```

```
<image>
<|grounding|>Convert the document to markdown.
```

---

## BERT-Style Tokens (Encoder Models)

Used primarily in encoder-only models for classification, NER, etc.

| Token | Purpose |
|-------|---------|
| `[CLS]` | Classification token (sequence start) |
| `[SEP]` | Separator between segments |
| `[MASK]` | Masked token for MLM training |
| `[PAD]` | Padding token |
| `[UNK]` | Unknown token |

---

## Reasoning & Chain-of-Thought Tokens

Used by reasoning models to separate thinking from final answers.

| Token | Purpose | Models |
|-------|---------|--------|
| `<think>` | Start thinking/reasoning | DeepSeek-R1, QwQ |
| `</think>` | End thinking/reasoning | DeepSeek-R1, QwQ |
| `<reasoning>` | Reasoning block start | Some models |
| `</reasoning>` | Reasoning block end | Some models |
| `<scratchpad>` | Internal working space | Some fine-tunes |
| `</scratchpad>` | End scratchpad | Some fine-tunes |

---

## How to Find Special Tokens for Any Model

### From HuggingFace Model Files

Look for these files in the model repository:

- `tokenizer.json` - Contains full vocabulary and special tokens
- `tokenizer_config.json` - Special token mappings
- `special_tokens_map.json` - Explicit special token definitions
- `generation_config.json` - Generation-related tokens
- `chat_template.jinja` - Jinja2 template showing token usage

### Example: Extracting from tokenizer_config.json

```json
{
  "bos_token": "<|im_start|>",
  "eos_token": "<|im_end|>",
  "pad_token": "<|endoftext|>",
  "chat_template": "{% for message in messages %}..."
}
```

### Using Python

```python
from transformers import AutoTokenizer

tokenizer = AutoTokenizer.from_pretrained("model-name")

# View all special tokens
print(tokenizer.special_tokens_map)
print(tokenizer.all_special_tokens)

# View chat template
print(tokenizer.chat_template)
```

---

## Tools & Resources

- **TokenBuster** - [tokenbuster.sentry.security](https://tokenbuster.sentry.security) - Browser tool with 200+ model configs
- **HuggingFace Tokenizers** - [huggingface.co/docs/tokenizers](https://huggingface.co/docs/tokenizers)
- **Jinja Chat Templates** - [huggingface.co/docs/transformers/chat_templating](https://huggingface.co/docs/transformers/en/chat_templating)
- **LLM Chat Templates Repo** - [github.com/jndiogo/LLM-chat-templates](https://github.com/jndiogo/LLM-chat-templates)

---

## Quick Reference Card

| Model Family | BOS | EOS | Roles | Style |
|--------------|-----|-----|-------|-------|
| ChatML/OpenAI | `<\|im_start\|>` | `<\|im_end\|>` | In token | `<\|im_start\|>role` |
| Llama 2 | `<s>` | `</s>` | `[INST]` tags | `[INST] text [/INST]` |
| Llama 3 | `<\|begin_of_text\|>` | `<\|eot_id\|>` | Header tags | `<\|start_header_id\|>role<\|end_header_id\|>` |
| Mistral | `<s>` | `</s>` | `[INST]` tags | Llama 2 style |
| DeepSeek | `<｜begin▁of▁sentence｜>` | `<｜end▁of▁sentence｜>` | Special markers | `<｜User｜>` / `<｜Assistant｜>` |

---

## Contributing

This reference is maintained as a community resource. Found an error or want to add a model? Contributions welcome!

---

*Last updated: January 2026*

*Sources: HuggingFace documentation, model repositories, Sentry Security research, community contributions*
