# LLM Special Tokens & ChatML Reference

A comprehensive reference guide for special tokens, control tokens, and chat markup used across major Large Language Model families.

## Overview

Special tokens are reserved sequences in LLM vocabularies that serve as control signals rather than representing natural language. This reference covers tokens for:

- Message boundaries and turn-taking
- Role markers (system, user, assistant)
- Tool and function calling
- Code completion (Fill-in-the-Middle)
- Vision and multimodal inputs
- Reasoning and chain-of-thought

## Model Families Covered

| Family | Examples |
|--------|----------|
| ChatML/OpenAI | GPT-4, Qwen, Yi, OpenChat |
| Llama/Meta | Llama 2, Llama 3, Alpaca |
| DeepSeek | DeepSeek-V2, DeepSeek-V3, DeepSeek-R1 |
| Mistral | Mistral, Mixtral |
| BERT-style | BERT, RoBERTa, encoder models |

## Live Site

View the reference at: [your-netlify-url.netlify.app](https://your-netlify-url.netlify.app)

## Local Development

This is a static single-page site. To preview locally:

```bash
# Using Python
python -m http.server 8000

# Using Node.js
npx serve .

# Or just open index.html in your browser
open index.html
```

## Deployment

### Netlify

1. Connect your GitHub repository to Netlify
2. Set publish directory to `/` (root)
3. No build command required

### Manual

Simply upload `index.html` to any static hosting service.

## Project Structure

```
.
├── index.html                      # Static site (single file)
├── llm-special-tokens-reference.md # Source content in markdown
└── README.md
```

## Features

- Clean, documentation-style design
- Dark/light mode toggle (respects system preference)
- Syntax highlighting with Prism.js
- Fully responsive layout
- Table of contents navigation
- No build step required

## Contributing

Found an error or want to add a model? Contributions welcome!

1. Fork the repository
2. Make your changes
3. Submit a pull request

## Resources

- [TokenBuster](https://tokenbuster.sentry.security) - Browser tool with 200+ model configs
- [HuggingFace Tokenizers](https://huggingface.co/docs/tokenizers)
- [Chat Templating Guide](https://huggingface.co/docs/transformers/en/chat_templating)

## License

MIT License - feel free to use and adapt for your own projects.
