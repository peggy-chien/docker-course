# React + TypeScript + Vite

This template provides a minimal setup to get React working in Vite with HMR and some ESLint rules.

Currently, two official plugins are available:

- [@vitejs/plugin-react](https://github.com/vitejs/vite-plugin-react/blob/main/packages/plugin-react/README.md) uses [Babel](https://babeljs.io/) for Fast Refresh
- [@vitejs/plugin-react-swc](https://github.com/vitejs/vite-plugin-react-swc) uses [SWC](https://swc.rs/) for Fast Refresh

## Expanding the ESLint configuration

If you are developing a production application, we recommend updating the configuration to enable type aware lint rules:

- Configure the top-level `parserOptions` property like this:

```js
export default tseslint.config({
  languageOptions: {
    // other options...
    parserOptions: {
      project: ['./tsconfig.node.json', './tsconfig.app.json'],
      tsconfigRootDir: import.meta.dirname,
    },
  },
})
```

- Replace `tseslint.configs.recommended` to `tseslint.configs.recommendedTypeChecked` or `tseslint.configs.strictTypeChecked`
- Optionally add `...tseslint.configs.stylisticTypeChecked`
- Install [eslint-plugin-react](https://github.com/jsx-eslint/eslint-plugin-react) and update the config:

```js
// eslint.config.js
import react from 'eslint-plugin-react'

export default tseslint.config({
  // Set the react version
  settings: { react: { version: '18.3' } },
  plugins: {
    // Add the react plugin
    react,
  },
  rules: {
    // other rules...
    // Enable its recommended rules
    ...react.configs.recommended.rules,
    ...react.configs['jsx-runtime'].rules,
  },
})
```

# Docker

## In the `compose.yaml` file

We're using the `build` section to build the image.
The `context` property is the path to the directory containing the Dockerfile.
The `docker build` command will look for a Dockerfile in the current directory by default, but we can specify a different path using the `-f` flag.
The `ports` section is used to expose the port that the application listens on.
The `volumes` section is used to mount the volume to the container.

_Note: remember to add the `"dev": "vite --host"` script to the `package.json` file to expose the port for vite._

## To run the container

```bash
docker compose up
```

Add `sudo` if you get permission errors.

## Docker Compose Watch

Docker compose isn't optimal for developer experience.
e.g. Every time we make a change to the `package.json` file, we have to rerun the container.

Docker compose watch listens to our changes and rebuilds the container, rerunning our app, and so on.

```bash
docker compose up --watch
```

Docker compose does three main things:

1. Sync: moves our changes from the host machine to the container
2. Rebuild: starts with the creation of new container images, and then updates the services (benifitial when rolling out changes to applications)
3. Restart: restarts the container
