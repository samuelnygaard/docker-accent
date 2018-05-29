# docker-accent
There are instructions for deploying [accent](https://github.com/mirego/accent) on either a local OSX machine or heroku but there is no official docker setup. So here's a docker image for running Accent.

#### Environment
Check out the [official README](https://github.com/mirego/accent#environment-variables) for a list of environment variables used by Accent. The docker-compose example below shows an example configuration. I recommend you at least provide it
* `MIX_ENV`
* `PORT`
* `WEBAPP_PORT`
* `DATABASE_URL`

Don't forget you will have to manually run `mix ecto.setup` when running this container for the first time!

#### Docker Compose
An example of how this repository can be used as part of a docker-compose setup

```
version: "3.2"

services: 
  accent:
    build: ./accent
    links:
      - postgres
    ports:
      - 4000:4000
      - 4200:4200
    environment:
      MIX_ENV: dev
      PORT: 4000
      WEBAPP_PORT: 4200
      DATABASE_URL: postgres://postgres:password@postgres/accent_development

  postgres:
    image: postgres:10.4
    restart: always
    environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: password
    volumes:
      - postgresdata:/var/lib/postgresql/data

volumes:
  postgresdata:
    driver: local

``` 
