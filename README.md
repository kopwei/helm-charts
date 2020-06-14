# KOPWEI's Personal Helm Charts

This repo contains personal helm charts created by kopwei

## Upload charts after change

Here is the basic flow about how to refresh the chart index and release after changes has been merged to master branch. You need to have [chart-releaser](https://github.com/helm/chart-releaser) installed on your laptop and have chart-releaser's configuration ready.

```bash
helm package charts/{chart1, chart2} --destination .deploy 
cr upload

git checkout gh-pages

cr index -i ./index.yaml -c https://github.com/kopwei/helm-charts

git add index.yaml
git commit -m "Updated index.yaml"
git push
```
