## Prerequisites

Before you begin, ensure that the following tools are installed on your system:

1. **Docker**: To build and run containers. Install Docker from [docker.com](https://www.docker.com/get-started).
2. **Docker Compose**: To manage multi-container Docker applications. Install Docker Compose from [docs.docker.com/compose](https://docs.docker.com/compose/install/).
3. **Git**: For version control. Install Git from [git-scm.com](https://git-scm.com/).
4. **Node.js & npm**: To manage your Vue.js project dependencies. Install from [nodejs.org](https://nodejs.org/).

## Install Instructions

1. **Clone the repository**:

```sh
git clone https://github.com/yourusername/vue-app-template.git
cd vue-app-template
```
   
2. **Install project dependencies**:

Inside the project directory, install the necessary npm packages:

   ```sh
   npm install
   ```
If the npm install fails, ensure that your package.json file contains the proper dependencies. You can also remove the node_modules directory and try again:

   ```sh
   rm -rf node_modules
   npm install
   ```

## Docker Build Instructions (for Multiple Architectures)

This template supports building Docker images for **x86_64** (amd64) and **ARM64** architectures.

### Step-by-Step Build Process

1. **Ensure Docker Buildx is Enabled**:

   Docker Buildx allows you to build multi-platform images. First, enable it if it's not already enabled:

   ```sh
   docker buildx create --use
   ```

2. **Build the Image for Multiple Architectures**:

   Use the following command to build and push the Docker image for both `x86_64` (amd64) and `ARM64` (aarch64) platforms:

   ```sh
   docker buildx build --platform linux/amd64,linux/arm64 -t yourusername/vue-app-template:latest --push .
   ```
- --platform linux/amd64,linux/arm64: Specifies the target architectures.
- --push: Automatically pushes the image to Docker Hub after building.
- -t yourusername/vue-app-template:latest: Tags the image with your Docker Hub username and the image name.

3. **Verify the Multi-Architecture Image**:

   After the build and push, verify that your image is available for both platforms:

   ```sh
   docker manifest inspect yourusername/vue-app-template:latest
   ```

   This will show you the image manifest, including the supported architectures.

## Running the Image on Your Server

1. **Pull the Image on Your Server**:

   After pushing the image, you can pull it to your server. Docker will automatically select the right image based on the architecture of the machine:

   ```sh
   docker pull yourusername/vue-app-template:latest
   ```

2. **Run the Image**:

   Once the image is pulled, you can run it on your server using the following command:

   ```sh
   docker run -d -p 80:80 yourusername/vue-app-template:latest
   ```
   This will start the container in detached mode and map port 80 inside the container to port 80 on the host, allowing you to access the app via the server's IP or domain.

## Commit Message Standard

This project follows the **Conventional Commit** standard for commit messages. The format is as follows:

**Commit Message Format:**

```sh
<action>(<scope>): <message>
```

- **`action`**: The type of change being made:
    - `chore`: Initial commits, maintenance tasks, or other minor changes.
    - `feat`: A new feature or functionality.
    - `style`: Changes related to formatting (whitespace, code style, etc.).
    - `refactor`: Changes to improve code without adding new features or fixing bugs.

- **`scope`** (optional): The part of the project that is affected, e.g., `build`, `docker`, `vue`, etc.
- **`message`**: A short description of the change.

### Examples:

- `feat(docker): add multi-platform build support`
- `chore(docs): update README with build instructions`
- `style(vue): fix indentation issues`
