# Vouch Helm Charts
<a href="https://github.com/jessebot/vouch-helm-chart/releases"><img src="https://img.shields.io/github/v/release/jessebot/vouch-helm-chart?style=plastic&labelColor=blue&color=green&logo=GitHub&logoColor=white"></a>

This is a fork of the official Vouch helm chart with some quality of life updates to match standard helm chart style. It's actively maintained and kept up to date by @jessebot and renovateBot, so if a new version of the Vouch docker image we'll automatically get a PR to update it :)

## Usage

Make sure you have helm installed. To get started with helm, read their [documentation](https://helm.sh/docs/).
Here's the basics of running this chart, however you'll want to update your [`values.yaml`](./charts/vouch/values.yaml).

```console
helm repo add vouch https://jessebot.github.io/helm-charts/
helm repo update
helm install vouch/vouch vouch --values.yaml
```

Docs for the [`values.yaml`](./charts/vouch/values.yaml) can be found in in the chart [README](./charts/vouch/README.md).

## License
Chart documentation is available in [helm-charts licencse](./LICENSE). We've kept it the same as the upstream chart.

### Contributing
We'd love to have you contribute! Please refer to our [contribution guidelines](./CONTRIBUTING.md) for details.
