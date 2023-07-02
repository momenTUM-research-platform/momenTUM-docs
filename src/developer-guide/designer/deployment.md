# Deployment

The frontend of the project is developed using React and TypeScript. The source code for the frontend is located in the `frontend` folder. Notable libraries used in the frontend include:

- [TailwindCSS](https://tailwindcss.com) for styling using utility classes. Additionally, TailwindUI, which provides pre-made components, has been used (Please contact Manuel for information regarding the license).
- [ReactFlow](https://reactflow.dev/) for displaying the study graph.
- [ReactJsonSchemaForm](https://github.com/rjsf-team/react-jsonschema-form) for creating forms based on JSON schemas and validating their correctness.
- [Zustand](https://github.com/pmndrs/zustand) for state management. Zustand is responsible for storing all the data required for the study designer.

To build the frontend, you can run the following command in the `frontend` folder:

```shell
npm run build
```

However, it is recommended to use `pnpm` instead of `npm` for better performance and disk space optimization.

## Installing pnpm

To install `pnpm`, follow the steps below:

### Prerequisites

Before proceeding with the installation, ensure that you have the following prerequisites:

- Node.js and npm: `pnpm` requires Node.js and npm to be installed on your system. Make sure you have Node.js and npm installed and properly configured.

### Installation Process

To install `pnpm`, please follow these steps:

1. Open your terminal or command prompt.

2. Run the following command to install `pnpm` globally:

   ```shell
   npm install -g pnpm
   ```

   This command uses npm to install `pnpm` as a global package on your system.

3. After the installation is complete, verify that `pnpm` is installed correctly by running the following command:

   ```shell
   pnpm --version
   ```

   This command will display the version of `pnpm` installed on your system. If you see the version number, `pnpm` is installed successfully.

### Additional Recommendations

Consider the following recommendations to make the most out of `pnpm`:

- Use `pnpm` for your JavaScript projects by running `pnpm` commands instead of `npm` commands. For example, instead of using `npm install`, use `pnpm install` to install dependencies.

- If you have an existing project that uses npm, you can switch to `pnpm` by running `pnpm install` in the project's root directory. `pnpm` will use the existing `package.json` file and install the dependencies efficiently.

- Regularly update `pnpm` to the latest version by running `pnpm update -g pnpm`. This ensures that you have the latest features and bug fixes.

By following these steps and recommendations, you can successfully install and use `pnpm` as your preferred package manager for JavaScript projects. Enjoy faster installation times and optimized disk space usage with `pnpm`!

## Reproduction Steps

After installing the packages, run the build command.

To build the frontend, navigate to the `frontend` folder and execute the following command:

```shell
cd frontend && npm run build
```

or

```shell
cd frontend && pnpm build
```

The output will be available in the `frontend/dist` folder. When serving the application, the API serves this folder under the base route `/`, while API-specific requests are handled under `/api/v1/`.

In a production environment, the `preview` branch of the git repository is served under `/preview` to showcase features that are still under development.

## Developing Designer

To debug the application, change the environment variable to `development` by running the following command:

```shell
set NODE_ENV=development
```

Then, navigate to the frontend folder and install the dependencies. Use one of the following commands to launch the application:

```shell
npm run dev
```

or

```shell
pnpm dev
```