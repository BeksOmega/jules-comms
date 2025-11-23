# Send Feedback to Jules

[![Built with Jules](https://img.shields.io/badge/Built%20with-Jules-715cd7?link=https://jules.google)](https://jules.google)

This GitHub Action facilitates a feedback loop for [Jules](https://jules.google). It triggers when a pull request review is submitted. It checks if the review comes from an authorized user and if the PR was created by Jules. If these conditions are met, it sends the review summary and line comments back to the Jules session, allowing Jules to incorporate the feedback.

## Prerequisites

Before using this action, you must have:

1.  **Authenticated with GitHub at [jules.google.com](https://jules.google.com).**
2.  **A Jules API Key:** Generate an API key from your Jules account settings. For more information, see the [Jules API documentation](https://developers.google.com/jules/api).
3.  **Stored the API key as a secret:** You will need to add this as a secret in your GitHub repository. For more information, see the [GitHub documentation on using secrets in GitHub Actions](https://docs.github.com/en/actions/security-guides/using-secrets-in-github-actions).

## Inputs

| Input | Description | Required |
| :--- | :--- | :--- |
| `jules_api_key` | **Required.** The Jules API key to use for authentication. Store this as a secret in your repository settings. | `true` |
| `feedback_users` | **Required.** Comma-separated list of GitHub usernames authorized to provide feedback. | `true` |

## Usage

Here's an example of how to use the Send Feedback to Jules action in your workflow:

```yaml
name: Send Feedback to Jules

on:
  pull_request_review:
    types: [submitted]

jobs:
  send-feedback:
    runs-on: ubuntu-latest
    permissions:
      contents: read
      pull-requests: read
    steps:
      - name: Send Feedback
        uses: BeksOmega/jules-comms@v1.0.0 # Replace with the actual repository name and version
        with:
          jules_api_key: ${{ secrets.JULES_API_KEY }}
          feedback_users: "octocat,monalisa"
```

**Note:** This action ignores reviews from the user who started the Jules task, preventing feedback loops from the bot itself or the initiator if they review their own PR (which is rare but possible).

## Attribution

If you find this action useful, spread the word by adding the "Built with Jules" shield to your `README.md`:

```markdown
[![Built with Jules](https://img.shields.io/badge/Built%20with-Jules-715cd7?link=https://jules.google)](https://jules.google)
```

## Learn More

For more information on Jules and how to get the most out of it, please visit the [Jules documentation](https://jules.google/docs).
