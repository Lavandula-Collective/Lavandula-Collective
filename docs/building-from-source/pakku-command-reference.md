---
order: 4
title: Pakku Command Reference
---

Practical Pakku commands for working on Lavendre Collective modpacks, plus two project rules: where mods get pulled from, and what happens to untracked files on fetch.

## Adding Mods: Modrinth Only

:::quote 

\[!IMPORTANT\] Pull from Modrinth only, as much as possible. This keeps mod sourcing consistent and avoids conflicts between platforms.

:::

If a mod is CurseForge-only and can't be pulled this way, it has to be bundled manually:

1. Confirm the mod's license explicitly allows redistribution. If it doesn't (or says nothing about it), it cannot be bundled.

2. Download the mod file directly from CurseForge.

3. Place it in the correct `.pakku` overrides folder per [Directory Structure](./directory-structure):

   -  Client-only -> `.pakku/client-overrides/mods/`

   -  Shared -> `.pakku/overrides/mods/`

   -  Server-only -> `.pakku/server-overrides/mods/`

4. Note the source and license permission in your commit message.

---

## Common Commands

### Adding a project

```bash
pakku add sodium
```

Add multiple projects in one command:

```bash
pakku add sodium lithium fabric-api
```

You can also add by URL if the slug search doesn't resolve correctly:

```bash
pakku add https://modrinth.com/mod/sodium
```

For more complex or specific adding:

```bash
pakku add prj --mr <slug>
```

### Removing a project

```bash
pakku rm sodium
```

Remove multiple at once:

```bash
pakku rm sodium lithium
```

### Updating projects

**(NOT RECOMMENDED)** Update everything:

```bash
pakku update
```

Update a specific project:

```bash
pakku update sodium
```

### Fetching your dev environment

Normal fetch (deletes anything untracked, see warning below):

```bash
pakku fetch
```

Safe fetch that preserves untracked files in `.pakku/shelf` instead of deleting them:

```bash
pakku fetch shelf
```

### Syncing local changes back into the repo

After editing configs or files inside your instance, sync them back into your Pakku project files:

```bash
pakku sync
```

### Packaging / exporting

Export a distribution-ready package:

```bash
pakku export .mrpack/.zip
```

Pakku supports export profiles (`curseforge`, `modrinth`, `serverpack`).

For the full command reference, see the [official Pakku documentation](https://juraj-hrivnak.github.io/Pakku).

---

## `pakku fetch` and Unregistered Files

:::quote 

\[!IMPORTANT\] Running `pakku fetch` will **automatically delete, without warning,** any resource packs, shaders, or mods present in your instance that were not added through Pakku.

:::

This includes files you might assume are safe because they're "required," such as the Mizuno's 16 Craft JE and Mizuno's 16 Craft JE CIT resource packs referenced in [Building From Source](./_index). If those packs aren't tracked by Pakku, a plain `pakku fetch` will wipe them on the next run.

### Use `pakku fetch shelf` instead

```bash
pakku fetch shelf
```

Instead of deleting untracked files, this moves them into `.pakku/shelf`, where they're preserved rather than wiped. Copy them back into your instance's `resourcepacks`, `shaderpacks`, or `mods` folder as needed.

**When to use it:**

-  You've manually installed a resource pack or shader that isn't part of the modpack definition.

-  You're testing a CurseForge-only mod locally before deciding whether to bundle it.

-  You're unsure whether everything in your instance is currently tracked by Pakku.

When in doubt, shelf it first. A plain `pakku fetch` gives you no second chance to recover deleted files.