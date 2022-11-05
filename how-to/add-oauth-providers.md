---
description: Implement custom OAuth providers to Feedbacky.
---

# Add OAuth Providers

{% hint style="warning" %}
<mark style="color:orange;">**Citation needed**</mark>

This section is currently undocumented by the developer.
{% endhint %}

{% code title="oauth_providers.yml" %}
```yaml
discord:
  provider-data:
    name: Discord
    oauth-link: https://discordapp.com/api/oauth2/authorize?client_id={CLIENT_ID}&redirect_uri={REDIRECT_URI}&response_type=code&scope=identify%20email&state=
    icon: https://static.plajer.xyz/svg/login-discord.svg
    color: "#7289da"
  environment-variables:
    enabled: OAUTH_DISCORD_ENABLED
    redirect-uri: OAUTH_DISCORD_REDIRECT_URI
    client-id: OAUTH_DISCORD_CLIENT_ID
    client-secret: OAUTH_DISCORD_CLIENT_SECRET
  oauth:
    token-url: https://discordapp.com/api/oauth2/token
    authorization-property: Bearer {TOKEN}
    user-url: https://discordapp.com/api/users/@me
  data-fields:
    id: id
    email: email
    username: username
    # Discord doesn't show avatar url instead shows hash, we need the url
    avatar: null
    email-verified: verified
github:
  provider-data:
    name: GitHub
    oauth-link: https://github.com/login/oauth/authorize?client_id={CLIENT_ID}&redirect_uri={REDIRECT_URI}&scope=read%3Auser%20user%3Aemail&state=
    icon: https://static.plajer.xyz/svg/login-github.svg
    color: "#333333"
  environment-variables:
    enabled: OAUTH_GITHUB_ENABLED
    redirect-uri: OAUTH_GITHUB_REDIRECT_URI
    client-id: OAUTH_GITHUB_CLIENT_ID
    client-secret: OAUTH_GITHUB_CLIENT_SECRET
  oauth:
    token-url: https://github.com/login/oauth/access_token
    authorization-property: token {TOKEN}
    user-url: https://api.github.com/user
  data-fields:
    id: id
    email: email
    username: login
    avatar: avatar
    email-verified: null
google:
  provider-data:
    name: Google
    oauth-link: https://accounts.google.com/o/oauth2/v2/auth?client_id={CLIENT_ID}&response_type=code&scope=https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fuserinfo.email%20https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fuserinfo.profile&redirect_uri={REDIRECT_URI}&state=
    icon: https://static.plajer.xyz/svg/login-google.svg
    color: "#db4437"
  environment-variables:
    enabled: OAUTH_GOOGLE_ENABLED
    redirect-uri: OAUTH_GOOGLE_REDIRECT_URI
    client-id: OAUTH_GOOGLE_CLIENT_ID
    client-secret: OAUTH_GOOGLE_CLIENT_SECRET
  oauth:
    token-url: https://www.googleapis.com/oauth2/v4/token
    authorization-property: Bearer {TOKEN}
    user-url: https://www.googleapis.com/oauth2/v1/userinfo?alt=json
  data-fields:
    id: id
    email: email
    username: name
    avatar: picture
    email-verified: email_verified
gitlab:
  provider-data:
    name: GitLab
    oauth-link: https://gitlab.com/oauth/authorize?client_id={CLIENT_ID}&redirect_uri={REDIRECT_URI}&response_type=code&scope=read_user%20email&state=
    icon: https://static.plajer.xyz/svg/login-gitlab.svg
    color: "#fca121"
  environment-variables:
    enabled: OAUTH_GITLAB_ENABLED
    redirect-uri: OAUTH_GITLAB_REDIRECT_URI
    client-id: OAUTH_GITLAB_CLIENT_ID
    client-secret: OAUTH_GITLAB_CLIENT_SECRET
  oauth:
    token-url: https://gitlab.com/oauth/token
    authorization-property: Bearer {TOKEN}
    user-url: https://gitlab.com/api/v4/user
  data-fields:
    id: id
    email: email
    username: username
    avatar: avatar_url
    email-verified: null
```
{% endcode %}
