---
title: Set up your Environment
weight: 3

### FIXED, DO NOT MODIFY
layout: learningpathall
---

To follow this Learning Path, you will need to set up an environment to develop
with SME2 and download the code examples. This learning path assumes two
different ways of working, and you will need to select the one appropriate for
your machine:
- Case #1: Your machine has native SME2 support --- check the [list of devices
  with SME2 support](#devices-with-sme2-support).
- Case #2: Your machine does not have native SME2 support. This learning path
  supports this use case by enabling you to run code with SME2 instructions in
  an emulator in bare metal mode, i.e., the emulator runs the SME2 code
  *without* an operating system.

## Code examples

[Download the code examples](https://gitlab.arm.com/learning-code-examples/code-examples/-/archive/main/code-examples-main.tar.gz?path=learning-paths/cross-platform/multiplying-matrices-with-sme2) for this learning path, expand the archive, and change your current directory to:
``code-examples/learning-paths/cross-platform/multiplying-matrices-with-sme2`` :

```BASH
tar xfz code-examples-main-learning-paths-cross-platform-multiplying-matrices-with-sme2.tar.gz -s /code-examples-main-learning-paths-cross-platform-multiplying-matrices-with-sme2/code-examples/
cd code-examples/learning-paths/cross-platform/multiplying-matrices-with-sme2
```

The listing of the content of this directory should look like this:

```TXT
code-examples/learning-paths/cross-platform/multiplying-matrices-with-sme2/
├── .clang-format
├── .devcontainer/
│   └── devcontainer.json
├── .git/
├── .gitignore
├── Makefile
├── README.rst
├── docker/
│   ├── assets.source_me
│   ├── build-all-containers.sh
│   ├── build-my-container.sh
│   └── sme2-environment.docker
├── hello.c
├── main.c
├── matmul.h
├── matmul_asm.c
├── matmul_asm_impl.S
├── matmul_intr.c
├── matmul_vanilla.c
├── misc.c
├── misc.h
├── preprocess_l_asm.S
├── preprocess_vanilla.c
├── run-fvp.sh
└── sme2_check.c
```

It contains:
- The code examples that will be used throughout this learning path.
- A ``Makefile`` that builds the code examples.
- A shell script called ``run-fvp.sh`` that runs the FVP (used in the emulated
  SME2 case).
- A directory called ``docker`` that contains materials related to Docker, which
  are:
  - A script called ``assets.source_me`` that provides the FVP and compiler
    toolchain references.
  - A Docker recipe called ``sme2-environment.docker`` to build the container
    that you will use.
  - A shell script called ``build-my-container.sh`` that you can use if you want
    to build the Docker container. This is not essential; ready-made images are
    available for you.
  - A script called ``build-all-containers.sh`` that was used to create the
    image for you to download to provide multi-architecture support for both
    x86_64 and AArch64.
- A configuration script for VS Code to be able to use the container from the
  IDE called ``.devcontainer/devcontainer.json``.

{{% notice Note %}}
From this point in the Learning Path, all instructions assume that your current
directory is
``code-examples/learning-paths/cross-platform/multiplying-matrices-with-sme2``.
{{% /notice %}}

## Platforms with native SME2 support

If your machine has native support for SME2, then you only need to ensure that
you have a compiler with support for SME2 instructions.

A recent enough version of the compiler is required because SME2 is a recent
addition to the Arm instruction set. Compiler versions that are too old will
have incomplete or no SME2 support, leading to compilation errors or
non-functional code. You can use [Clang](https://www.llvm.org/) version 18 or
later, or [GCC](https://gcc.gnu.org/) version 14 or later. This Learning Path
uses ``clang``.

At the time of writing, the ``clang`` version shipped with macOS is ``17.0.0``,
which forces us to use the version from ``homebrew`` (which has version
``20.1.7``). Ensure the ``clang`` compiler you are using is recent enough with
``clang --version``:

{{< tabpane code=true >}}

  {{< tab header="Linux/Ubuntu" language="bash">}}
  sudo apt install clang
  {{< /tab >}}

  {{< tab header="macOS" language="bash">}}
  brew install clang
  {{< /tab >}}

{{< /tabpane >}}

You are now all set to start hacking with SME2!

## Platforms with emulated SME2 support

If your machine does not have SME2 support or if you want to run SME2 with an
emulator, you will need to install Docker. Docker containers provide
functionality to execute commands in an isolated environment, where you have all
the necessary tools you require without cluttering your machine. The containers
run independently, meaning they do not interfere with other containers on the
same machine or server.

This learning path provides a Docker image that has a compiler and [Arm's Fixed
Virtual Platform (FVP)
model](https://developer.arm.com/Tools%20and%20Software/Fixed%20Virtual%20Platforms)
for emulating code with SME2 instructions. The Docker image recipe is provided
(with the code examples) so you can study it and build it yourself. You could
also decide not to use the Docker image and follow the
``sme2-environment.docker`` Docker file instructions to install the tools on
your machine.

### Docker

{{% notice Note %}}
This Learning Path works without ``docker``, but the compiler and the FVP must
be available in your search path.
{{% /notice %}}

Start by checking that ``docker`` is installed on your machine by typing the
following command line in a terminal:

```BASH { output_lines="2" }
docker --version
Docker version 27.3.1, build ce12230
```

If the above command fails with a message similar to "``docker: command not
found``" then follow the steps from the [Docker Install
Guide](https://learn.arm.com/install-guides/docker/).

{{% notice Note %}}
You might need to log in again or restart your machine for the changes to take
effect.
{{% /notice %}}

Once you have confirmed that Docker is installed on your machine, you can check
that it is operating normally with the following:

```BASH { output_lines="2-27" }
docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
478afc919002: Pull complete
Digest: sha256:305243c734571da2d100c8c8b3c3167a098cab6049c9a5b066b6021a60fcb966
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker followed these steps:

1. The Docker client contacted the Docker daemon.

2. The Docker daemon pulled the "hello-world" image from the Docker Hub.

    (arm64v8)

3. The Docker daemon created a new container from that image which runs the

    executable that produces the output you are currently reading.

4. The Docker daemon streamed that output to the Docker client, which sent it

    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:

$ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:

https://hub.docker.com/

For more examples and ideas, visit:

https://docs.docker.com/get-started/
```

You can use Docker in the following ways:
- Directly from the command line. For example, when you are working from a
  terminal on your local machine.
- Within a containerized environment. Configure VS Code to execute all the
  commands inside a Docker container, allowing you to work seamlessly within the
  Docker environment.

### Working with Docker from a terminal

When a command is executed in the Docker container environment, you must prepend
it with instructions on the command line so that your shell executes it within
the container.

For example, to execute ``COMMAND ARGUMENTS`` in the SME2 Docker container, the
command line looks like this:

```BASH
docker run --rm -v "$PWD:/work" -w /work armswdev/sme2-learning-path:sme2-environment-v2 COMMAND ARGUMENTS
```

This invokes Docker, using the
``armswdev/sme2-learning-path:sme2-environment-v2`` container image, and mounts
the current working directory (the
``code-examples/learning-paths/cross-platform/multiplying-matrices-with-sme2``)
inside the container to ``/work``, then sets ``/work`` as the working directory
and runs ``COMMAND ARGUMENTS`` in this environment.

For example, to run ``make``, you need to enter:

```BASH
docker run --rm -v "$PWD:/work" -w /work armswdev/sme2-learning-path:sme2-environment-v2 make
```

### Working within the Docker container from the terminal

The above commands are long and error-prone, so you can instead choose to work
interactively within the terminal, which would save you from prepending the
``docker run ...`` magic before each command you want to execute. To work in
this mode, run Docker without any command (note the ``-it`` command line
argument to the Docker invocation):

```BASH
docker run --rm -it -v "$PWD:/work" -w /work armswdev/sme2-learning-path:sme2-environment-v2
```

You are now in the Docker container; you can execute all commands directly. For
example, the ``make`` command can now be simply invoked with:

```BASH
make
```

To exit the container, simply hit CTRL+D. Note that the container is not
persistent (it was invoked with ``--rm``), so each invocation will use a
container freshly built from the image. All the files reside outside the
container, so changes you make to them will be persistent.

### Working within the Docker container with VSCode

If you are using Visual Studio Code as your IDE, it can use the container as is.

Make sure you have the [Microsoft Dev Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) extension installed.

Then select the **Reopen in Container** menu entry as Figure 1 shows.

It automatically finds and uses ``.devcontainer/devcontainer.json``:

![example image alt-text#center](VSCode.png "Figure 1: Setting up the Docker Container.")

All your commands now run within the container, so there is no need to prepend
them with a Docker invocation, as VS Code handles all this seamlessly for you.

{{% notice Note %}}
For the rest of this Learning Path, shell commands include the full Docker
invocation so that users not using VS Code can copy the complete command line.
However, if you are using VS Code, you only need to use the `COMMAND ARGUMENTS`
part.
{{% /notice %}}

### Devices with SME2 support

By chip:

| Manufacturer | Chip   | Devices |
|--------------|--------|---------|
| Apple        | M4     | iPad Pro 11" & 13", iMac, Mac mini, MacBook Air 13" & 15"|
| Apple        | M4 Pro | Mac mini, MacBook Pro 14" & 16" |
| Apple        | M4 Max | MacBook Pro 14" & 16", Mac Studio |

By product:

| Manufacturer | Product family | Models |
|--------------|----------------|--------|
| Apple        | iPhone 16      | iPhone 16, iPhone 16 Plus, iPhone 16e, iPhone 16 Pro, iPhone 16 Pro Max |