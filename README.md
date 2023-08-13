# Vouch Helm Charts
<a href="https://github.com/jessebot/vouch-helm-chart/releases"><img src="https://img.shields.io/github/v/release/jessebot/vouch-helm-chart?style=plastic&labelColor=blue&color=green&logo=GitHub&logoColor=white"></a>

This is a [fork](https://github.com/jessebot/vouch-helm-chart) of the [official Vouch helm chart](https://github.com/vouch/helm-charts) with some quality of life updates to match standard helm chart style. It's actively maintained and kept up to date by @jessebot and renovateBot, so if a new version of the Vouch docker image comes out, we'll automatically get a PR to update it :)

# Usage

Make sure you have helm installed. To get started with helm, read their [documentation](https://helm.sh/docs/).
Here's the basics of running this chart, however you'll want to update your [`values.yaml`](./charts/vouch/values.yaml).

```console
helm repo add vouch https://jessebot.github.io/helm-charts/
helm repo update
helm install vouch/vouch vouch --values.yaml
```

Docs for the [`values.yaml`](./charts/vouch/values.yaml) can be found in in the chart [README](./charts/vouch/README.md).

## Using Existing Kubernetes Secrets for Private Info

### Existing Secret for the Oauth config

In your values.yaml specify the name of the of the secret and then the names of the keys that will store the sensitive info:

```yaml
config:
  # https://console.developers.google.com/apis/credentials
  oauth:
    # -- existingSecret for clientId, clientSecret, authUrl, tokenUrl,userInfoUrl, callbackUrls, and preferredDomain. 
    # If this value is not empty, we will ignore all of those plain text values and only use your secret keys
    existingSecret: 'my-vouch-oauth-secret'
    # keys in oauth.existingSecret to use for Oauth2 config
    secretKeys:
      # -- key in existingSecret for the clientID from your provider
      clientId: 'clientId'
      # -- key in existingSecret for clientSecret from your provider
      clientSecret: 'clientSecret'
      # -- key in existingSecret for authentication url from your oidc provider
      authUrl: 'authUrl'
      # -- key in existingSecret for token url from your oidc provider
      tokenUrl: 'tokenUrl'
      # -- key in existingSecret for userInfoUrl from your oidc provider
      userInfoUrl: 'userInfoUrl'
      # -- key in oauth.existingSecret for comma seperated list of valid
      # callback urls to use, example value for your key in your existing secert:
      # 'https://vouch.example.com/auth,https://vouch.example.com/login'
      callbackUrls: 'callbackUrls'
      # -- secret key in oauth.existingSecret for your preferred domain
      preferredDomain: 'preferredDomain'
```

Example secret:
```yaml
apiVersion: v1
kind: Secret
metadata:
  name: my-vouch-oauth-secret
# "stringData" doesn't have to be used, but if you use "data", you have to base64 encode the string values below
stringData:
  clientId: 'vouch'
  clientSecret: '6f7dag78dagr4bcfydsuoivh9a8fh89'
  authUrl: 'https://iam.example.com/realms/demo-realm/protocol/openid-connect/auth'
  tokenUrl: 'https://iam.example.com/realms/master/protocol/openid-connect/token'
  userInfoUrl: 'https://iam.example.com/realms/master/protocol/openid-connect/userinfo'
  callbackUrls: 'https://vouch.example.com/auth'
```


### Existing Secret for vouch allowed domains and allowed emails

In your values.yaml specify the name of the of the secret and then the names of the keys that will store the sensitive info:

```yaml
config:
  vouch:
    # -- existingSecret for domains, whiteList, and jwtSecret. If this value is
    # not empty, we ignore vouch.domains, vouch.whiteList, and vouch.jwt.secret
    existingSecret: 'my-vouch-config-secret'
    # keys in vouch.existingSecret to use for vouch config
    secretKeys:
      # -- secret key in vouch.existingSecret with comma seperated list of
      # domains you'd like to allow access from.
      domains: 'domains'
      # -- secret key in vouch.existingSecret with comma seperated list of emails
      # for users that allowed to use SSO via vouch.
      whiteList: 'whiteList'
      # -- secret key in vouch.existingSecret to pass in a secret to used for cookies
      jwtSecret: 'jwtSecret'
```

Make sure that `config.vouch.secretKeys.domains` and `config.vouch.secretKeys.whiteList` are both comma seperated lists.

Example secret:
```yaml
apiVersion: v1
kind: Secret
metadata:
  name: my-vouch-config-secret
# "stringData" doesn't have to be used, but if you use "data", you have to base64 encode the string values below
stringData:
  domains: "coolcats.com,cooldogs.com"
  whiteList: "not-a-dog@gmail.com,cat@coolcats.com"
```
 
### Overriding the entire `config.yaml` for vouch-proxy
You can configure your `values.yml` for vouch to use an existing Kubernetes Secret for it's *ENTIRE* config file. 

Example `values.yaml`:
```yaml
config:
  # -- Allow overriding the config value with an existing secret, like a sealed secret
  overrideConfigExistingSecret: "vouch-existing-secret"
```

Example of setting an existing Secret via the helm cli:

```console
helm install vouch/vouch vouch --set existingSecretName=vouch-existing-secret
```

Here's a Kubernetes Secret containing a Vouch config that uses keycloak as the OIDC provider:

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: vouch-existing-secret
stringData:
  config.yaml: |
    vouch:
      logLevel: debug
      testing: false
      domains:
      - example.com
      whiteList:
      - myuser@myemaildomain.com
      allowAllUsers: false
      cookie:
        maxAge: 900
        secure: true
        domain: example.com
    oauth:
      provider: oidc
      client_id: vouch
      client_secret: 8943hncds9aavy89hn39ncdsa89y79vh79as 
      auth_url: https://iam.example.com/realms/master/protocol/openid-connect/auth
      token_url: https://iam.example.com/realms/master/protocol/openid-connect/token
      user_info_url: https://iam.example.com/realms/master/protocol/openid-connect/userinfo
      scopes:
        - openid
        - email
        - profile
      callback_urls:
        - https://vouch.example.com/auth
      preferredDomain:
```

## License
This uses the [MIT licencse](./LICENSE). We've kept it the same as the upstream chart. All credit for the vouch-proxy goes to the [Vouch project](https://github.com/vouch) :)

## Contributing
We'd love to have you contribute! Please refer to our [contribution guidelines](./CONTRIBUTING.md) for details.
