# Inventory

## Folder structure

For the different environments, a directory is created containing a host file and groupvars. For
global default variables, files are placed in the root of the `inventory` directory. A symlink is
created in each environment groupvars directory.

```bash
inventory
├── README.md
├── global_default.yml
└── test
    ├── group_vars
    │   └── all
    │       ├── default.yml
    │       └── global_default.yml -> ../../../global_default.yml
    └── hosts
```

## Symlinks

This inventory uses **linux** symlinks to share global default variables over the different environments.
These simlinks have been create with `ln -s ../../../global_default.yml`.

### Symlinks on Windows

> **NOTE:** These are **linux** symlinks and do **not** work on a windows system. VSC will not show
> them in the file explorer.
> An `ls` using either git bash or wsl terminal will not show the files after checkout.

To see if there are symlinks committed to the repository in the inventory on a windows machine, you
can use the following command: `git ls-files -s ./inventory`. Any files with the `120000` file
permission are symlinks.

```bash
> git ls-files -s .inventory
100644 6de42c996d760637d48bb9f1f752d40cbf9a6854 0   inventory/README.md
100644 4de1313e28872d378ab935c136ddf49066822699 0   inventory/global_default.yml                    # symlink source
120000 1cfec40b16c22c8677ed9ba400f4145320324da5 0   inventory/prd/group_vars/all/global_default.yml # symlink file
100644 4ba166cb7edeb94dca5b8ae5c064b6e80f8f35ea 0   inventory/prd/hosts
120000 1cfec40b16c22c8677ed9ba400f4145320324da5 0   inventory/test/group_vars/all/global_default.yml
100644 4ba166cb7edeb94dca5b8ae5c064b6e80f8f35ea 0   inventory/test/hosts
```

### Create symlink on windows

To create a symlink on a windows system, you must use the Windows Subsistem Linux (`WSL`). This can
be done in 2 ways:

- option 1
  - check out repository to your windows file system
  - open repository in VSC
  - Open WSL terminal and create symlink with `ln -s ../../../global_default.yml`

> **NOTE:** Git will see the new symlink file but you cannot open it. You can however commit it.

- Option 2 (recommended)
  - Check out repository to your WSL file system
  - Open repository in VSC as a WSL workspace
    - Navigate to dir using terminal and open repo with `code .`
  - Create symlink with `ln -s ../../../global_default.yml`

> **NOTE:** In WSL you can view the symlink files and its content.
