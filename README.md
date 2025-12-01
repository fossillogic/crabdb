<p align="center">
    <img src=".github/logo.png" alt="Blue Crab Tool Logo" width="620"/>
</p>

# Blue Crab Command Tool  
### A Command-Line Utility for the Blue Crab Database Platform  
Built by Fossil Logic

The Blue Crab Command Tool is a unified CLI for building, managing, and inspecting Blue Crab databases across MyShell, NoShell, and CacheShell. It supports schema workflows, key-value operations, FSON modeling, caching, git-chain versioning, and deep record-level introspection. With a consistent flag system and streamlined command set, it replaces multiple standalone database tools with one coherent interface.

---

# Features

- Create, open, clone, and manage Blue Crab databases  
- Execute MyShell SQL-like queries with FSON integration  
- Perform NoShell key-value operations with git-chain commits  
- Manage CacheShell with TTL, eviction rules, and serialization  
- Full git-chain lifecycle: commit, branch, merge, diff, log, rollback  
- FSON schema creation, validation, and conversion  
- Searching, scanning, and pattern matching across keys and records  
- Monitoring of keys, commits, cache events, and DB health  
- Structured summaries, statistics, and content analysis  
- Cross-platform support (Linux, macOS, Windows)

---

# Command Table

| **Command** | **Category** | **Description** | **Common Flags** |
|-------------|--------------|-----------------|------------------|
| `init` | Core | Create a new Blue Crab database. | `--path <dir>`, `--schema <file>`, `--mode <myshell/noshell/cacheshell>` |
| `open` | Core | Open or attach to an existing database. | `--path <db>`, `--readonly` |
| `clone` | Core | Clone a database using git-chain history. | `--branch <name>`, `--depth <n>` |
| `drop` | Core | Delete a database. | `-f`, `--backup` |
| `backup` | Core | Create a database snapshot. | `--full`, `--diff`, `--output <file>` |
| `restore` | Core | Restore database from snapshot. | `--force`, `--preserve-time` |
| `schema` | Core | View, update, or validate schema. | `--show`, `--apply <file>`, `--validate` |
| `query` | MyShell | Execute SQL-like MyShell queries. | `--file <sql>`, `--limit <n>`, `--fson` |
| `plan` | MyShell | Show query execution plan. | `--verbose`, `--costs` |
| `explain` | MyShell | Explain MyShell query structure. | `--fson` |
| `get` | NoShell | Retrieve values by key. | `--fson`, `--raw` |
| `set` | NoShell | Insert or update key-value pairs. | `--ttl <sec>`, `--fson` |
| `delete` | NoShell | Remove keys. | `--pattern` |
| `keys` | NoShell | List keys. | `--prefix <pfx>`, `--limit <n>` |
| `scan` | NoShell | Sequentially scan keyspace. | `--start <key>`, `--fson` |
| `cache-get` | CacheShell | Retrieve cached value. | `--decode` |
| `cache-set` | CacheShell | Store cached value. | `--ttl <sec>`, `--fson` |
| `cache-clear` | CacheShell | Clear cache namespace. | `--all` |
| `cache-stats` | CacheShell | Display cache metrics. | `--fson` |
| `commit` | Git-Chain | Commit database changes. | `-m <msg>`, `--amend` |
| `log` | Git-Chain | Show commit history. | `--limit <n>`, `--fson` |
| `diff` | Git-Chain | Compare commits. | `--keys`, `--records` |
| `branch` | Git-Chain | Manage branches. | `--create <name>`, `--delete <name>` |
| `merge` | Git-Chain | Merge branches. | `--strategy <auto/git/fson>` |
| `rollback` | Git-Chain | Reset database to earlier commit. | `--hard` |
| `find` | Analysis | Search keys or records. | `--content <expr>`, `--prefix` |
| `inspect` | Analysis | Inspect record metadata. | `--fson`, `--schema` |
| `stats` | Analysis | Database statistics. | `--keys`, `--records` |
| `summary` | Analysis | Generate structured database summary. | `--keywords`, `--topics`, `--entropy` |
| `watch` | Monitoring | Monitor DB events. | `--events <list>`, `--interval <n>` |
| `profile` | Monitoring | Performance profiling. | `--queries`, `--kv` |
| `health` | Monitoring | Database consistency and health check. | `--repair` |

---

# Global Flags

| **Flag** | **Description** |
|---------|------------------|
| `--help` | Show help for any command. |
| `--version` | Display tool version. |
| `-v, --verbose` | Enable detailed output. |
| `-q, --quiet` | Suppress output. |
| `--dry-run` | Simulate actions without changes. |
| `--color` | Colorize output. |
| `--time` | Include timestamps in output. |

---

# Usage Examples

| **Example** | **Description** |
|--------------|-----------------|
| `crab init --path db/ --schema schema.fson --mode=myshell` | Create a new database. |
| `crab query --file setup.sql` | Run a MyShell SQL-like script. |
| `crab set user:123 --fson '{name:"Ada"}'` | Insert an FSON record. |
| `crab keys --prefix user:` | List all user keys. |
| `crab commit -m "Seed initial data"` | Commit changes to git-chain. |
| `crab diff --records HEAD~1 HEAD` | Compare two commit histories. |
| `crab cache-set session:42 --ttl 3600` | Store a session in cache. |
| `crab watch --events=commit,key` | Monitor live database activity. |
| `crab summary --keywords --stats` | Generate high-level summary. |
| `crab rollback --hard HEAD~2` | Restore to earlier commit. |

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
    git clone https://github.com/fossillogic/app-c.git
    cd app-c
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
    <exe name>
    ```

## **Contributing**

Interested in contributing? Please open pull requests or create issues on the [GitHub repository](https://github.com/fossillogic/app-c).

## **Feedback and Support**

For issues, questions, or feedback, open an issue on the [GitHub repository](https://github.com/fossillogic/app-c/issues).

## **License**

This project is licensed under the [Apache 2.0 License](LICENSE).
