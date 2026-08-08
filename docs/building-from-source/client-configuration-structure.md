---
order: 3
title: Client Configuration Structure
---

Most modpack configuration changes will be made inside `client-overrides/config/`.

```text
client-overrides/
└── config/
    ├── crash_assistant/
    ├── fancymenu/
    └── defaultoptions/
        ├── options.txt
        ├── keybindings.txt
        └── extra/
            └── config/
```

## `client-overrides/config/`

This directory contains **high-priority client configuration files**.

Everything inside this folder is copied directly into the instance's `config` directory **before Minecraft starts**, ensuring the configuration already exists when mods initialize.

Mods whose configuration must be available during startup belong here. Examples include:

-  Crash Assistant

-  FancyMenu

-  Any other mod that reads its configuration during initialization

This directory is also the preferred location for **large configuration files or folders** that would unnecessarily increase the size of the Default Options package.

## `client-overrides/config/defaultoptions/`

This directory is managed by the **Default Options** mod and stores the modpack's default Minecraft settings.

Typical contents include:

-  `options.txt`

-  `keybindings.txt`

These files define the default controls and game options shipped with the modpack.

### Updating Default Options

After changing keybinds or Minecraft options in-game, regenerate these files by running:

```mcfunction
/defaultoptions saveAll
```

This command saves your current options and keybindings back into the `defaultoptions` directory so they can be included in future releases.

## `client-overrides/config/defaultoptions/extra/`

The `extra` directory stores additional default files that should be copied into a fresh installation.

Unlike the rest of the `defaultoptions` directory, `extra` mirrors the structure of the Minecraft instance.

For example, this:

```text
defaultoptions/
└── extra/
    └── config/
        ├── mod_a.json
        └── mod_b.toml
```

becomes this once Default Options initializes:

```text
config/
├── mod_a.json
└── mod_b.toml
```

This behaves similarly to **YOSBR**--if the user doesn't already have these files, the mod automatically populates them using the versions bundled with the modpack.

:::quote 

\[!TIP\] Unless a configuration **must** exist before Minecraft finishes loading or is exceptionally large, it should be placed inside `client-overrides/config/defaultoptions/extra/config/`. This should be your default location when adding or updating a mod configuration.

:::

---

## Syncing Configuration Changes

When configuring mods, **always make your changes inside your development instance**, **not** inside the `.pakku` directory.

Once you're satisfied with the changes, copy the updated configuration files from your instance's `config` folder into the appropriate directory under `.pakku`:

{% table header="row" %}

---

*  {% colwidth=[390] %}

   From (your instance)

*  {% colwidth=[395] %}

   To (repository)

---

*  {% colwidth=[390] %}

   `config/modid/config.json`

*  {% colwidth=[395] %}

   `.pakku/client-overrides/config/modid/config.json` **or** `.pakku/client-overrides/config/defaultoptions/extra/config/modid/config.json`

{% /table %}

Which target path to use depends on where the configuration belongs -- see [Choosing the Correct Directory](./directory-structure#directory-structure) below.

:::quote 

\[!IMPORTANT\] Files inside `.pakku` are the versions that will be packaged and distributed with the modpack. Changes made only inside your development instance will **not** be included in future releases unless they are copied back into `.pakku`.

:::

---

## Choosing the Correct Directory

When adding or updating a mod configuration:

**Use** `**client-overrides/config/**` **if...**

-  the mod requires its configuration during startup;

-  the configuration must already exist before Minecraft loads;

-  the configuration consists of large files or entire folders (such as FancyMenu);

-  or the mod specifically expects its configuration before Default Options runs.

**Use** `**client-overrides/config/defaultoptions/extra/config/**` **if...**

-  the configuration is simply the default configuration for new users;

-  the mod does not require the configuration during startup;

-  you're updating a normal config file for inclusion in the modpack;

-  or you're unsure where the configuration belongs.

:::quote 

\[!IMPORTANT\] **For most mods, the correct location is** `**client-overrides/config/defaultoptions/extra/config/**`**.** Only place files directly in `client-overrides/config/` when there is a specific reason they need to be available before the Default Options mod initializes or when the configuration is too large to reasonably include inside `extra/`.

:::

---

**Next:** [Pakku Command Reference](./pakku-command-reference)