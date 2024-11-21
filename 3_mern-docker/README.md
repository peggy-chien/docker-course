# To run the project, run the following command:

```bash
docker compose up
```

It's going to run all the services one by one based on the `compose.yaml` file.
Since the `api` service depends on the `db` service, the `db` service will be started first.

However, this won't update the frontend/backend automatically when we make changes to the code.
To do that, we need to run the following command:

```bash
docker compose watch
```

This will automatically update the frontend/backend when we make changes to the code.