# Basilisp Example Getting Started Library

[Basilisp](https://github.com/basilisp-lang/basilisp) is a Lisp implementation broadly compatible with Clojure, running on the Python VM. Refer to the [documentation](https://basilisp.readthedocs.io/en/latest/index.html) to get started.

## Overview

This repository provides a Basilisp Example (`basilex`) Python project to get you started developing a Basilisp library (`basilib`) that can be easily referenced in your local Python Virtual Environments. It uses [setuptools](https://setuptools.pypa.io/en/latest/userguide/) to manage dependencies, eliminating the need for additional build tools.

## Prerequisites

- Python >= 3.9.

## Project Anatomy

The project is structured as follows

```
.
├── basilisp.edn   (B)
├── pyproject.toml (1)
├── setup.cfg      (2)
├── basilib        (N)
│   └── core.lpy   (3)
```

🄑 An empty file indicating to Clojure-enabled editors that this is a Basilisp Project.

🄝 The project's namespace.

① The configuration file where the `build-system` is specified, in our case it is `setuptools`.

② The configuration file where we specify dependencies for `setuptools`.

③ The core Basilisp Clojure code for the `basilib` library.

## Setup

To use this library, clone this repository and install the library in a local Python Virtual Environment.

### Create a Virtual Environment

To start from scratch, create a new virtual environment in `<venv path>` using the following command

```shell
$ python -m venv <venv path>
```

### Activate Environment and Install Basilib

Activate your virtual environment and install the `basilib` library from `<path to basilisp repo>` in editable mode (`pip -e`). This ensures updates to the project are immediately reflected in the virtual environment. 

Typically, when the environment is active, the `<venv>` prefix appears in your shell prompt.

```shell
$ source <venv path>/bin/activate
#   or if you are on MS-Windows: <venv path>\Scripts\Activate.ps1

(<venv>) $ pip install -e <path to basilex-basilib repo>
```

## Start Developing

The following instructions assume you are working within an activated Virtual Environment where `basilex-basilib` is installed, as described in the setup above.

To activate a virtual environment located at <venv path>, use the following command:

```shell
$ source <venv path>/bin/activate
# or if you are on MS-Windows
> <venv path>\Scripts\Activate.ps1
```
### Using the REPL

Run `basilisp repl`

```clojure
(<venv>) $ basilisp repl
basilisp.user=> (require '[basilib.core :as bc])
nil
basilisp.user=> (bc/hello)
:hi
```

### From your Clojure-Enabled Editor via the nREPL Server

Start the nREPL server to connect from a Clojure-enabled editor

- Specify a fixed port with `--port`
```shell
(<venv>) $ basilisp nrepl-server --port 9999
nREPL server started on port 9999 on host 127.0.0.1 - nrepl://127.0.0.1:9999
```

- Use a random available port
```shell
(<venv>) $ basilisp nrepl-server
nREPL server started on port 50398 on host 127.0.0.1 - nrepl://127.0.0.1:50398
```

#### Connecting your Clojure-Enabled Editor

> [!NOTE]
> While it’s not necessary to open the project in your editor to connect to the nREPL server, doing so simplifies setup. 

Open the `basilisp.edn` file in the root of your `basilex-baslib` project to enable Clojure-specific features in your editor.

Then use your Editor's Clojure nREPL commands to connect to the server.

Both [Emacs/CIDER](https://docs.cider.mx/cider/platforms/basilisp.html) and [VSCode/Calva](https://calva.io/basilisp/) offer explicit support for Basilisp.

To connect

##### CIDER (Emacs)

1. Run `M-x cider-connect-clj`
2. Select `localhost`.
3. Enter the port number from the nREPL server output.

##### Calva (VSCode)

1. Press `Ctrl-Shift-P` to open the Command Palette.
2. Select `Calva: Connect to a Running REPL Server, not in your project`>`basilisp`.
3. Enter the port number from the nREPL server output.

### Automatic port discovery

Alternatively, to simplify connection, configure the nREPL server to create a `.nrepl-port` file next to `basilisp.edn`. Editors can detect this file and automatically connect using the port it specifies.

- Using `--port-filepath`

```shell
(<venv>) $ basilisp nrepl-server --port-filepath <path to basilisp.edn dir>/.nrepl-port
nREPL server started on port 62904 on host 127.0.0.1 - nrepl://127.0.0.1:62904
```

- Starting from the project directory

If you start the server in the directory containing basilisp.edn, the `.nrepl-port` file will be created there automatically:

```shell
(<venv>) $ basilisp nrepl-server
nREPL server started on port 50398 on host 127.0.0.1 - nrepl://127.0.0.1:50398
```

Editor Connections with `.nrepl-port`

- CIDER (Emacs)

1. Run `M-x cider-connect-clj`
2. Select `localhost`.
3. Select the `<project-dir>:<port number>` option.

- Calva (VSCode)
1. Press `Ctrl-Alt-P` to open the Command Palette.
2. Select `Calva: Connect to a Running REPL Server, in your project`>`basilisp`.
3. The editor will automatically find the port using `.nrepl-port`.

The Editor should now connect seamlessly to the nREPL server.


## Managing Library Dependencies

Library dependencies are specified in `setup.cfg`. For more details on configuring dependencies, refer to the [Dependencies Management in Setuptools](https://setuptools.pypa.io/en/latest/userguide/dependency_management.html) guide.

If you make any changes to the dependencies, you may need to reinstall the project in your virtual environment for the changes to take effect:

```shell
(<venv>) $ pip install -e <path to basilex-basilib repo>
```


