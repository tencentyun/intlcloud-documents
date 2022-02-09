
Aegis will report the data environment as `production`, and you can modify it through the `env` parameter.

```javascript
new Aegis({
  id: '',
  env: Aegis.environment.gray
})
```


Valid values of `Aegis.environment`:

```javascript
export enum Environment {
  production = 'production', // Production environment
  gray = 'gray', // Beta test environment
  pre = 'pre', // Prerelease environment
  daily = 'daily', // Daily release environment
  local = 'local', // Local environment
  test = 'test', // Test environment
  others = 'others' // Other environments
}
```

After you modify the `env` parameter, the data reported by Aegis will carry it to help you distinguish between the data from different environments. However, only data in the `production` environment can participate in the calculation of the project score.
