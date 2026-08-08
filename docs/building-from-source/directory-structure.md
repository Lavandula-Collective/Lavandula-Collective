---
order: 2
title: Directory Structure
---

# Directory Structure

The `.pakku` directory contains files managed by Pakku when building and distributing the modpack. Each subdirectory serves a different purpose depending on where its contents should be installed.

```text
.pakku
├── client-overrides
│   ├── config/
│   ├── defaultoptions/
│   └── fancymenu/
├── overrides
│   └── mods/
└── server-overrides
    └── mods/
```

## `client-overrides/`

Contains files that are installed **only on client instances**. This includes client-only configurations, menus, resource pack settings, and other files that should never be present on a dedicated server.

Example contents:

-  `config/`

-  `defaultoptions/`

-  `fancymenu/`

-  Client-only mods

-  Resource pack settings

## `overrides/`

Contains files that are installed on **both the client and dedicated servers**.

Use this for anything shared between both environments, such as:

-  Shared configuration files

-  KubeJS scripts

-  Datapacks

-  Server-compatible mods

-  Other common assets

## `server-overrides/`

Contains files that are installed **only on dedicated servers**.

Typical contents include:

-  Server-only configuration

-  Server-only mods

-  Startup scripts

-  Other dedicated server files

---

**Next:** [Client Configuration](./client-configuration-structure) -- a closer look at `client-overrides/config/` and where mod configs belong.