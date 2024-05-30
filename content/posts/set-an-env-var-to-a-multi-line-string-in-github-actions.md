---
title: "Set an Environment Variable to a Multi-line String in GitHub Actions"
date: 2024-05-07T18:46:37-07:00
draft: false
tags:
- github
---

When creating GitHub Actions workflows, it's often useful to set environment variables to pass info from one step to the next.

Setting an environment variable to a single-line string is easy. Assuming `my-cmd` is any command that produces a single-line output, you can set the variable like this:

```yaml
steps:
  - name: Set environment variable
    run: echo "MY_ENV_VAR=$(my-cmd)" >> "$GITHUB_ENV"
```

And use `$MY_ENV_VAR` or `${{ env.MY_ENV_VAR }}` in subsequent steps.

But this doesn't work for multi-line strings. If you try to do that, you will see an error like:

```shell
Error: Unable to process file command 'env' successfully.
Error: Invalid format ...
```

To correctly set an environment variable to a multi-line string, you have to use a different syntax. Assuming `my-cmd` is any command that produces a multi-line output, you can set the variable like this:

```yaml
steps:
  - name: Set environment variable
    run: |
      {
        echo "CHANGELOG<<EOF"
        echo "$(my-cmd)"
        echo EOF
      } >> "$GITHUB_ENV"
```

After this, you can once again use `$MY_ENV_VAR` or `${{ env.MY_ENV_VAR }}` in subsequent steps.

[source](https://docs.github.com/en/actions/using-workflows/workflow-commands-for-github-actions#multiline-strings)
