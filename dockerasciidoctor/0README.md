**Docker-Asciidoctor Publishing Environment (WSL Edition)**

- Update: 2025-05-01

- Sources:
  
  - https://learn.microsoft.com/en-us/windows/wsl/
  
  - https://docs.docker.com/desktop/
  
  - https://github.com/asciidoctor/docker-asciidoctor



A minimal set of Bash scripts to launch a **Docker-based Asciidoctor** environment and manage related assets easily under **WSL**.



## 📋 Requirements

- ✅ WSL (ie, WSL2) installed and properly configured
- ✅ Docker Desktop installed and running
- ✅ A `_publishing` directory under your WSL home (`~/_publishing`)
- ✅ A `scripts` directory under your WSL home (`~/scripts`)
  
  - Place all provided Bash scripts into `~/scripts`



## 📂 Scripts Overview

### `gopublishing`

**Description:**

- Checks if the `~/_publishing` directory exists.

- Verifies Docker is installed and running.

- Changes to the `_publishing` directory and runs `rundockerasciidoctor`.

**Usage:**

```bash
~/scripts/gopublishing
```



### `rundockerasciidoctor`

**Description:**

- Launches a Docker container running Asciidoctor.

- Mounts:
  
  - Your `~/_publishing` folder into the container's `/documents`
  
  - Your `~/scripts` folder into the container's `/scripts`

- Makes your local publishing "path" and custom scripts available inside the container.

**Usage:**

```
~/scripts/rundockerasciidoctor
```



### `doinitrevealjs`

**Description:**

- Initializes a `reveal.js` presentation environment ==inside the container==

- Helps you prepare a publishing environment via the Asciidoctor toolchain.

**Options:**

- `--basic`: 
  - Creates a minimal structure with essential files only.
- `--full`:
  - Clones the full `reveal.js` GitHub repository.

**Usage:**

```
/scripts/doinitrevealjs
```



## 🛠 Typical Workflow

1. 🔥 Start Docker Desktop.

2. 🔥 Start a WSL terminal session.

3. 📁 Ensure your publishing environment is set up:

   ```
   mkdir -p ~/scripts
   # Place your gopublishing, rundockerasciidoctor, doinitrevealjs scripts here
   ```

   ```
   sudo ln -sf <your-content-path> ~/_publishing
   ```

4. 🚀 Launch your publishing Docker environment:

   ```
   ~/scripts/gopublishing
   ```

5. 🎤 (Optional) Initialize Reveal.js setup:

   ```
   /scripts/doinitrevealjs --basic
   # or
   /scripts/doinitrevealjs --full
   ```

   

## ⚡ Troubleshooting

- **Docker command not found:** Install Docker Desktop and enable WSL integration.

- **Docker daemon not running:** Start Docker Desktop manually before running scripts.

- **Missing _publishing link:** Create it using:

  ```
  sudo ln -sf <your-content-path> ~/_publishing
  ```

- **Scripts not found:** Ensure they are placed under `~/scripts` and are executable (`chmod +x ~/scripts/*`).



## 📜 License

MIT License (or customize as needed for your project).



