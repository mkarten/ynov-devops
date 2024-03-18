# Setting up Environment on GitLab for App Deployment

To facilitate the deployment process of your application via GitLab, follow these steps to configure the environment properly. This includes creating an SSH key pair and setting up necessary environment variables.

## 1. Create SSH Key Pair:

Generate an SSH key pair using the command:

```
ssh-keygen -t ed25519 -C "GitLab SSH key"
```

Follow the prompts to generate the key pair. This will create two files:
- `id_ed25519` (private key)
- `id_ed25519.pub` (public key)

## 2. Add SSH Public Key to Authorized Keys:

Copy the contents of the public key (`id_ed25519.pub`) and add it to the authorized keys on your distant server. This allows GitLab to authenticate with the server via SSH.

## 3. Configure Environment Variables:

In GitLab, navigate to your project and go to `Settings > CI/CD > Variables`. Add the following environment variables:

- **SSH_PRIVATE_KEY**: Paste the contents of your private SSH key (`id_ed25519`). Make sure to remove any line breaks.
- **SSH_USER**: Username to access the distant server via SSH.
- **VM_IPADDRESS**: IP address of the distant server where the application will be deployed.
- **DOCKER_HUB_USERNAME**: Your Docker Hub username.
- **DOCKER_HUB_ACCESS_TOKEN**: Docker Hub access token for authentication.

Ensure these variables are securely stored and accessible only to authorized users.

## 4. Configure GitLab CI Pipeline:

use the provided `.gitlab-ci.yml` file to configure the CI pipeline. This file contains the necessary stages and jobs to build, test, and deploy the application.

- **Build Stage**: This stage builds the Docker image of the application.

- **Push Stage**: This stage pushes the Docker image to Docker Hub.

- **Deploy Stage**: This stage deploys the application to the distant server.

## 5. Deployment Verification:

After the pipeline runs successfully, verify the deployment:
- Access the application via the IP address of your distant server.
- Check if the Docker image has been pushed to Docker Hub.


## Author
- [Luca Morgado](https://github.com/mkarten)
- [Romain Fromentin](