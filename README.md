# Pull Request Policy Checker

This is a GitHub action to check if the pull request complies the project's
policy for pull requests.

## How to use

Include this yaml code into your GitHub action file:

```yaml
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - name: Check pull reques policy
        uses: lorien/pr-policy-checker@main
        with:
          restricted-words: "ai,mcp,apify"
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          GITHUB_REPOSITORY_OWNER: ${{ github.repository_owner }}
          GITHUB_REPOSITORY_NAME: ${{ github.event.repository.name }}
          PR_NUMBER: ${{ github.event.pull_request.number }}
```

In `restricted-words` parameter, you specify a comma separted list of words which must not
be in the title or the description of the pull request being checked. Under the hood, each
of these words is transformed into regular expression bounded by `\b` token, then the
expression is checked for match in the title and the description of the pull request. For
example, the word "ai" becomes the regular expression "\bai\b". These regular expressions
are checked with ignoring the case of letters.

All environment varaibles specified in `env` section of the example are mandatory!
