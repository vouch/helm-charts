## Changelog

3.2.0
  * Add an option to set extra self-signed CA files

3.1.0
  * Add extraEnvVars option to add env variables to the vouch deployment

3.0.7
  * Fix the README.md file. It's no longer a template.

3.0.6
  * Allow vouch-proxy to default the secret at startup


2.0.0
  * Require Vouch secret to be set (#8 thanks @punkle)
  * Add image command and args in deployment template (#6 thanks @tidalf)

1.0.0
  * Upgrade chart to newer base templates (https://github.com/halkeye/helm-chart-starter)
  * Upgrade ingress so it picks the right api version based on installed k8s version

0.2.0
  * Replacing configmap with secret, and allow existingSecretName
  * Upgrade to latest vouch (0.9.5)

