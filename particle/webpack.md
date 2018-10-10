# Webpack

## Analyze your bundle

```bash
NODE_ENV=production npx webpack --config apps/pl/webpack.pl.js --profile --json > stats.json
npx webpack-bundle-analyzer stats.json
```



