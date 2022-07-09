# Rails app. to demonstrate [this issue](https://github.com/rails/importmap-rails/issues/137)

This app. runs in a docker compose environment created via this [rails from scratch](https://github.com/digitalronin/rails-from-scratch) project.

To launch the app, run: `make up`

# Usage without `make`

## 1. Build the application

```
docker compose --file .dockerdev/compose.yml --project-name Foobar-application down --volumes
docker compose --file .dockerdev/compose.yml --project-name Foobar-application build rails
docker compose --file .dockerdev/compose.yml --project-name Foobar-application up -d postgres
docker compose --file .dockerdev/compose.yml --project-name Foobar-application run --no-deps --rm rails /bin/bash -c bin/setup
docker compose --file .dockerdev/compose.yml --project-name Foobar-application run --no-deps --rm rails yarn
```

## 2. Start the application

After running step 1:

```
docker compose --file .dockerdev/compose.yml --project-name Foobar-application up
```

At this point, you should be able to view the application at `http://localhost:3000`

## 3. Stop the appplication

You can just Ctrl-C in the terminal where the appplication is running, or run this in a separate terminal window (after changing to the project directory):

```
docker compose --file .dockerdev/compose.yml --project-name Foobar-application down
```

## 4. Remove docker volumes

The application creates several docker volumes (for postgres & redis data, node_modules, etc). To remove all of these when you no longer need the application, run this:

```
docker compose --file .dockerdev/compose.yml --project-name Foobar-application down --volumes
```
