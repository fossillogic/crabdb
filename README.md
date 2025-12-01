<p align="center">
    <img src=".github/logo.png" alt="Blue Crab Tool Logo" width="620"/>
</p>

# Blue Crab DB Tool  
### A Command-Line Database Utility by **Fossil Logic**

The **Blue Crab DB Tool** is a unified command-line interface for developing, administering, and managing **Blue Crab databases**. It consolidates the entire database lifecycle—creation, schema definition, key-value operations, queries, caching, versioning, branching, merging, snapshots, and introspection—into a coherent and predictable set of commands. Built atop Blue Crab’s git-chain commit model and schema-aware FSON type system, the tool provides transparent version history, fast atomic operations, and flexible workflows across MyShell, NoShell, and CacheShell paradigms. All global flags remain consistent across commands for clarity and portability.

---

## Features

- Create, initialize, clone, or drop Blue Crab databases
- Import, export, migrate, and bulk-load records
- Strong schema-aware operations using the FSON type system
- SQL-like structured querying via MyShell syntax
- Low-level, direct key-value manipulation via NoShell modes
- CacheShell integration for in-memory caching, TTL management, and cache flushing
- Commit history, branching, merging, diffing, and rollback powered by git-chain
- Database snapshots and structural integrity checks
- Live monitoring of database mutation events
- Deep introspection of keys, values, types, and commit ancestry

---

# Command Palette

## Core Database Management Commands

| **Command** | **Description** | **Common Flags** |
|-------------|-----------------|------------------|
| `init` | Create and initialize a new Blue Crab database. | `-f, --force` Overwrite existing directory<br>`--from <template>` Use a template |
| `open` | Open an existing database and verify integrity. | `--readonly` Disable writes<br>`--check` Validate structure |
| `drop` | Delete a Blue Crab database permanently. | `-f, --force` Skip confirmation<br>`--wipe` Secure-wipe |
| `clone` | Clone a Blue Crab database with full commit history. | `--shallow` Partial history<br>`--branch <name>` Select branch |
| `branch` | Create, list, or switch branches. | `-c, --create <name>` Create branch<br>`-s, --switch <name>` Switch branch |
| `merge` | Merge a branch into the current one. | `--no-ff` Disable fast-forward<br>`--resolve <strategy>` Conflict strategy |
| `commit` | Commit staged changes to the git-chain. | `-m <msg>` Commit message<br>`--amend` Amend last commit |
| `rollback` | Rewind the database to a previous commit. | `--to <hash>` Target commit<br>`--soft` Keep working data<br>`--hard` Replace working data |
| `schema` | Define or modify FSON schemas. | `-a, --apply <file>` Apply schema<br>`-v, --validate` Validate schema |
| `put` | Insert or update a key-value pair. | `--fson` Use FSON input<br>`--ttl <sec>` TTL for caches |
| `get` | Retrieve a key’s value. | `--raw` Raw output<br>`--fson` FSON output<br>`--meta` Include metadata |
| `delete` | Remove a key or keyset. | `-r, --recursive` Remove nested keys |
| `query` | Execute MyShell-style SQL-like queries. | `--plan` Show query plan<br>`--limit <n>` Limit rows |
| `kv` | Execute NoShell-style key-value operations. | `--batch <file>` Batch mode |
| `cache` | Manage CacheShell caching. | `--flush` Clear cache<br>`--ttl <sec>` Set global TTL |
| `export` | Export data or full database snapshots. | `-f, --format <type>` fson/json/bin<br>`--keys <set>` Key subset |
| `import` | Import or batch-load records. | `--merge` Merge keys<br>`--wipe` Clear before import |
| `snapshot` | Capture a complete database snapshot. | `--name <label>` Snapshot label |
| `diff` | Compare commits, branches, or snapshots. | `--keys` Key-level changes<br>`--fson` FSON output |
| `inspect` | Inspect keys, snapshots, or commits. | `--meta` Metadata<br>`--history` Show ancestry |
| `stats` | Generate database statistics. | `--keys` Key stats<br>`--storage` Storage metrics<br>`--fson` Structured output |
| `watch` | Monitor real-time database activity. | `-e, --events <list>` Event filters<br>`-t, --interval <n>` Poll interval |
| `repair` | Detect and fix database inconsistencies. | `--auto` Auto-repair |
| `help` | Display help for commands. | `--man` Manual |

---

## Global Flags (Available to All Commands)

| **Flag** | **Description** |
|-----------|-----------------|
| `--help` | Show command help. |
| `--version` | Display tool version. |
| `-v, --verbose` | Enable detailed output. |
| `-q, --quiet` | Suppress output. |
| `--dry-run` | Simulate without altering data. |
| `--color` | Enable colored output. |
| `--time` | Show timestamps in output. |

---

# Usage Examples

| **Example** | **Description** |
|-------------|-----------------|
| `crab init mydb/` | Create a new Blue Crab database. |
| `crab open --check project.db` | Open database and validate structure. |
| `crab put --fson user:1 "{name:cstr:'Alex', age:i32:30}"` | Insert a structured FSON record. |
| `crab get --fson --meta user:1` | Retrieve value and metadata in FSON format. |
| `crab query "SELECT name FROM users WHERE age > 20"` | Execute SQL-like query. |
| `crab branch -c dev` | Create a branch named `dev`. |
| `crab merge --resolve=ours dev` | Merge `dev` into the current branch. |
| `crab rollback --to 7fa92c1 --hard` | Hard rollback to a specific commit. |
| `crab snapshot --name before-import` | Create a labeled snapshot. |
| `crab diff main dev --keys` | Compare branches at key granularity. |
| `crab export -f fson --keys users > users.fson` | Export users as FSON. |
| `crab import --merge newdata.fson` | Import and merge new data. |
| `crab watch -e create,update` | Monitor creation and update events. |
| `crab stats --storage` | Show storage metrics. |
| `crab repair --auto` | Automatically fix errors. |

---

## **Prerequisites**

Ensure you have the following installed before starting:

- **Meson Build System**: This project relies on Meson. For installation instructions, visit the official [Meson website](https://mesonbuild.com/Getting-meson.html).

## **Setting Up Meson Build**

1. **Install Meson**:
    - Follow the installation guide on the [Meson website](https://mesonbuild.com/Getting-meson.html) for your operating system.

## **Setting Up, Compiling, Installing, and Running the Project**

1. **Clone the Repository**:

    ```sh
    git clone https://github.com/fossillogic/crabdb.git
    cd crabdb
    ```

2. **Configure the Build**:

    ```sh
    meson setup builddir
    ```

3. **Compile the Project**:

    ```sh
    meson compile -C builddir
    ```

4. **Install the Project**:

    ```sh
    meson install -C builddir
    ```

5. **Run the Project**:

    ```sh
    crab
    ```

## **Contributing**

Interested in contributing? Please open pull requests or create issues on the [GitHub repository](https://github.com/fossillogic/crabdb).

## **Feedback and Support**

For issues, questions, or feedback, open an issue on the [GitHub repository](https://github.com/fossillogic/crabdb/issues).

## **License**

This project is licensed under the [Apache 2.0 License](LICENSE).
