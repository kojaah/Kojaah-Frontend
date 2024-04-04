# KOJAAH FRONTEND

This is the frontend repository for Kojaah that will contain all the frontend applications for the platform.

## IN DEVELOPMENT

1. Buyer and seller web application

## BACKLOG

1. Admin web application with product and order management
2. Advertisement management for the platform

## GETTING STARTED

1. Make sure to install the most recent version of Node.js on your machine.
2. Run `npm install` in Kojaah-Frontend folder to install the dependencies.
3. This is a npm worskspace project thus each project in the `apps` and `libs` folder contains workspaaces that have their own respective package.json file with scripts that can be run by invoking `[script] -w [workspace name]`
   for example:

```bash
npm run start -w=koojah-main
```

If the `-w` flag is not specified, it will run the from the root package.json file in the workspace.

4. To install a library for a specific workspace please specific the `-w` flag and the workspace name

```bash
npm install [package-name] -w=koojah-main
```

5. The package actually uses turborepo for easier development, build, testing, and linting pipelines. You can look through the package.json scripts for a list of possible commands. Therefore after installation of all packages, any of the commands below can be ran.

## REQUIREMENTS

1. Each project in the `apps` folder might include a .env.example file that contains the environment variables for the specific project. Please make sure to create a .env file in that specific project folder that contains the environment variables that is needed to successfully run the project.

## COMMANDS

1. `npm build` - builds all apps and libraries
2. `npm run build:main` - builds only the kojaah-main app and it's dependencies
3. `npm run dev` - runs a development server for all apps
4. `npm run dev:main` - runs a development server for the kojaah-main app
5. `npm run lint` - lints all apps
6. `npm run type-check` - type checks all apps
7. `npm run clean` - runs clean script for all apps
8. `npm run format` - runs prettier for all apps

## What's inside?

This Turborepo includes the following packages/apps:

### Apps and Packages

- `kojaah-main`: a [Next.js](https://nextjs.org/) app for the main kojaah site
- `@kojaah/ui`: a stub React component library with [Tailwind CSS](https://tailwindcss.com/) shared by both `web` and `docs` applications
- `@kojaah/eslint-config`: `eslint` configurations (includes `eslint-config-next` and `eslint-config-prettier`)
- `@kojaah/typescript-config`: `tsconfig.json`s used throughout the monorepo

### Note about building libs/ui (for help with creating more UI component libraries)

This example is set up to produce compiled styles for `ui` components into the `dist` directory. The component `.tsx` files are consumed by the Next.js apps directly using `transpilePackages` in `next.config.js`. This was chosen for several reasons:

- Make sharing one `tailwind.config.js` to apps and packages as easy as possible.
- Make package compilation simple by only depending on the Next.js Compiler and `tailwindcss`.
- Ensure Tailwind classes do not overwrite each other. The `ui` package uses a `ui-` prefix for it's classes.
- Maintain clear package export boundaries.

Another option is to consume `packages/ui` directly from source without building. If using this option, you will need to update the `tailwind.config.js` in your apps to be aware of your package locations, so it can find all usages of the `tailwindcss` class names for CSS compilation.

For example, in [tailwind.config.js](packages/tailwind-config/tailwind.config.js):

```js
  content: [
    // app content
    `src/**/*.{js,ts,jsx,tsx}`,
    // include packages if not transpiling
    "../../packages/ui/*.{js,ts,jsx,tsx}",
  ],
```

If you choose this strategy, you can remove the `tailwindcss` and `autoprefixer` dependencies from the `ui` package.
