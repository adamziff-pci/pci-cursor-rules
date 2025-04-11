# PCI Cursor Rules

This repository contains a set of Cursor rules and prompt templates that can be used to enforce coding standards and expedite development across all of our projects. We will enhance this repository over time to include more rules and templates.

The guide below covers the basics of using Git submodules to install this shared `.cursor` directory across multiple repositories.

---

# Shared Cursor Configuration via Git Submodules

We use a **dedicated repository** to store the entire `.cursor` directory (containing both rules and prompt templates). Each client repository includes this shared repository as a **Git submodule**. This way, all repos point back to one source of truth.

## 1. Initial Setup (One-Time)

1. **Clone** your client repository (or open it if you already have it cloned).
2. **Add** the submodule:

   ```bash
   git submodule add https://github.com/adamziff-pci/pci-cursor-rules.git .cursor
   git commit -m "Add shared cursor configuration as a submodule"
   git push
   ```

3. **Initialize** and **update** submodules:

   ```bash
   git submodule update --init --recursive
   ```

Now your local `.cursor` folder is linked to the `pci-cursor-rules` repository.

## 2. Pulling Updates from the Shared Repo

Whenever the `pci-cursor-rules` repository is updated (e.g., new or modified rules, prompt templates):

```bash
# Navigate to your client repo root
cd path/to/your-client-repo

# Pull latest submodule changes
git submodule update --remote .cursor

# Commit the pointer update to your client repo
git add .cursor
git commit -m "Update submodule pointer to latest shared cursor configuration"
git push
```

## 3. Editing Configuration and Pushing Back

If you need to make changes to the shared configuration and push them upstream:

1. **Enter** the submodule directory and create a branch (optional):

   ```bash
   cd .cursor
   git checkout -b feature/update-configuration
   ```

2. **Edit** your configuration, then **commit** and **push**:

   ```bash
   # Make changes to files in .cursor
   git add .
   git commit -m "Update cursor configuration"
   git push origin feature/update-configuration
   ```

3. **Create a pull request** in the `pci-cursor-rules` repository (if desired), or merge it directly if you have permissions.

4. **Back in your client repo**, update to the new commit (once merged):

   ```bash
   cd ..  # return to client repo root
   git submodule update --remote .cursor
   git add .cursor
   git commit -m "Update submodule pointer to latest shared cursor configuration"
   git push
   ```

## 4. Cloning a Client Repo That Already Has a Submodule

When **cloning** a client repo that already contains the shared submodule:

```bash
git clone https://github.com/your-org/client-repo.git
cd client-repo
git submodule update --init --recursive
```

This ensures the `.cursor` folder is properly initialized.

---

**That's it!** With this approach, each client repo references the same set of Cursor configuration (rules and prompt templates). Updating the submodule "pointer" ensures everyone stays aligned on the latest configuration.
