# Vouch Helm Charts
<a href="https://github.com/jessebot/vouch-helm-chart/releases"><img src="https://img.shields.io/github/v/release/jessebot/vouch-helm-chart?style=plastic&labelColor=blue&color=green&logo=GitHub&logoColor=white"></a>

This is a fork of the official Vouch helm chart with some quality of life updates to match standard helm chart style. It's actively maintained and kept up to date by @jessebot and renovateBot, so if a new version of the Vouch docker image comes out, we'll automatically get a PR to update it :)

## Usage

Make sure you have helm installed. To get started with helm, read their [documentation](https://helm.sh/docs/).
Here's the basics of running this chart, however you'll want to update your [`values.yaml`](./charts/vouch/values.yaml).

```console
helm repo add vouch https://jessebot.github.io/helm-charts/
helm repo update
helm install vouch/vouch vouch --values.yaml
```

Docs for the [`values.yaml`](./charts/vouch/values.yaml) can be found in in the chart [README](./charts/vouch/README.md).

### Using an external secret

You can configure your values.yml for vouch to use an existing Kubernetes Secret for it's config file. Example `values.yaml`:

```yaml
config:
  # -- Allow overriding the config value with an existing secret, like a sealed secret
  existingSecretName: "vouch-existing-secret"
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
Chart documentation is available in [helm-charts licencse](./LICENSE). We've kept it the same as the upstream chart. All credit for the vouch-proxy goes to the [Vouch project](https://github.com/vouch) :)

## Contributing
We'd love to have you contribute! Please refer to our [contribution guidelines](./CONTRIBUTING.md) for details.
