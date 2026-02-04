# Contributing to Langfuse + Ollama

> **Note:** This is a community fork of [Langfuse](https://github.com/langfuse/langfuse) with **Ollama integration for local LLM evaluation**. This repository maintains compatibility with the original Langfuse project while adding OpenAI-compatible local LLM support.

First off, thanks for taking the time to contribute! ❤️

This project welcomes contributions from the community. This document outlines our conventions regarding development workflow and contribution process.

## About This Fork

This is a community-maintained fork of the original [Langfuse](https://github.com/langfuse/langfuse) project that adds:

- **Local LLM support via Ollama** - Run open-source models locally (Mistral, Gemma, LLaMA, etc.)
- **Zero external API calls** - Everything runs on your machine
- **Free evaluations** - No cloud provider costs

For questions specific to the **Ollama integration**, please open an issue on this repository. For questions about the **core Langfuse features**, refer to the [original Langfuse documentation](https://langfuse.com/docs).

## How to Contribute

We welcome contributions through GitHub pull requests. The best ways to contribute:

- Report bugs or suggest features via [Issues](https://github.com/MohsinCreed/LangfuseOllama/issues)
- Open a [Pull Request](https://github.com/MohsinCreed/LangfuseOllama/pulls) with improvements
- Help improve documentation

If you like the project, you can also show support by:

- Starring the repository
- Sharing it with others
- Referring to this project in your readme
- Contributing improvements

## Making a Change

Before making significant changes, please [open an issue](https://github.com/MohsinCreed/LangfuseOllama/issues). Discussing your proposed changes ahead of time makes the review process smooth.

Once changes are discussed and code is ready, ensure tests pass and open a pull request.

**Focus areas for contributions:**

- Ollama integration improvements
- Local LLM evaluation features
- Docker setup and infrastructure
- Documentation and examples

## Project Overview

This project extends Langfuse with local Ollama integration. Key features:

- Fully local evaluation without cloud dependencies
- Docker-based infrastructure (PostgreSQL, ClickHouse, Redis, MinIO, Ollama)
- Support for any Ollama model via OpenAI-compatible API

For detailed information:

- See [README.md](README.md) for quick start and development setup
- See [SECURITY.md](SECURITY.md) for security and privacy details
- For core Langfuse architecture, refer to the [original documentation](https://langfuse.com/docs)

## Commit Messages

This project follows [conventional commits](https://www.conventionalcommits.org/en/v1.0.0/) for clear, descriptive commit messages.

Examples:

- `feat(ollama): add model auto-detection`
- `fix(docker): resolve ollama container connectivity`
- `docs(setup): improve local deployment guide`
- `refactor(api): improve llm connection logic`

## Code Quality

Before submitting PRs:

```bash
# Lint all packages
pnpm run lint

# Auto-fix linting issues
pnpm run lint:fix

# Format code
pnpm run format
```

## Testing

While Docker-based test infrastructure isn't available in all environments, follow these guidelines when writing tests:

- Keep test blocks independent and decoupled
- Tests should not depend on the outcome of previous tests
- Avoid shared state between tests
- Tests in worker use `vitest`, web uses `jest`

## License

This fork is MIT licensed (see [LICENSE](LICENSE)). The project is based on [Langfuse](https://github.com/langfuse/langfuse) which is also MIT licensed.

For contributions to this fork, no additional CLA is required. By contributing, you agree to have your work licensed under the same MIT license.

## Acknowledgments

This project is built upon the excellent [Langfuse](https://github.com/langfuse/langfuse) project by the Langfuse team. We are grateful for their open-source work and community-friendly contribution guidelines.

If you find this fork useful, please also consider supporting the original Langfuse project!

## Questions?

Feel free to open an issue or discussion on this repository. We're here to help!
