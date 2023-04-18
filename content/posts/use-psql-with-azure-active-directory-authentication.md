---
title: "Use psql with Azure Active Directory authentication"
date: 2023-04-17T22:51:26-07:00
draft: false
tags:
- azure
- postgres
- psql
---

I needed to connect to an [Azure Database for PostgreSQL](https://azure.microsoft.com/en-us/products/postgresql/) which uses [Azure Active Directory](https://azure.microsoft.com/en-us/products/active-directory) for authentication. Despite the many GUI clients available, I prefer using [psql](https://www.postgresql.org/docs/current/app-psql.html). Fortunately, it's fairly easy to connect using psql.

The following steps are taken from [here](https://learn.microsoft.com/en-us/azure/postgresql/single-server/how-to-configure-sign-in-azure-ad-authentication).

### Step 1 - Install Azure CLI
On macOS, the simplest method is to use Homebrew:

```shell
brew update && brew install azure-cli
```

Detailed instructions can be found [here](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli-macos).

### Step 2 - Login to Azure
```shell
az login
```

This command will open a browser window where you can login to Azure.

### Step 3 - Retrieve and set Azure AD access token as the password
Next, we need to get an access token from Azure AD and set that in the `PGPASSWORD` environment variable so psql can access it. This is easy to do if you have [jq](https://stedolan.github.io/jq/) installed.

```shell
export PGPASSWORD=$(az account get-access-token --resource-type oss-rdbms | jq -r '.accessToken')
```

### Step 4 - Connect using psql
That was it! You are ready to connect to the server using psql:

```shell
psql "host=... user=... dbname=... sslmode=require"
```

You can also combine the previous two commands, which can be useful if you want to create an alias:

```shell
PGPASSWORD=$(az account get-access-token --resource-type oss-rdbms | jq -r '.accessToken') psql "host=... user=... dbname=... sslmode=require"
```
