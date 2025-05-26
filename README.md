# ScapCore - Agnostic Starter Kit

A CMS-agnostic starter kit to build websites using Next.js 13 with the Pages Router, TypeScript, Storybook for component documentation, and Jest for unit testing.

The name “Scapcore” comes from the Latin *scapus* — the vertical shaft of a column, silent and strong, bearing the weight of the structure it supports. Like its namesake, Scapcore is designed to be the unseen backbone of any CMS-agnostic project: stable, elegant, and built to last.

## Features

- **Next.js 13** (Pages Router) - The React framework with hybrid static & server rendering
- **TypeScript** - Static type checking for better code quality
- **ESLint + Prettier** - Code linting and formatting
- **Jest + Testing Library** - Unit testing framework
- **Storybook** - Component documentation and development
- **Modular Design System** - React components styled with Tailwind, Radix UI, and CSS tokens for accessibility and full customization. See our [Design System Guidelines](./docs/design-system.md) for how we structure, style, and override UI components using tokens and Tailwind. For layout patterns, check out our [Grid & Stack System](./docs/grid-stack-system.md) documentation
- **Internationalization (i18n)** – Built-in support for localized UI using `next-i18next`, with auto-typed namespaces and server-side translations (`withSharedNamespaces`) for seamless SSR and hydration-safe components. See our [i18n documentation](./docs/i18n.md)
- **Husky** - Git hooks for code quality
- **Bundle Analyzer** - Interactive visual reports to inspect the weight and composition of client, server, and edge bundles (`npm run analyze`)


##  Getting Started

### 1. Clone the repository and install dependencies:

```bash
git clone https://github.com/veilfelix/scapcore.git
cd scapcore
npm install
```

### 2. Run the development server

```bash
npm run dev
```

