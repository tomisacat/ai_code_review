# ai_code_review

> Important: This project is heavily inspired by [ai-codereviewer](https://github.com/freeedcom/ai-codereviewer)

`ai_code_review` is a GitHub Action that leverages self-deployed Ollama's REST API to provide intelligent feedback and suggestions on
your pull requests. This powerful tool helps improve code quality and saves developers time by automating the code
review process.

## Features

- Reviews pull requests using self-deployed Ollama's REST API.
- Provides intelligent comments and suggestions for improving your code.
- Filters out files that match specified exclude patterns.
- Easy to set up and integrate into your GitHub workflow.

## Setup

1. To use this GitHub Action, you need a self-deployed Ollama service. If you don't have one, deploy your own according to [ollama#Linux](https://github.com/ollama/ollama?tab=readme-ov-file#linux)

2. Add the Ollama service address as a GitHub Secret in your repository with the name `OLLAMA_ADDRESS`. You can find more
   information about GitHub Secrets [here](https://docs.github.com/en/actions/reference/encrypted-secrets).

3. Create a `.github/workflows/code_review.yaml` file in your repository and add the following content:

```yaml
name: Code Review with ollama
on:
  pull_request:
    types:
      - opened
      - synchronize
permissions: write-all
jobs:
  code_review:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v3
      - name: Code Review
        uses: tomisacat/ai_code_review@main
        with:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          OLLAMA_ADDRESS: ${{ secrets.OLLAMA_ADDRESS }}
          exclude: "yarn.lock,dist/**"
```

4. Customize the `exclude` input if you want to ignore certain file patterns from being reviewed.

5. Commit the changes to your repository, and `ai_code_review` will start working on your future pull requests.

## How It Works

The `ai_code_review` GitHub Action retrieves the pull request diff, filters out excluded files, and sends code chunks to
the Ollama's REST API. It then generates review comments based on the AI's response and adds them to the pull request.

## Contributing

Contributions are welcome! Please feel free to submit issues or pull requests to improve the `ai_code_review` GitHub
Action.

Let the maintainer generate the final package (`yarn build` & `yarn package`).

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for more information.
