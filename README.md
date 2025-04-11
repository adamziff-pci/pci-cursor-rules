# PCI Cursor Rules

This repository contains a set of Cursor rules that can be used to enforce coding standards across all of our projects. It also contains a set of prompt templates to expedite development with agentic AI systems. We will enhance this repository over time to include more rules and templates.

The guide below covers the basics of using Git submodules to install this shared `.cursor/rules` directory across multiple repositories.

---

# Shared Cursor Rules via Git Submodules

We use a **dedicated repository** (e.g. `shared-cursor-rules`) to store the `.cursor/rules` directory. Each client repository includes this shared repository as a **Git submodule**. This way, all repos point back to one source of truth.

## 1. Initial Setup (One-Time)

1. **Clone** your client repository (or open it if you already have it cloned).
2. **Add** the submodule:

   ```bash
   git submodule add https://github.com/adamziff-pci/pci-cursor-rules.git .cursor/rules
   git commit -m "Add shared cursor rules as a submodule"
   git push
   ```

3. **Initialize** and **update** submodules:

   ```bash
   git submodule update --init --recursive
   ```

Now your local `.cursor/rules` folder is linked to the `shared-cursor-rules` repository.

## 2. Pulling Updates from the Shared Repo

Whenever the `shared-cursor-rules` repository is updated (e.g., new or modified rules):

```bash
# Navigate to your client repo root
cd path/to/your-client-repo

# Pull latest submodule changes
git submodule update --remote .cursor/rules

# Commit the pointer update to your client repo
git add .cursor/rules
git commit -m "Update submodule pointer to latest shared cursor rules"
git push
```

## 3. Editing Rules and Pushing Back

If you need to make changes to the shared rules and push them upstream:

1. **Enter** the submodule directory and create a branch (optional):

   ```bash
   cd .cursor/rules
   git checkout -b feature/update-rules
   ```

2. **Edit** your rules, then **commit** and **push**:

   ```bash
   # Make changes to files in .cursor/rules
   git add .
   git commit -m "Update cursor rules"
   git push origin feature/update-rules
   ```

3. **Create a pull request** in the `shared-cursor-rules` repository (if desired), or merge it directly if you have permissions.

4. **Back in your client repo**, update to the new commit (once merged):

   ```bash
   cd ../..  # return to client repo root
   git submodule update --remote .cursor/rules
   git add .cursor/rules
   git commit -m "Update submodule pointer to latest shared cursor rules"
   git push
   ```

## 4. Cloning a Client Repo That Already Has a Submodule

When **cloning** a client repo that already contains the shared submodule:

```bash
git clone https://github.com/your-org/client-repo.git
cd client-repo
git submodule update --init --recursive
```

This ensures the `.cursor/rules` folder is properly initialized.

---

**That’s it!** With this approach, each client repo references the same set of Cursor rules. Updating the submodule “pointer” ensures everyone stays aligned on the latest rules.
