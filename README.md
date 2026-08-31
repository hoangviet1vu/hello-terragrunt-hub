# hello-terragrunt-hub

The hub repository for the **Helloworld Terragrunt** project — a reference implementation of a self-service infrastructure platform built with [Terragrunt](https://terragrunt.gruntwork.io/).

This repo ties the project together as a set of git submodules, and is the starting point for anyone exploring, running, or contributing to the project. It provides:

- A high-level overview of how the pieces fit together
- Pointers to each component repository (as git submodules)
- Shared/top-level documentation for the project

## Architecture

```
                    ┌───────────────────────────────┐
                    │  hello-terragrunt-backstage    │
                    │  Platform Provisioning UI      │
                    └───────────────┬─────────────────┘
                                    │ provisions via
                                    ▼
                    ┌───────────────────────────────┐
                    │      hello-terragrunt-live     │
                    │  Living Tenant Configuration   │
                    └───────────────┬─────────────────┘
                                    │ instantiates
                                    ▼
                    ┌───────────────────────────────┐
                    │    hello-terragrunt-modules    │
                    │   Terraform Module Definitions │
                    └───────────────────────────────┘
```

- **[hello-terragrunt-modules](https://github.com/hoangviet1vu/hello-terragrunt-modules)** defines the reusable Terraform modules — the building blocks for infrastructure.
- **[hello-terragrunt-live](https://github.com/hoangviet1vu/hello-terragrunt-live)** holds the live Terragrunt configuration per tenant/environment, wiring modules together with real inputs.
- **[hello-terragrunt-backstage](https://github.com/hoangviet1vu/hello-terragrunt-backstage)** is the self-service portal for platform provisioning, sitting on top of the live configuration.

## Repository structure

| Path | Submodule | Description |
|---|---|---|
| [`backstage/`](https://github.com/hoangviet1vu/hello-terragrunt-backstage) | `hello-terragrunt-backstage` | The Backstage instance for platform provisioning |
| [`modules/`](https://github.com/hoangviet1vu/hello-terragrunt-modules) | `hello-terragrunt-modules` | Terraform module definitions |
| [`live/`](https://github.com/hoangviet1vu/hello-terragrunt-live) | `hello-terragrunt-live` | Living tenant configuration managed by Terragrunt |

## Getting started

### Clone with submodules

```bash
git clone --recurse-submodules https://github.com/hoangviet1vu/hello-terragrunt-hub.git
```

If you already cloned without `--recurse-submodules`, fetch them with:

```bash
git submodule update --init --recursive
```

### Keeping submodules up to date

Pull the latest hub changes and sync submodules to the commits it references:

```bash
git pull
git submodule update --init --recursive
```

To pull the latest changes from each submodule's own default branch:

```bash
git submodule update --remote --merge
```

### Working inside a submodule

Each submodule is an independent repository — `cd` into it, make changes, and commit/push there as usual. Then come back to the hub, `git add <submodule-path>`, and commit to bump the pinned reference.

```bash
cd live
git checkout -b my-change
# ... make changes ...
git commit -am "..."
git push
cd ..
git add live
git commit -m "Bump live submodule"
```

## Documentation

Project-wide documentation and decisions that span multiple components live in this repo. Component-specific docs live in each submodule's own README.

## License

Licensed under the [Apache License 2.0](LICENSE).
