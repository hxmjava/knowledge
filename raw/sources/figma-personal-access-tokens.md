# Manage personal access tokens

**Source**: https://help.figma.com/hc/en-us/articles/8085703771159-Manage-personal-access-tokens
**Fetched**: 2026-05-09

---

Personal access tokens allow you to grant access to your data through the Figma API. Some third-party integrations and plugins require a personal access token so that they can be authorized to access your data within Figma.

A personal access token can only be used for a single integration. You must generate a new personal access token for every integration you configure.

> **Note**: Personal access tokens allow third-party programs to access **all** of your files and data in Figma. It's not possible to restrict access when using a personal access token. We recommend only giving this information to trusted third-party integrations.

## Generate a personal access token

1. From the file browser, click the account menu in the top-left corner and select **Settings**.
2. Select the **Security** tab.
3. Scroll to the **Personal access tokens** section, then click **Generate new token**.
4. Enter a name for your new token, assign the scopes you want, and press Return / Enter. For a complete list of the scopes you can assign to your personal access token, see the [developer documentation](https://help.figma.com/hc/en-us/articles/8085703771159).
5. Copy the token that is generated.

> **Note**: The token only displays immediately after being generated. If you navigate away from the page, you will not be able to copy the token and will have to generate a new one.

## Revoke a personal access token

If you no longer want to use a third-party integration, you can block access to your data by revoking the personal access token.

1. From the file browser, click the account menu in the top-left corner and select **Settings**.
2. Select the **Security** tab.
3. Scroll to the **Personal access tokens** section.
4. From the list of personal access tokens, select the token you want to revoke.
5. Click **Revoke access**.

The integration will no longer be able to access your data via the API. If you want to use the integration again in the future, you will need to generate another personal access token and reconfigure the integration.
