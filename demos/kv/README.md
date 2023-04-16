# Persisting non-relational data with the Spin key/value store

This demo showcases how to use Spin's built-in key/value store to persist non-relational data in your applications, with minimal configuration.

## Prerequisites

- `spin templates install --git https://github.com/radu-matei/spin-kv-explorer --update`

## Talk Track

For every new request, Spin will create a new instance for the corresponding Wasm component, then shut it down — the downside of this is that state needs to be persisted somewhere else. This is where Spin's key/value store comes into play — Spin has a built-in and configurable key/value store, that is always available when you are running your application.

Let's look at an application that lets us explore the contents of Spin's default key/value store. After installing the template from the prerequisites section, you can create create an application (or add the component to an existing application) based on the explorer:

```bash
$ spin new kv-explorer
Enter a name for your new application: spin-kv-explorer
```

Exploring `spin.toml`, the only configuration required for this is adding the "default" key/value store:

```toml
# spin.toml
[[component]]
id = "kv-explorer"
key_value_stores = ["default"]
```

Next, we can start the application locally. Passing the environment variable `--env SPIN_APP_KV_SKIP_AUTH=1` will skip authentication when running the application locally:

```
$ spin up --env SPIN_APP_KV_SKIP_AUTH=1
Logging component stdio to ".spin/logs/"
Storing default key-value data to ".spin/sqlite_key_value.db"

Serving http://127.0.0.1:3000
Available Routes:
  kv-explorer: http://127.0.0.1:3000/internal/kv-explorer (wildcard)
```

Accessing the explorer lets you list, view, delete, and create key/value pairs. Note that you can store any binary data as values.

Fermyon Cloud has a key/value store that is available with no extra configuration — you can deploy your application using `spin deploy`, and you can set initial values for key/value pairs using the `--key-value` flag — in this case, setting the credentials for the explorer:

```
$ export KV_CREDENTIALS="user:some-password"
$ spin deploy --key-value kv-credentials=$KV_CREDENTIALS
Uploading spin-kv-explorer version 0.1.0+r2083595e...
Deploying...
Waiting for application to become ready...... ready
Available Routes:
  kv-explorer: https://spin-kv-explorer-xxxxx.fermyon.app/internal/kv-explorer (wildcard)
```

What if you want to provide your own database for persistence? When running Spin locally, you can configure the backing implementation for the default store — for example, using a Redis instance:

```toml
# runtime-config.toml
[key_value_store.default]
type = "redis"
url = "rediss://xxxxxx"
```

Start the Spin application using the runtime configuration file from above:

```bash
$ spin up --env SPIN_APP_KV_SKIP_AUTH=1 --runtime-config-file runtime-config.toml
```

## Key Takeaways

* Spin offers a built-in key/value store that lets you store non-relational data with minimal configuration
* You can deploy your application to Fermyon Cloud with no changes and you will have a default store available for your applications
* You can configure your own Redis instance as the backing implementation for the key/value store, without changing or recompiling your application — only with a minimal configuration file
