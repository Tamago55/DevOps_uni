# CI/CD Pipeline Explanation

This project provides an overview of the Continuous Integration and Continuous Deployment (CI/CD) pipeline. The pipeline is designed to automate testing, security scanning, building, and deployment processes.

This explanation primarily references the `.github/workflows/deploy-to-cloud-run.yaml` and `.github/workflows/pull-request-test.yaml` files.

## Run test suite on Pull Request

When a pull request is made to the `main` branch, this pipeline triggers a series of actions:

1. **Environment Setup**: Initializes the runner environment with Ubuntu and sets up Python 3.9.
2. **Dependency Installation**: Installs necessary dependencies from `requirements.txt` and `requirements-dev.txt`.
3. **Testing**: Executes pytest to run tests and generate a coverage report.
4. **Codecov**: Uploads the coverage report to Codecov for code quality tracking.
5. **Security Scanning**: 
   - Sets up Node.js environment.
   - Installs and runs Snyk to detect vulnerabilities in the code and dependencies.
6. **Containerization**:
   - Logs into GitHub Container Registry.
   - Builds a Docker image and pushes it to the registry tagged with the GitHub commit SHA.

## Deploy to Cloud Run

On pushing to the repository, this part of the pipeline handles deployment:

1. **Authentication**: Uses Google GitHub Actions to authenticate with Google Cloud using a specific service account.
2. **Deployment**:
   - Deploys the application to Google Cloud Run from source.
   - Sets environment variables as needed for the deployment.
3. **Verification**:
   - Uses the deployed service's URL to verify its operational status via a simple curl command.

This pipeline ensures that each pull request and push to the main branch is automatically tested, scanned for security issues, containerized, and deployed, facilitating a robust DevOps workflow.

