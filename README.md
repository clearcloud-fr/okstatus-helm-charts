# OKStatus Helm charts

```sh
helm repo add okstatus https://charts.okstatus.eu
helm repo update
helm search repo okstatus
```

| Chart | Description |
|---|---|
| [`private-agent`](charts/private-agent) | OKStatus private monitoring agent — runs in your cluster, monitors your private services, outbound HTTPS only. |

## private-agent quick start

```sh
helm install okstatus-agent okstatus/private-agent \
  --set credentials.agentId=<id> --set credentials.agentSecret=<secret> \
  --set name=k8s-private-agent
```

Get the id/secret from **Dashboard → Private Agents → Add agent**. See
[`charts/private-agent/values.yaml`](charts/private-agent/values.yaml) for
every option (existing Secret, egress proxy, resources, tolerations…).

Image: `ghcr.io/clearcloud-fr/okstatus-agent` — source and releases at
[Clearcloud-Fr/okstatus-agent](https://github.com/Clearcloud-Fr/okstatus-agent).

## Publishing

Charts are released with [chart-releaser](https://github.com/helm/chart-releaser-action):
bump `version` in `Chart.yaml`, merge to `main`, and the `release` workflow
packages the chart, creates a GitHub release and updates `index.yaml` on the
`gh-pages` branch. `charts.okstatus.eu` is a CNAME to that GitHub Pages site
(`CNAME` file lives on `gh-pages`, see workflow).
