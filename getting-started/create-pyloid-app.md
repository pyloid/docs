# Create Pyloid App Guide

Pyloid allows you to easily start a new project through its own CLI tool, `create-pyloid-app`. This guide will show you how to create and run a new Pyloid application.

## Getting Started

To create a new Pyloid project, run the following command in your terminal:

{% tabs %}
{% tab title="npm" %}
```bash
npm create pyloid-app@latest
```
{% endtab %}

{% tab title="pnpm" %}
```bash
pnpm create pyloid-app@latest
```
{% endtab %}

{% tab title="yarn" %}
```bash
yarn create pyloid-app@latest
```
{% endtab %}

{% tab title="bun" %}
```bash
bun create pyloid-app@latest
```
{% endtab %}
{% endtabs %}

## Project Setup Process

### 1. Specify Project Path

Enter the path where you want to create your project. The default is `pyloid-app`.

```
Enter the path to create the project (default: pyloid-app):
```

### 2. Select a Package Manager

Choose a package manager for your project:

- npm
- pnpm
- yarn
- bun

### 3. Select a Framework

Choose a frontend framework:

- React
- Vue
- Svelte
- Next.js
- SvelteKit

### 4. Select a Language

Choose a development language:

- JavaScript
- TypeScript

## Running Your Project

After creating your project, you can start development with the following commands:

{% tabs %}
{% tab title="npm" %}
```bash
cd project-name
npm run setup
npm run dev
```
{% endtab %}

{% tab title="pnpm" %}
```bash
cd project-name
pnpm run setup
pnpm run dev
```
{% endtab %}

{% tab title="yarn" %}
```bash
cd project-name
yarn run setup
yarn run dev
```
{% endtab %}

{% tab title="bun" %}
```bash
cd project-name
bun run setup
bun run dev
```
{% endtab %}
{% endtabs %}

The `setup` command installs all necessary dependencies and initializes the project.
The `dev` command starts the development server and runs the application locally.

## Project Structure

Pyloid projects may have slightly different structures depending on the chosen framework and language, but generally include the following main directories and files:

- `src-pyloid/` - Pyloid backend-related files
- `src/` - Frontend source code
- `build_config.json` - Build configuration file
- `package.json` - Project dependencies and scripts

## Build Configuration

The `build_config.json` file in your project automatically sets the appropriate icon format according to the operating system:

- Windows: `.ico` format
- macOS: `.icns` format
- Linux: `.png` format

These settings can be manually adjusted as needed.
