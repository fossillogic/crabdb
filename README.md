<p align="center">
    <img src=".github/logo.png" alt="Crab Tool Logo" width="620"/>
</p>

### A Command-Line Power Utility by **Fossil Logic**

**CrabCtl** is the official **Blue Crab Database CLI**, designed for DBAs, developers, and operations teams. Every change in Blue Crab is **versioned, branched, and mergeable**, providing fully traceable history, rollback, and auditability. FSON provides self-describing, schema-aware structures for both simple and complex data.

---

## Command Palette

### Core Database Operations

| **Command** | **Description** | **Common Flags** |
|-------------|-----------------|-----------------|
| `connect` | Connect to a Blue Crab instance. | `--host <host>` Database host<br>`--port <port>` Database port<br>`--user <username>` Login user<br>`--password <password>` Login password<br>`--ssl` Enable SSL |
| `shell` | Open an interactive shell. | `--type <myshell/noshell/cacheshell>` Select interface<br>`--db <dbname>` Connect to a specific database |
| `db` | Database management. | See sub-table below |
| `user` | Manage database users. | See sub-table below |
| `backup` | Backup and restore operations. | See sub-table below |
| `status` | Show database instance or shell status. | `--verbose` Detailed output<br>`--fson` FSON output |
| `metrics` | Show live performance metrics. | `--interval <s>` Refresh interval<br>`--fson` FSON output |
| `queries` | Inspect queries (MyShell only). | `--slow` Show slow queries<br>`--limit <n>` Number of queries |
| `connections` | Inspect active connections. | `--user <username>` Filter by user<br>`--db <dbname>` Filter by database |
| `cluster` | Cluster and node management. | See sub-table below |
| `help` | Display help. | `--examples` Usage examples<br>`--man` Full manual |

---

#### `db` Subcommands

| **Subcommand** | **Description** | **Common Flags** |
|----------------|-----------------|-----------------|
| `list` | List all databases. | `--fson` Output FSON |
| `create <dbname>` | Create a new database (git-chain backed). | `--template <template>` Use template<br>`--owner <user>` Assign owner |
| `drop <dbname>` | Delete a database. | `--force` Skip confirmation<br>`--cascade` Drop dependent objects |
| `open <dbname>` | Open database for operations. | `--branch <branch>` Open a specific branch |
| `close <dbname>` | Close database. | No flags |
| `branch <name>` | Create or switch branch. | `--from <branch>` Source branch |
| `merge <source> <target>` | Merge branch changes. | `--strategy <fast-forward/rebase/manual>` |
| `stats <dbname>` | Show database statistics. | `--verbose` Detailed info<br>`--fson` FSON output |

---

#### `user` Subcommands

| **Subcommand** | **Description** | **Common Flags** |
|----------------|-----------------|-----------------|
| `list` | List users. | `--fson` FSON output |
| `add <username>` | Add user with role. | `--role <role>` Assign role (admin, read, write)<br>`--password <password>` |
| `passwd <username>` | Change password. | `--password <password>` New password |
| `remove <username>` | Delete user. | `--force` Skip confirmation |

---

#### `backup` Subcommands

| **Subcommand** | **Description** | **Common Flags** |
|----------------|-----------------|-----------------|
| `create --db <dbname> --out <file>` | Backup database via git-chain commit. | `--compress` Compress backup<br>`--encrypt` Encrypt backup |
| `list` | List backups. | `--fson` FSON output |
| `restore --db <dbname> --in <file>` | Restore database from backup. | `--force` Overwrite<br>`--decrypt` Decrypt backup |

---

#### `cluster` Subcommands

| **Subcommand** | **Description** | **Common Flags** |
|----------------|-----------------|-----------------|
| `info` | Show cluster info. | `--fson` FSON output |
| `add-node <address>` | Add a node. | `--role <primary/replica>` |
| `remove-node <node-id>` | Remove a node. | `--force` Skip confirmation |
| `rebalance` | Rebalance data across nodes. | `--verbose` Detailed output |
| `status` | Show cluster health. | `--fson` FSON output |

---

### Global Flags (Available to All Commands)

| **Flag** | **Description** |
|-----------|-----------------|
| `--help` | Show help for command. |
| `--version` | Display CrabCtl version. |
| `-v, --verbose` | Enable detailed output. |
| `-q, --quiet` | Suppress output. |
| `--dry-run` | Simulate without changing data. |
| `--color` | Colorize output. |

---

### Usage Examples

| **Example** | **Description** |
|-------------|-----------------|
| `crabctl connect --host 127.0.0.1 --port 4429 --user admin` | Connect to a local instance. |
| `crabctl shell --type myshell --db warehouse` | Open MyShell for SQL-like queries. |
| `crabctl shell --type noshell --db warehouse` | Open NoShell for direct key-value operations. |
| `crabctl shell --type cacheshell --db cache` | Open CacheShell for in-memory cache operations. |
| `crabctl db create warehouse --owner admin` | Create a git-chain backed database. |
| `crabctl db branch feature-1 --from main` | Create and switch to a new branch. |
| `crabctl db merge feature-1 main --strategy fast-forward` | Merge a feature branch into main. |
| `crabctl user add analyst --role read --password secret` | Add a read-only user. |
| `crabctl backup create --db warehouse --out /backups/warehouse.bcdump` | Backup the database via git-chain. |
| `crabctl backup restore --db warehouse --in /backups/warehouse.bcdump --force` | Restore database from backup. |
| `crabctl cluster add-node 10.0.0.5 --role replica` | Add a new replica node. |
| `crabctl metrics --interval 5` | Display live metrics every 5 seconds. |
| `crabctl queries --slow --limit 10` | Show the top 10 slow queries (MyShell). |
| `crabctl connections --db warehouse` | List active connections to a database. |

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
    git clone https://github.com/fossillogic/crabctl.git
    cd crabctl
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
    crabctl
    ```

## **Contributing**

Interested in contributing? Please open pull requests or create issues on the [GitHub repository](https://github.com/fossillogic/crabctl).

## **Feedback and Support**

For issues, questions, or feedback, open an issue on the [GitHub repository](https://github.com/fossillogic/crabctl/issues).

## **License**

This project is licensed under the [Apache 2.0 License](LICENSE).
