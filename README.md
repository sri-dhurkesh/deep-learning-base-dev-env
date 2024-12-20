## Deep Learning Base Development Environment

This repository contains a Dockerfile to set up a base development environment tailored for deep learning projects. It includes essential tools such as Python, Poetry, and Miniconda, with CUDA support for GPU-accelerated computation. This setup is optimized for flexibility and efficiency in development.

### Dockerfile Explanation

1. **Base Image:**
   The Docker image starts from `nvidia/cuda:12.1.0-devel-ubuntu20.04`, which includes the necessary CUDA toolkit for GPU-related tasks. This image does not come with Python pre-installed, so we manually install Python 3.8 to ensure compatibility with the development environment.

2. **Python Installation:**
   We update the package list and install essential utilities like `wget`, `curl`, `git`, and `python3`, followed by `python3-pip` for managing Python packages.

3. **Poetry Installation:**
   Poetry is used for Python dependency management and packaging. We install Poetry version 1.8.0 by fetching its installation script and adding its executable to the `PATH`.

4. **Miniconda Installation:**
   To manage environments more efficiently, we install Miniconda, a lightweight version of Anaconda. It allows the creation of isolated environments using `conda` and is ideal for deep learning workflows. Miniconda is installed by downloading and running the installer script.

5. **TINI Installation:**
   To handle proper signal handling for the container, we install TINI, a tiny init system, which ensures that the container shuts down gracefully.

6. **Conda Environment Integration with Poetry:**
   We configure Poetry to use a `conda` environment for virtual environments rather than Poetry’s default virtual environment system. This is achieved by setting the `CONDA_ENV_PATH` to `/opt/conda/envs/` and disabling Poetry’s internal virtualenv creation.

### Key Features:
- **CUDA Toolkit:** Enables GPU-accelerated computing for deep learning.
- **Python 3.8**: Installed for compatibility with deep learning libraries.
- **Poetry**: For efficient Python package management.
- **Miniconda**: A lightweight package manager for managing isolated environments.
- **TINI**: Ensures graceful shutdown of the container.
- **Conda Environment Integration**: Uses `conda` environments for virtual environments, managed by Poetry.

### Setup Instructions (If Not Using a Development Container)::

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/deep-learning-base-dev-env.git
   cd deep-learning-base-dev-env
   ```

2. Build the Docker image:
   ```bash
   docker build -t deep-learning-dev-env .
   ```

3. Run the Docker container:
   ```bash
   docker run -it deep-learning-dev-env bash
   ```

4. Verify Poetry Installation:
   ```bash
   poetry --version
   ```

5. Configure Conda environment (if needed):
   Poetry is already configured to use `conda` for environment management.


