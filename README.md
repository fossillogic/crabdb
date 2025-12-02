<p align="center">
    <img src=".github/logo.png" alt="Blue Crab Database" width="620"/>
</p>

### A Database Power Utility by **Fossil Logic**

**crabd** is a modern command-line management utility for Blue Crab databases.  
It unifies initialization, storage control, backups, process management, logging, and deep introspection into one efficient CLI—ideal for developers, operators, and production administrators.

---

# Features

- Full lifecycle management (`start`, `stop`, `restart`, `status`)
- Snapshot backups with compression and encryption
- Storage diagnostics, expansion, repair, and compaction
- Process and worker management (`process`, `kill`)
- Real-time log inspection and filtering
- Schema, cache, index, and query introspection
- Metadata bootstrap and environment initialization
- FSON output for automation and pipelines

---

# Command Palette

---

## Core Database Commands

| **Command** | **Description** | **Flags** |
|-------------|-----------------|-----------|
| `init` | Initialize a new Blue Crab database environment. | `--path <dir>` Target directory<br>`--force` Overwrite metadata<br>`--config <file>` Use config<br>`--mode <dev\|prod>` Initialization mode |
| `backup` | Create a snapshot backup. | `--output <file>` Backup path<br>`--compress` Compress backup<br>`--encrypt` Encrypt output<br>`--include-logs` Include logs<br>`--consistent` Consistent snapshot |
| `storage` | Inspect or modify database storage. | `--info` Storage stats<br>`--expand <size>` Add capacity<br>`--compact` Compact storage<br>`--check` Validate<br>`--repair` Attempt repair |
| `start` | Start the database instance. | `--foreground` Run in foreground<br>`--config <file>` Use config<br>`--no-journal` Disable journaling<br>`--bootstrap` Init missing components |
| `stop` | Gracefully stop the database. | `--timeout <sec>` Shutdown timeout<br>`--force` Immediate termination<br>`--drain` Wait for queries |
| `restart` | Restart the instance. | `--timeout <sec>` Shutdown timeout<br>`--reload-config` Reload before restart<br>`--force` Hard restart |
| `status` | Show runtime status and metrics. | `--verbose` Extra details<br>`--fson` FSON output<br>`--threads` List internal threads<br>`--storage` Include storage metrics |
| `process` | List or inspect internal DB processes. | `--list` List processes<br>`--id <pid>` Show details<br>`--json` JSON output<br>`--stats` CPU/mem stats |
| `kill` | Terminate a stuck DB process or worker. | `--id <pid>` Process ID<br>`--force` Hard kill<br>`--signal <sig>` Send custom signal |
| `log` | View and filter logs. | `--level <trace\|debug\|info\|warn\|error>` Severity<br>`--tail <n>` Last N lines<br>`--follow` Stream logs<br>`--export <file>` Save logs<br>`--raw` Raw output |
| `introspect` | Inspect schemas, indexes, caches, and query plans. | `--schema` Schemas<br>`--indexes` Index info<br>`--cache` Cache details<br>`--query-plan <crabql>` Query plan<br>`--fson` FSON |
| `help` | Display help for commands. | `--command <name>` Command help<br>`--all` Full docs<br>`--examples` Usage examples |

---

## Global Flags

| **Flag** | **Description** |
|----------|-----------------|
| `--help` | Show help. |
| `--version` | Blue Crab version. |
| `-v, --verbose` | Verbose output. |
| `-q, --quiet` | Suppress output. |
| `--dry-run` | Simulate actions. |
| `--color` | Colorized output. |
| `--time` | Timestamped output. |

---

# Usage Examples

| **Example** | **Description** |
|-------------|-----------------|
| `crabd init --path db/ --mode=prod` | Initialize a production DB environment. |
| `crabd start --foreground --config=crab.conf` | Start with configuration in the foreground. |
| `crabd backup --output backup.crab --compress --encrypt` | Create compressed, encrypted backup. |
| `crabd storage --info` | Display storage usage and metadata. |
| `crabd storage --compact --check` | Compact and validate storage. |
| `crabd stop --drain --timeout 30` | Stop only after active queries finish. |
| `crabd log --follow --level=info` | Stream INFO-level logs. |
| `crabd kill --id 42 --signal TERM` | Gracefully terminate a process. |
| `crabd introspect --schema --indexes` | Inspect schemas and index structures. |
| `crabd status --fson` | Machine-readable status. |

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
