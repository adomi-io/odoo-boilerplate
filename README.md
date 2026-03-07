<p align="center">
  <a href="https://github.com/new?template_name=odoo-boilerplate&template_owner=adomi-io">
    <img
      src="https://img.shields.io/badge/Use%20this%20template-2ea44f?style=for-the-badge&logo=github&logoColor=white"
      alt="Use this template"
      width="400"
    />
  </a>
</p>

# Adomi - Odoo Boilerplate

Odoo is an open-source ERP platform that bundles common business apps (CRM, Sales, Inventory, Accounting, HR, Manufacturing, and more) into a single system.

This repository is a starter template for getting up and running with Odoo quickly, using a community-driven nightly build of 
Odoo's Github repository.

Clone it, add your custom addons, and you're ready to ship Odoo

> [!TIP]
> Upstream image source code
> 
> - [adomi-io/odoo](https://github.com/adomi-io/odoo)
 
> [!TIP]
> Example Downstream image
> 
> - [adomi-io/odoo-community-base](https://github.com/adomi-io/odoo-community-base)

# Highlights

- 🚀 **Fast local setup**: Docker Compose stack ready for development.
- 🧩 **Addons-first workflow**: Mount your project addons into the container with a predictable path.
- 🔧 **Config you can ship**: Keep Odoo config and environment values separated and portable.
- 🪝 **Hooks support**: A place for startup/install scripts that run when the container boots.
- 🧱 **Easy image extension**: Add Python deps, extra addons, or Enterprise without fighting Docker.

# Getting started

> [!WARNING]
> This project is made to run via Docker.
> If you’re on Windows or macOS, install Docker Desktop:
>
> **[Download Docker Desktop](https://www.docker.com/products/docker-desktop/)**

Use this template to create your own Odoo project. 

When you use this template, it will create you a GitHub repository with
a CI/CD workflow that will optionally build and deploy your Odoo image to ghcr.

Simply take a copy of this repo, upload your custom addons into the `addons` folder, and you're ready to go!


## Manual setup

## 1) Clone

```bash
git clone git@github.com:adomi-io/boilerplate-odoo.git
cd boilerplate-odoo
````

## 2) Configure environment

Copy the example `env.example` to `.env`:

```bash
cp .env.example .env
```

Then update values in `.env` as needed (db credentials, ports, etc).

## 3) Start with Docker Compose

```bash
docker compose up --build
```

Odoo should come up on the port defined in your compose/env (commonly `http://localhost:8069`).

## 4) Logs + shell access

```bash
docker compose logs -f
```

```bash
docker compose exec odoo /bin/bash
```

# Project layout

* `addons/`
  Your custom Odoo addons live here.

* `config/`
  Odoo config files you want to mount into the container.

* `hooks/`
  Startup/setup scripts (auto-install modules, bootstrap config, etc).

* `extra_addons/` (optional)
  Extra addons you want to bake into a downstream image or mount separately from `addons/`.

# Changing the base image
> [!TIP]
> Try our [odoo-community-base](https://github.com/adomi-io/odoo-community-base) base image
> which includes some helpful OCA packages and additional addons. Set the `ODOO_DOCKER_IMAGE` arg to:
> ```md
> ghcr.io/adomi-io/odoo-community-base:latest
> ```

This repo lets you use any base image you want. This lets you extend any part of our stack,
and quickly swap out the base image for your own image, or one of our pre-configured images.

This allows you to have a custom pre-built version of Odoo with all your custom addons which you can
quickly take a copy of, or to swap a user's underlying image to Enterprise quickly and easily. 

You can change the base image via a build arg in the `docker-compose.yml`, or by editing the `Dockerfile`.

## Dockerfile
If you would like to change the default base image for your project, after taking a copy of this template,
change the first line of the `Dockerfile` to your desired base image url:

```dockerfile
ARG ODOO_BASE_IMAGE=ghcr.io/adomi-io/odoo:19.0
```

## Build arg

You can override the build arg on a per-deployment basis. This is helpful if you wish to offer both a community and enterprise version of Odoo.
If you have a pre-configured image with Enterprise, you can override the base image in the `docker-compose.yml`

```yaml
services:
  app_odoo:
    build:
      context: .
      dockerfile: Dockerfile
      args:
        ODOO_BASE_IMAGE: ghcr.io/your-company/odoo-enterprise:latest
```

# Making your own base image

To make your own base image, simply take a copy of this repo, and add your custom addons to the `extra_addons` folder,
and push your code to GitHub. GitHub Actions will build and push your image to GitHub Container Registry. Copy the image URL
from the Packages tab, and use it as the base image.

See our [Odoo Community Base image](https://github.com/adomi-io/odoo-community-base) for an example

## Debugging

If you’re using the Adomi Odoo image as your runtime, you can also use it as a development environment.
See the main image repo for IDE and breakpoint setup patterns:

* **[adomi-io/odoo](https://github.com/adomi-io/odoo)**

# Adomi
Adomi is an Odoo partner and consulting company. We try to make developing Odoo apps and business
utilities as easy as possible. This boilerplate will get you started with Odoo quickly and allow you to run
your odoo instance anywhere.

Check out some of our other projects:
* **[adomi-io on GitHub](https://github.com/adomi-io)**