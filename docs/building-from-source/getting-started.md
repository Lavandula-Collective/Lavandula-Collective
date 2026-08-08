---
order: 1
title: Getting Started
---

:::quote 

\[!IMPORTANT\] This repository is intended for development and contributions only. Please read the [license](./../license) before redistributing or publishing modified versions of a Lavendre Collective modpack.

:::

## Requirements

Before you begin, install the following requirements:

-  [Temurin® JDK 21](https://adoptium.net/temurin/releases/?version=21)

-  [Git](https://git-scm.com/downloads)

-  [Pakku](https://juraj-hrivnak.github.io/Pakku/installing-pakku.html)

-  [Modrinth](https://modrinth.com/app)

-  [IntelliJ IDEA](https://www.jetbrains.com/idea/) (recommended)

Optional:

<details>

<summary>

**Installing** `**wget**`

</summary>

`wget` is only required if you want to download the required resource packs from the command line. Otherwise, you can download them through the in-game prompt.

### Windows

Using **Winget** (recommended):

```powershell
winget install GNU.Wget2
```

Or, if you use **Scoop**:

```powershell
scoop install wget
```

### macOS

Using **Homebrew**:

```sh
brew install wget
```

### Linux

**Debian / Ubuntu**

```sh
sudo apt install wget
```

**Fedora**

```sh
sudo dnf install wget
```

**Arch Linux**

```sh
sudo pacman -S wget
```

</details>

## Prepare the Modrinth Instance

This is where your local clone will live. You can use another launcher if you prefer, but Modrinth is recommended.

1. Create a new **Custom** instance in Modrinth.

   -  **Name:** `[PAKKU] Lavendre` (or anything you like)

   -  **Mod Loader:** Fabric

   -  **Minecraft Version:** 1\.21.1

   -  **Loader Version:** 0\.19.3

2. Open the instance folder.

3. Delete everything inside the instance folder.



## Clone the Repository

Clone the repository directly into the empty instance folder.

```bash
git clone https://github.com/aerhazu/Lavendre.git .
```

:::quote 

\[!NOTE\] The trailing `.` clones the repository into the current folder instead of creating a new `Lavendre` folder.

:::



## Switch to a Version Branch

:::quote 

\[!IMPORTANT\] **Do not use the master branch for development.** The master branch is reserved for documentation, assets, and other repository files. Always switch to a version branch you want to work on (for example, 1.0.0) before continuing.

:::

To see all available branches:

```bash
git branch -r
```

Then switch to the version you want to work on:

```bash
git switch 1.0.0
```

Replace 1.0.0 with the appropriate development branch if you're working on a different version.



## Initialize Pakku

Before fetching the modpack, copy the contents of:

```text
.pakku/client-overrides/config
```

into the root `config` folder of your instance.

After that, download all managed files (mods, resource packs, shaders, etc.):

```bash
pakku fetch
```

:::quote 

\[!TIP\] See [Pakku Command Reference](./pakku-command-reference) for what `pakku fetch` does, including a warning about files it can delete.

:::



## (Optional) Install Required Resource Packs

If you installed `wget` earlier, you can automatically download the required Mizuno's resource packs:

```bash
wget -O "resourcepacks/Mizunos 16 Craft JE_1.20.4-1.0_230105.zip" "https://raw.githubusercontent.com/aerhazu/CIT-Repository/main/minecraft/ResourcePack/Mizunos%2016%20Craft%20JE_1.20.4-1.0_230105.zip"
wget -O "resourcepacks/Mizunos 16 Craft JE CIT_1.21.1-1.1_170726.zip" "https://raw.githubusercontent.com/aerhazu/CIT-Repository/main/minecraft/CITs/Mizunos%2016%20Craft%20JE%20CIT_1.21.1-1.1_170726.zip"
```

If you don't have `wget`, don't worry--you can download both packs from the in-game prompt the first time you launch the instance.



## Launch the Game

Start the Modrinth instance as usual. If this is your first launch, Minecraft will generate any remaining configuration files and prompt you to download any missing optional resource packs.

---

## In This Section

-  [**Directory Structure**](./directory-structure) -- how the `.pakku` folder is organized

-  [**Client Configuration**](./client-configuration-structure) -- client config structure and where mod configs belong

-  [**Pakku Command Reference**](./pakku-command-reference) -- commands, mod source rules, and fetch safety