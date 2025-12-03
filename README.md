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

# Core Database Commands

| **Command** | **Description** | **Flags** |
|-------------|-----------------|-----------|
| `init` | Initialize a new Blue Crab database environment. | `--path <dir>` Target directory<br>`--force` Overwrite metadata<br>`--config <file>` Use config<br>`--mode <dev\|prod>` Initialization mode |
| `start` | Start the Blue Crab database instance. | `--foreground` Run in foreground<br>`--config <file>` Use config<br>`--no-journal` Disable journaling<br>`--bootstrap` Initialize missing components |
| `stop` | Gracefully stop the database service. | `--timeout <sec>` Shutdown timeout<br>`--force` Immediate termination<br>`--drain` Wait for active queries |
| `restart` | Restart the running Blue Crab instance. | `--timeout <sec>` Shutdown timeout<br>`--reload-config` Reload before restart<br>`--force` Hard restart |
| `status` | Display runtime status, health, and metrics. | `--verbose` Extra details<br>`--json` JSON/FSON output<br>`--threads` List internal worker threads<br>`--storage` Include storage metrics |
| `process` | List or inspect internal worker processes/sessions. | `--list` List processes<br>`--id <pid>` Show process details<br>`--json` JSON output<br>`--stats` CPU/memory statistics |
| `kill` | Terminate a stuck worker or internal process. | `--id <pid>` Process ID<br>`--force` Hard kill<br>`--signal <sig>` Send custom signal |
| `log` | View, filter, and export logs. | `--level <trace\|debug\|info\|warn\|error>` Severity filter<br>`--tail <n>` Last N lines<br>`--follow` Stream logs<br>`--export <file>` Export logs<br>`--raw` Raw output |
| `introspect` | Inspect internal schemas, metadata, caches, and plans. | `--schema` Schema information<br>`--indexes` Index metadata<br>`--cache` Cache details<br>`--query-plan <crabql>` Explain/plan a CrabQL query<br>`--json` JSON/FSON output |
| `help` | Display command documentation. | `--command <name>` Help for a specific command<br>`--all` Full documentation<br>`--examples` Show command usage examples |

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
