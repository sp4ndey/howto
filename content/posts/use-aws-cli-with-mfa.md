---
title: "Use AWS CLI With MFA"
date: 2024-09-23T23:55:49-07:00
draft: false
tags:
- aws
---

When you have MFA enabled in your AWS account, certain commands may not work with a simple access key and secret key. You need to get a session token and use that instead. Here are the steps to get a session token.

1. Make sure you AWS CLI installed and configured with your access key and secret key. Following steps assume that these credentials are set as the default profile; if not, then add `--profile profile-name` at the end of each command.
1. Find out the ARN of you MFA device.
    ```shell
    aws iam list-mfa-devices
    ```
1. Get code from your MFA device.
1. Get a session token.
    ```shell
    aws sts get-session-token --serial-number arn-of-the-mfa-device --token-code code-from-mfa-device
    ```
    This will return an output like this:
    ```json
    {
        "Credentials": {
            "SecretAccessKey": "secret-access-key",
            "SessionToken": "temporary-session-token",
            "Expiration": "expiration-date-time",
            "AccessKeyId": "access-key-id"
        }
    }
    ```
1. Add these credentials to your AWS CLI configuration. Change `--profile mfa` to whatever profile name you want to use.
    ```shell
    aws configure set aws_access_key_id access-key-id --profile mfa
    aws configure set aws_secret_access_key secret-access-key --profile mfa
    aws configure set aws_session_token temporary-session-token --profile mfa
    ```
1. You can now use the `mfa` profile to run commands that require MFA.
    ```shell
    aws s3 ls --profile mfa
    ```

[source](https://repost.aws/knowledge-center/authenticate-mfa-cli)