Visit [http://localhost:3000](http://localhost:3000/) to see the application.


## Project Commands

Below is a list of useful commands to run, test, and validate the project during development and deployment.

### Development

|Command|Description|
|---|---|
|`npm run dev`|Launches the Next.js development server.|
|`npm run start`|Starts the production server (after build).|
|`npm run build`|Builds the production version of the app.|

### Storybook

|Command|Description|
|---|---|
|`npm run storybook`|Starts the Storybook UI at `localhost:6006`.|
|`npm run build-storybook`|Builds a static version of the Storybook UI.|

### Internationalization

|Command|Description|
|---|---|
|`node scripts/generate-default-namespaces.js`|Scans your `/public/locales` folders and updates the list of shared i18n namespaces (`defaultNamespaces` in `/utils/i18nNamespaces.generated.ts`) used in SSR (`withSharedNamespaces`). Helps ensure hydration-safe translations by keeping server-side and client-side namespaces in sync.|
| See [docs/i18n.md](./docs/i18n.md) for full details. |

### Code Quality

| Command | Description |
|--|--|
| `npm run lint` | Runs ESLint to check for code style and best practices. |
| `npm run lint:fix` | Automatically fixes fixable linting issues. |
| `npm run lint:use-client` | Ensures all client-side components are properly annotated with `'use client'`. See [docs/use-client.md](./docs/use-client.md) for full details. |
| `npm run format` | Formats all code using Prettier. |
| `npm run format:check` | Checks formatting without writing changes (CI-friendly). |
| `npm run typecheck` | Runs the TypeScript compiler in strict mode without emitting files. |
| `npm run check` | Runs `typecheck`, `lint`, `lint:use-client`, and `test` in one command. Ideal for CI and pre-commit hooks. |

### Testing

|Command|Description|
|---|---|
|`npm run test`|Runs all Jest unit tests.|
|`npm run test:watch`|Runs tests in watch mode.|
|`npm run test:coverage`|Generates a code coverage report.|

### Performance

|Command|Description|
|---|---|
|`npm run analyze`|Runs `next build` with bundle analyzer (@next/bundle-analyzer) enabled.|

### Image Placeholders

| Command | Description |
|--|--|
| `node scripts/generate-blur-placeholder.js <image-url>` | Generates a base64 `blurDataURL` from an image URL for use with the `Image` component. See [docs/blur-placeholder.md](./docs/blur-placeholder.md) for full details. |


## Project Structure

```
/
├── .husky/                                 # Git hooks (e.g., pre-commit hook to run lint/tests)
│   └── pre-commit                          # Executes lint + tests + namespace sync script before commit
├── .storybook/                             # Storybook configuration (used for component documentation/dev)
│   ├── main.ts                             # Entry point and plugin config
│   └── preview.ts                          # Global decorators and styling
├── public/                                 # Static files (served as-is)
│   ├── favicon.ico                         # Site favicon
│   └── locales/                            # Translation files by locale (e.g. /locales/en/common.json)
├── src/                                    # All source files live here after migration
│   ├── components/                     
│   │   └── a11y/                           # Accessibility component utilities
│   │   ├── composed/                       # Structural or multi-element components (Header, Footer, Layout, Seo)
│   │   │   ├── layout/                     # Page wrapper layout
│   │   │   │   └── header/                 # Site header with navigation
│   │   │   │   └── footer/                 # Site footer
│   │   │   ├── Dialog/                     # Dialog which can include any React element
│   │   │   │   ├── Dialog.tsx              # Dialog component
│   │   │   │   ├── Dialog.stories.tsx      # Dialog stories for Storybook
│   │   │   │   └── Dialog.test.tsx         # Dialog unit tests using Jest and @testing-library
│   │   │   └── ...
│   │   └── ui/                             # Design system primitives (themed + variant-based)
│   │       ├── button/                     # Clickable button with variants
│   │       │   ├── button.tsx              # Button component
│   │       │   ├── button.stories.tsx      # Button stories for Storybook
│   │       │   └── button.test.tsx         # Button unit tests using Jest and @testing-library
│   │       └── ...
|   ├── scripts/
│   │   ├── generate-default-namespaces.js  # CLI to detect and sync namespaces in /public/locales/
│   │   └── lint-use-client.js              # CLI to enforce 'use client' on layout-level i18n components
│   ├── hooks/                              # Custom React hooks
│   ├── lib/                                # Application logic or API fetchers
│   │   └── api/                            # Internal API utils
│   ├── pages/                              # Next.js route pages (automatically routed)
│   │   ├── _app.tsx                        # Global layout and providers
│   │   ├── _document.tsx                   # Custom HTML structure, <html lang="..."> etc.
│   │   ├── 404.tsx                         # Custom Not Found page
│   │   ├── 500.tsx                         # Custom Error page
│   │   ├── index.tsx                       # Homepage route (/)
│   │   └── api/hello.ts                    # Example Next.js API route
│   ├── styles/                             
│   │   └── globals.css                     # Tailwind base/reset + theme injection
│   ├── theme/                              # Design system tokens & variables
│   │   ├── index.css                       # CSS variables used by Tailwind theme
│   │   └── tokens.ts                       # JS-accessible tokens (colors, spacing, fonts)
│   └── utils/                              
│       ├── classNames.ts                   # Helper to combine conditional Tailwind classNames
│       ├── i18n.ts                         # i18n utilities (initTestI18n, withSharedNamespaces, defaultNamespaces array)
│       ├── i18nSSR.ts                         # i18n utilities for SSR only
│       └── getButtonClassNames.ts          # Returns Tailwind classes for Button + ButtonLink
├── jest.config.ts                          # Jest configuration
├── jest.setup.ts                           # Jest test setup file (e.g., mocks, extensions)
├── next.config.ts                          # Next.js global configuration
├── postcss.config.js                       # Tailwind + PostCSS plugin configuration
├── tailwind.config.js                      # Tailwind theme extensions (colors, spacing, fonts, tokens)
├── tsconfig.json                           # TypeScript compiler options
├── tsconfig.tsbuildinfo                    # TypeScript incremental build cache
├── package.json                            # Project scripts and dependencies
├── README.md                               # You’re reading it 😉
```

## Contributing

This project is publicly available for learning and reuse.

However, I am **not accepting pull requests or external contributions** at this time.  
If you'd like to use this project, feel free to fork it and adapt it to your own needs.


## License

This project is licensed under the [MIT License](./LICENSE).

You are free to use, copy, modify, and distribute this code in your own projects — even for commercial use — as long as you include the original license.