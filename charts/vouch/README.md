# vouch

![Version: 4.0.1](https://img.shields.io/badge/Version-4.0.1-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 0.39](https://img.shields.io/badge/AppVersion-0.39-informational?style=flat-square)

An SSO and OAuth login solution for nginx using the auth_request module.

**Homepage:** <https://github.com/vouch/vouch-proxy/>

## Maintainers

| Name | Email | Url |
| ---- | ------ | --- |
| jessebot | <jessebot@linux.com> |  |

## Source Code

* <https://github.com/vouch/vouch-proxy/>

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity | object | `{}` |  |
| args | list | `[]` | arguments to command for container |
| command | list | `[]` | Allow to specify an alternate command before launching vouch example: command: ['/bin/sh', '-c', 'source /vault/secrets/config && /vouch-proxy'] |
| config.oauth.authUrl | string | `""` | authentication url from your oidc provider |
| config.oauth.callbackUrls | list | `[]` | valid callback urls to use, example https://vouch.example.com/auth |
| config.oauth.clientId | string | `""` | clientID from  your provider |
| config.oauth.clientSecret | string | `""` | clientSecret from your provider |
| config.oauth.existingSecret | string | `""` | existingSecret for clientId, clientSecret, authUrl, tokenUrl, userInfoUrl, scopes, callbackUrls, and preferredDomain. If this value is not empty, we will ignore all of those plain text values and only use your secret keys |
| config.oauth.preferredDomain | string | `""` | preferred domain |
| config.oauth.provider | string | `""` | oauth2 provider, such as keycloak |
| config.oauth.scopes | list | `[]` | array of scopes to get from the provider e.g. [openid, email, profile] |
| config.oauth.secretKeys.authUrl | string | `"authUrl"` | secret key in oauth.existingSecret for authentication url from your oidc provider |
| config.oauth.secretKeys.callbackUrls | string | `"callbackUrls"` | secret key in oauth.existingSecret for commas seperated list of valid callback urls to use, example value for your key in your existing secert: 'https://vouch.example.com/auth,https://vouch.example.com/login' |
| config.oauth.secretKeys.clientId | string | `"clientId"` | secret key in oauth.existingSecret for the clientID from your provider |
| config.oauth.secretKeys.clientSecret | string | `"clientSecret"` | secret key in oauth.existingSecret for clientSecret from your provider |
| config.oauth.secretKeys.preferredDomain | string | `"preferredDomain"` | secret key in oauth.existingSecret for your preferred domain |
| config.oauth.secretKeys.tokenUrl | string | `"tokenUrl"` | secret key in oauth.existingSecret for token url from your oidc provider |
| config.oauth.secretKeys.userInfoUrl | string | `"userInfoUrl"` | secret key in oauth.existingSecret for userInfoUrl from your oidc provider |
| config.oauth.tokenUrl | string | `""` | token url from your oidc provider |
| config.oauth.userInfoUrl | string | `""` | user info Url from your oidc provider |
| config.overrideConfigExistingSecret | string | `""` | Allow overriding the ENTIRE config.yaml value with an existing secret, like a sealed secret. If not empty string, ALL  values under config are ignored except for config.existing. For all possible config.yaml values, see: https://github.com/vouch/vouch-proxy/blob/master/config/config.yml_example |
| config.vouch.allowAllUsers | bool | `false` | whether or not to allow ALL users to login |
| config.vouch.domains | list | `[]` | array of specific domains you'd like to allow access from |
| config.vouch.existingSecret | string | `""` | existingSecret for domains, whiteList, and jwtSecret. If this value is not empty, we ignore vouch.domains, vouch.whiteList, and vouch.jwt.secret |
| config.vouch.jwt.secret | string | `""` | pass in a secret to used for cookies |
| config.vouch.logLevel | string | `"debug"` | logging level for vouch |
| config.vouch.port | int | `9090` | the container port for vouch |
| config.vouch.secretKeys.domains | string | `"domains"` | secret key in vouch.existingSecret with comma seperated list of domains you'd like to allow access from. Example secret value in your existing secret: 'coolcats.com,cooldogs.com' |
| config.vouch.secretKeys.jwtSecret | string | `"jwtSecret"` | secret key in vouch.existingSecret to pass in a secret to used for cookies |
| config.vouch.secretKeys.whiteList | string | `"whiteList"` | secret key in vouch.existingSecret with comma seperated list of emails for users that allowed to use SSO via vouch. Example secret value in your 'friend@coolcats.com,kitty@coolcats.com' |
| config.vouch.testing | bool | `false` | if you enable this, it will    force all 302 redirects to be rendered as a webpage with a link |
| config.vouch.whiteList | list | `[]` | array of emails for users that allowed to use SSO via vouch |
| deploymentAnnotations | object | `{}` |  |
| extraEnvVars | list | `[]` | An array to add extra environment variables |
| fullnameOverride | string | `""` |  |
| image.pullPolicy | string | `"IfNotPresent"` | image pullPolicy, set to always if using an image with the latest tag |
| image.repository | string | `"quay.io/vouch/vouch-proxy"` |  |
| image.tag | string | `""` | change the tag we use for the vouch docker image |
| imagePullSecrets | list | `[]` |  |
| ingress.annotations | object | `{}` |  |
| ingress.enabled | bool | `false` |  |
| ingress.hosts[0] | string | `"chart-example.local"` |  |
| ingress.paths[0] | string | `"/"` |  |
| ingress.tls | list | `[]` |  |
| nameOverride | string | `""` |  |
| nodeSelector | object | `{}` |  |
| podAnnotations | object | `{}` |  |
| podSecurityContext | object | `{}` | securityContext for the pod. see more: https://kubernetes.io/docs/tasks/configure-pod-container/security-context/ |
| probes.liveness.enabled | bool | `true` |  |
| probes.liveness.failureThreshold | int | `5` |  |
| probes.liveness.initialDelaySeconds | int | `0` |  |
| probes.liveness.periodSeconds | int | `10` |  |
| probes.liveness.successThreshold | int | `1` |  |
| probes.liveness.timeoutSeconds | int | `1` |  |
| probes.readiness.enabled | bool | `true` |  |
| probes.readiness.failureThreshold | int | `5` |  |
| probes.readiness.initialDelaySeconds | int | `0` |  |
| probes.readiness.periodSeconds | int | `10` |  |
| probes.readiness.successThreshold | int | `1` |  |
| probes.readiness.timeoutSeconds | int | `1` |  |
| probes.startup.enabled | bool | `true` |  |
| probes.startup.failureThreshold | int | `30` |  |
| probes.startup.initialDelaySeconds | int | `5` |  |
| probes.startup.periodSeconds | int | `10` |  |
| replicaCount | int | `1` | how many pod replicas to deploy |
| resources | object | `{}` |  |
| securityContext | object | `{}` | securityContext for the container. see more: https://kubernetes.io/docs/tasks/configure-pod-container/security-context/ |
| service.externalTrafficPolicy | string | `nil` |  |
| service.port | int | `9090` |  |
| service.type | string | `"ClusterIP"` |  |
| serviceAccount.annotations | object | `{}` | Annotations to add to the service account |
| serviceAccount.create | bool | `true` | Specifies whether a service account should be created |
| serviceAccount.name | string | `nil` | The name of the service account to use. If not set and create is true, a name is generated using the fullname template |
| tolerations | list | `[]` |  |

----------------------------------------------
Autogenerated from chart metadata using [helm-docs v1.11.0](https://github.com/norwoodj/helm-docs/releases/v1.11.0)
