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

## To build the image

```bash
docker build -t react-docker .
```

## To run the container and map the port (`-p [host machine port]:[container port]`)

```bash
docker run -p 5173:5173 react-docker
```

We also need to add `"dev": "vite --host"` in `package.json` to expose the port for vite.

## To make Docker automatically build images when we update the code

We need to use to follow command to run the container:

```bash
docker run -p 5173:5173 -v $(pwd):/app -v /app/node_modules react-docker
```

- `-v $(pwd):/app` mounts the current directory to `/app` in the container
- `-v /app/node_modules` mounts the node_modules directory to `/app/node_modules` in the container

## To publish the image to Docker Hub

```bash
docker login
docker tag react-docker [your docker hub username]/react-docker
docker push [your docker hub username]/react-docker
```

## To automate the process above we can use **Docker Compose**

Docker Compose is a tool that allows us to define and manage multi-container Docker applications.
It uses a YAML file (`compose.yml`) to configure the application's services, networks, and volumes.

Docker provides a CLI that generates these files for us, it's called `Docker Init`.
By runnning `docker init`, it'll ask us for the details and generate the `compose.yml` file.

## Additional notes

- If you want to get rid of all the inactive containers, you can run `docker container prune`.
- If you want to delete one specific container, you can run `docker rm [container id or name]`.