## Deploy Discord Bot

This GitHub Actions workflow is designed to automatically deploy a Discord bot whenever changes are pushed to the `main` branch or manually triggered. It utilizes Docker and SSH to build and run the bot in a remote server environment.

### Workflow Steps

1. **Build & Push (push job)**: This step builds the Docker image for the Discord bot and pushes it to the target server.
   - It connects to the remote server using SSH.
   - It navigates to the project directory on the server and pulls the latest changes from the Git repository.
   - It builds the Docker image using `docker compose build`.

2. **Run (run job)**: This step starts the deployed Discord bot.
   - It connects to the remote server using SSH.
   - It navigates to the project directory on the server.
   - It starts the Docker containers using `docker compose up -d`, running the bot in detached mode.

### Environment Variables

The workflow uses the following environment variables:

- `REPO_NAME`: The name of the GitHub repository.
- `REPO_OWNER`: The owner of the GitHub repository.
- `USER`: The username on the remote server.

### Prerequisites

To set up and use this workflow, you need to ensure the following:

1. You have a remote server accessible via SSH, where the Discord bot will be deployed.
2. Docker and Docker Compose are installed on the remote server.
3. SSH private key and passphrase are set up as GitHub secrets. The private key should have access to the remote server.
4. In the repository settings, add the following secrets:
   - `SSH_HOST`: The hostname or IP address of the remote server.
   - `SSH_PRIVATE_KEY`: The SSH private key with access to the remote server.
   - `SSH_PASSPHRASE`: The passphrase for the SSH private key.
5. The `.github/workflows/deploy.yml` file with the workflow definition is present in the repository.

### Deployment Process

Whenever changes are pushed to the `main` branch or the workflow is manually triggered, the following deployment process will occur:

1. The workflow connects to the remote server via SSH.
2. It navigates to the project directory on the server and pulls the latest changes from the Git repository.
3. The Docker image for the Discord bot is built using `docker compose build`.
4. The deployed bot is started using `docker compose up -d`, running in detached mode.

This workflow simplifies the deployment process of your Discord bot, ensuring that it is always up to date on your remote server.
