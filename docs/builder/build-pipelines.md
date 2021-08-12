---
id: build-pipelines
title: Build Pipelines
---

Components are built using different build pipelines when running `bit build`, `bit snap`, and `bit tag`.

To get a list of all the tasks that will be running per pipeline on a specific component, run `bit build --list-tasks <id>`.
For example:

```
➜ bit build --list-tasks ui/button

Tasks List
id:    my-scope/ui/button@1.0.0
envId: my-scope/custom-env@0.0.1

Build Pipeline Tasks:
teambit.harmony/aspect:CoreExporter
teambit.compilation/compiler:TSCompiler
teambit.defender/tester:TestComponents
teambit.pkg/pkg:PreparePackages
teambit.pkg/pkg:PublishDryRun
teambit.preview/preview:GeneratePreview

Tag Pipeline Tasks:
teambit.harmony/application:build_ui_application
teambit.pkg/pkg:PackComponents
teambit.pkg/pkg:PublishComponents

Snap Pipeline Tasks:
teambit.pkg/pkg:PackComponents
```

## Build (the basic build pipeline)

Components can be built without committing changes using the `bit build` command. This is often used to test the build process.
`bit build` runs only the build's build pipeline which mainly includes:

- Generating the component's `package.json`
- Installing or symlinking the component's dependencies
- Compiling the component's code (optional)
- Testing the component (optional)
- Performing ['dry run'](https://docs.npmjs.com/cli/v6/commands/npm-publish#:~:text=%5B--dry-run%5D%20As,the%20specified%20registry.)
- Generating the component's visualization (mainly, docs and 'compositions')

### Extending the basic build pipeline

Use the below method in your own Env to extend Bit's default build pipeline:

```ts
getBuildPipe?: (tsconfig?: TsConfigSourceFile) => BuildTask[];
```

## Snap

`bit snap` executes the basic pipeline before it runs its own build pipeline. The snap build pipeline consists, mainly, of [packing](#) the component without publishing it (since it is a snap and not a release version).

### Extending the snap build pipeline

Use the below method in your own Env to extend Bit's default snap pipeline:

```ts
getSnapPipe?: (tsconfig?: TsConfigSourceFile) => BuildTask[];
```

## Tag

`bit tag` executes the basic pipeline before it runs its own build pipeline. The snap build pipeline consists, mainly, of [packing](#) the component and publishing it.

### Extending the tag build pipeline

Use the below method in your own Env to extend Bit's default tag pipeline:

```ts
getTagPipe?: (tsconfig?: TsConfigSourceFile) => BuildTask[];
```