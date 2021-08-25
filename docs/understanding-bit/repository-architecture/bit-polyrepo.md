---
title: Bit in a Polyrepo (Multi-repo)
id: bit-polyrepo
---

import multiRepoPng from './bit-multi-repo.png';
import multiRepoDivergedPng from './bit-multi-repo-diverged.png';
import wsVisibility from './ws-visibility.png';
import scopeGraph from './scope-graph.png';
import discovery from './discovery.png';

Bit enables teams to work in a Polyrepo architecture but still get all the benefits of using a Monorepo and even more.

Example org on Github: https://github.com/bit-demos
Example org on Bit.dev: https://bit.dev/learn-bit-react

Acting repositories:

- [Base UI](https://github.com/bit-demos/base-ui)
- [ecommerce](https://github.com/bit-demos/ecommerce)
- [Perfume store](https://github.com/bit-demos/perfume-store)
- [Sports store](https://github.com/bit-demos/sports-store)
- [Shoe store](https://github.com/bit-demos/shoe-store)
- [Electronics store](https://github.com/bit-demos/shoe-store)

<img src={multiRepoPng} />

Directory structure for a each repo:

```bash
├── base-ui --> scope defining team boundaries and ownership
    ├── ui --> namespace to assist with organization and configuration of components
        ├── button --> component directory
          ├── index.ts
          ├── button.ts
          ├── button.spec.ts
          ├── button.docs.md
          ├── ...
    ├── hooks
        ├── use-product
          ├── index.ts
          ├── use-product.ts
          ├── button.spec.ts
          ├── button.docs.md
          ├── ...
├── ecommerce
    ├── ui
        ├── button
          ├── index.ts
          ├── button.ts
          ├── button.spec.ts
          ├── button.docs.md
          ├── ...
├── ...
```

This is the graph of [Scopes](scope/overview) helping understand how teams owning different responsibilities depend and collaborate with each other.

<img src={scopeGraph} />

### Simple, decoupled codebases
Each team is maintaining a simple, decoupled codebase which includes the team's source code alone. Each codebase is a Bit [Workspace](workspace/overview) which allows access to permitted [Scopes](scope/overview) for either API usage or for making and proposing changes.

An example for a single decoupled codebase is: https://github.com/bit-demos/ecommerce.
This codebase is owned by the ecommerce team which might maintain different kind of APIs in the form of [UI components](https://bit.dev/learn-bit-react/ecommerce/ui/store-hero), [micro-services](/), [applications](https://bit.dev/learn-bit-react/shoe-store/apps/shoe-store), [modules](https://bit.dev/learn-bit-react/ecommerce/entity/product) and even Markdown [content](https://bit.dev/learn-bit-react/ecommerce/content/about). Or anything else.

Having a small codebase highly improves dev experience, dev performance and makes it easy for devs to onboard.

### API and source code accessibility
Components can be installed for consumption in the [node_modules](packages/node-modules) directory.

```bash
bit install
```

Component source code can also be [imported](scope/importing-components) into the [Workspace](workspace/overview) for collaboration and change proposal on Components owned by other teams, live in other repos.

```bash
bit import
```

### Diverge to more repos and scale over time
As a single codebase gets bigger, it be easily distributed and delegated to more teams taking responsibility over specific features and components.

<img src={multiRepoDivergedPng} />

### Easy developer on-boarding

Smaller codebases, means a faster ramp up and on-boarding to new developers. They have less code to get to know. Easy way to find the code they need and more confidence making changes. 

### Code sharing and reuse
Code sharing and reuse is native across all repositories using Bit. Every component is made accessible through the [Scope](scope/overview) for either API usage through an installation or by [Importing](scope/importing-components) the [Component](components/overview) into your [Workspace](/workspace/overview).

Components are versioned independently with a [Semantic Version](https://semver.org) to help developer communicate per [Component](components/overview) API changes. 

```bash
bit tag --all
```

Components can annotated as [Internal/Private](/) using the internal namespace in the [Component ID](/components/id). Internal components won't be discoverable for others.

### Update automation

### Visibility and Discoverability
Developers gets visibility and discoverability to every Component in either the Workspace they are working on or [Components](/) from other [Scope](scope/overview) regardless to the repo it is hosted on.

<img src={wsVisibility} />

Using the [Bit Cloud](https://bit.dev) components can be found across repositories and Scopes with smart filters and semantic search.

<img src={discovery} />

### Testing affection of component changes

```bash
bit status
```

```bash
bit test --change
```

```bash
bit tag --all
```


### Cross team collaboration

### Atomic changes
Atomic changes across repositories can be done with [Lanes](components/lanes). A Lane is like branch for tracking cross component and dependency changes. Lanes can be used across Bit Workspaces helping to drive large atomic changes across an organization even when distributed throughout

```bash
bit lane my-feature --create
```

After changes are tested and approved, they can be merged at once across all repositories in a single merge.

```bash
bit merge
```

:::note
Bit Cloud can be used to simulate and measure the effect of the changes on all Components using each of the used Components with [Ripple CI](https://bit.dev/ripple-ci).
:::

### Consistent and standard tooling
Component development and tooling can be standardized with [Envs](envs/overview).


### Gradual refactoring


### Large scale refactoring

### Feedback loop
Feedback loops get shorter.

### Team autonomy
Team autonomy is preserved

### Dev experience
