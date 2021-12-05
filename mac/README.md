1. Create project

```
$ docker compose run --rm --no-deps web mix phx.new sample
$ cd sample
$ cp ../{docker-compose.yml,Dockerfile} .
```

2. Fix `config/dev.exs`

```
config :sample, Sample.Repo,
  ...
  hostname: System.get_env("DB_HOST") || "localhost",

...

config :sample, SampleWeb.Endpoint,
  # Binding to loopback ipv4 address prevents access from other machines.
  # Change to `ip: {0, 0, 0, 0}` to allow access from other machines.
  http: [ip: {0, 0, 0, 0}, port: 4000],
```

3. Launch Docker

```
$ docker compose up -d
$ docker compose exec web mix setup
```
