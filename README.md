# Vouch Helm Charts
<a href="https://github.com/jessebot/vouch-helm-chart/releases"><img src="https://img.shields.io/github/v/release/jessebot/vouch-helm-chart?style=plastic&labelColor=blue&color=green&logo=GitHub&logoColor=white"></a>

## Usage

[Helm](https://helm.sh) must be installed to use the charts. Please refer to Helm's [documentation](https://helm.sh/docs/) to get started.

Here's the basics of running this chart, however you'll want to update your values.yaml.

```console
helm repo add vouch https://jessebot.github.io/helm-charts/
helm repo update
helm install vouch/vouch vouch --values.yaml
```

Docs for the `values.yaml` can be found in in the chart [README](./charts/vouch/README.md).

## License
Chart documentation is available in [helm-charts licencse](./LICENSE).

## Status
This chart is actively maintained and kept up to date by @jessebot and renovatebot :)

### Contributing
We'd love to have you contribute! Please refer to our [contribution guidelines](./CONTRIBUTING.md) for details.
