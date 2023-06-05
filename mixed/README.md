1. Execute `make` if you are not `Docker Desktop for Mac` user

```
$ make
```

2. Create project

```
$ docker compose run --rm --no-deps web mix phx.new sample
$ cd sample
$ cp ../{docker-compose.override.yml,docker-compose.yml,Dockerfile,Makefile,.env} .
```

3. Fix `config/dev.exs` and `config/test.exs`

Fix `config/dev.exs` and `config/test.exs`

```
config :sample, Sample.Repo,
  ...
  hostname: System.get_env("DB_HOST") || "localhost",
```

Fix `config/dev.exs`

```
config :sample, SampleWeb.Endpoint,
  # Binding to loopback ipv4 address prevents access from other machines.
  # Change to `ip: {0, 0, 0, 0}` to allow access from other machines.
  http: [ip: {0, 0, 0, 0}, port: 4000],
```

4. Launch Docker

```
$ docker compose up -d
$ docker compose exec web mix setup
```

You can access following url and develop Phoenix application!
http://localhost:4000/
