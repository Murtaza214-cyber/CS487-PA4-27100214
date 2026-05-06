<div align="center">

# PA4 Submission: TaskFlow Pipeline

<img alt="GitHub only" src="https://img.shields.io/badge/Submit-GitHub%20URL%20Only-10b981?style=for-the-badge">
<img alt="Total points" src="https://img.shields.io/badge/Total-100%20points-7c3aed?style=for-the-badge">

</div>

<div style="background:#f5f3ff;color:#111827;border-left:6px solid #6330bc;padding:14px 18px;border-radius:10px;margin:18px 0;">
This document serves as the formal technical submission for Programming Assignment 4. All supporting evidence is maintained within the <code>docs/</code> directory and referenced via relative paths.
</div>

## Student Information

| Field | Value |
|---|---|
| Name | Syed Muhammad Murtaza Hassan |
| Roll Number | 27100214 |
| GitHub Repository URL | https://github.com/Murtaza214-cyber/CS487-PA4-27100214 |
| Resource Group | `rg-sp26-27100214` |
| Assigned Region | `ukwest` |

## Evidence Rules

- Relative image paths are implemented: `![Description](docs/image.png)`.
- Descriptions provide technical verification for each architectural component.
- Security protocols were followed; sensitive connection strings and keys have been masked.

---

## Task 1: App Service Web App (15 points)

### Evidence 1.1: Forked Repository

![Forked GitHub Repository](docs/github-fork.png)

Description: The screenshot verifies the successful creation of the project fork under the GitHub account "Murtaza214-cyber," serving as the foundational source control for the pipeline.

### Evidence 1.2: App Service Overview

![App Service Overview](docs/webapp-overview.png)

Description: The Azure Portal overview confirms that the Web App `pa4-27100214` is in a "Running" state within the designated `ukwest` region and `rg-sp26-27100214` resource group.

### Evidence 1.3: Deployment Center / GitHub Actions

![Deployment Center Configuration](docs/deployment-center.png)

Description: This evidence demonstrates the successful integration between GitHub Actions and the Azure App Service Deployment Center, ensuring automated builds from the `main` branch.

### Evidence 1.4: Live Web UI

![TaskFlow Dashboard](docs/live-ui.png)

Description: The dashboard interface is shown loaded in a web browser, confirming that the App Service is successfully hosting the frontend React application.

![App settings](app_settings)
---

## Task 2: Azure Container Registry (15 points)

### Evidence 2.1: ACR Overview

![ACR Overview](docs/acr-overview.png)

Description: The container registry `pa427100214` is verified as provisioned on the Basic SKU with a healthy provisioning state.

### Evidence 2.2: Docker Builds

![Validator API Build](docs/build-validate-api.png)
![Validator API Logs](docs/build-validate-api-logs.png)
![Report Job Build](docs/build-report-job.png)
![Report Job Logs](docs/build-report-job-logs.png)
![Function App Build](docs/build-func-app.png)
![Function App Logs](docs/build-func-app-logs.png)
![Local Validator Test](docs/local-validator-test.png)

Description: These logs and status indicators provide evidence of the successful local compilation and testing of the three Docker images: `validate-api`, `report-job`, and `func-app`.

### Evidence 2.3: ACR Repositories

![ACR Push Logs](docs/acr-push-validate.png)
![ACR Push Logs](docs/acr-push-report.png)
![ACR Push Logs](docs/acr-push-func.png)
![ACR Repository Table](docs/acr-repository-table.png)

Description: The CLI output confirms the successful push of all three container images to the registry, with the repository list displaying all required services.

---

## Task 3: Durable Function Implementation (12 points)

### Evidence 3.1: Completed Function Code
### Evidence 3.2: Local Function Handler Listing

![Portal Function List](docs/portal-functions-list.png)

Description: The Azure Portal displays the discovered function triggers, confirming the presence of the `http_starter`, `my_orchestrator`, and both activity handlers.

---

## Task 4: Function App Container Deployment (8 points)

### Evidence 4.1: Function App Container Configuration

![Function App Container Settings 1](docs/func-container-settings-1.png)
![Function App Container Settings 2](docs/func-container-settings-2.png)

Description: The Deployment Center settings confirm the Function App is configured to pull the authenticated `func-app:v1` image from the `pa427100214` registry.

### Evidence 4.2: Orchestration Smoke Test

![Orchestration Trigger](docs/smoke-test-curl.png)

Description: A manual `curl` request successfully triggers the orchestrator, returning the unique instance ID and the status query URI for tracking.

### Evidence 4.3: Expected Failed Status Before Downstream Wiring

![Status Query Failure](docs/expected-failure-json.png)

Description: The status JSON confirms an orchestration failure due to the expected absence of the `VALIDATE_URL` environment variable at this stage of deployment.

---

## Task 5: AKS Validator (15 points)

### Evidence 5.1: AKS Cluster

![AKS Cluster Status](docs/aks-get-nodes.png)

Description: The `kubectl get nodes` command confirms the AKS node pool is operational and the cluster context has been correctly merged into the local configuration.

### Evidence 5.2: Kubernetes Nodes and Pods

![Validator Pod Status](docs/aks-get-pods.png)

Description: The evidence shows the `validate-deployment` pod in a "Running" state, confirming that the container was successfully pulled and scheduled.

### Evidence 5.3: Kubernetes Service

![Kubernetes Service Details](docs/aks-get-service.png)

Description: The `validate-service` is formally exposed via a LoadBalancer, providing a persistent External-IP for the Durable Function activity.

### Evidence 5.4: Validator API Tests

![Health Check](docs/curl-health.png)
![Successful Validation](docs/curl-validate-valid.png)
![Rejected Validation](docs/curl-validate-invalid.png)

Description: The API demonstrates correct behavior by approving valid quantities and rejecting orders that exceed the defined threshold of 100 units.

### Evidence 5.5: Function App `VALIDATE_URL`

![Function App CLI Config](docs/az-function-config-cli.png)
![Function App Portal Settings](docs/portal-env-validate-url.png)

Description: The environment variable `VALIDATE_URL` has been successfully applied to the Function App, enabling connectivity to the AKS LoadBalancer.

### Evidence 5.6: AKS Idle Behavior

![AKS Node State](docs/aks-nodes-state.png)

Description: The cluster remains provisioned while idle, maintaining the node state to ensure consistent availability for the validation activity.

---

## Task 6: ACI Report Job (15 points)

### Evidence 6.1: Blob Container

![Blob Container Creation](docs/az-storage-container-create.png)

Description: The Azure CLI output confirms the successful creation of the `reports` container within the storage account.

### Evidence 6.2: Manual ACI Run

![Manual ACI Test State](docs/az-container-list-test.png)

Description: The `ci-report-test` instance reached a "Succeeded" state, verifying that the `report-job` image can execute successfully in a serverless environment.

### Evidence 6.3: ACI Logs

![Reporting Job Logs](docs/aci-logs-trace.png)

Description: The detailed logs confirm that the ACI container successfully authenticated with Managed Identity and completed the PDF generation process.

### Evidence 6.4: Generated PDF

![Storage Browser Reports](docs/storage-browser-reports.png)

Description: The storage browser confirms the presence of `TEST-001.pdf` and `ORD-001.pdf`, validating successful write operations to the blob container.

### Evidence 6.5: Function App Managed Identity and IAM

![Portal Identity View](docs/portal-identity-managed.png)

Description: The evidence displays the User Assigned Managed Identity associated with the Function App to facilitate secure resource management.

### Evidence 6.6: Report App Settings

![Report Environment Variables](docs/report-app-settings-portal.png)

Description: The configuration demonstrates that all required reporting and identity variables have been formally applied to the Function App.

---

## Task 7: End-to-End Pipeline (15 points)

### Evidence 7.1: Web App Wiring

![Web App Settings](docs/frontend-wiring-settings.png)

Description: The Web App is formally integrated with the backend by configuring the `FUNCTION_START_URL` and `FUNCTION_STATUS_URL` in its environment variables.

### Evidence 7.2: Happy Path UI

![UI Submission Form](docs/happy-path-ui-form.png)
![UI Running Status](docs/happy-path-ui-running.png)
![UI Completion Status](docs/happy-path-ui-completed.png)
![Generated PDF locally](docs/pdf-report-opened.png)

Description: The dashboard demonstrates a complete orchestration cycle, successfully processing a valid order and providing a functional PDF report link.

### Evidence 7.3: Backend Participation

![Log Stream Grep Trace](docs/backend-logs-chain.png)
![Validate Activity Trace](docs/validate-activity-trace.png)
![Report Activity Trace](docs/report-activity-trace.png)

Description: The filtered log stream provides a formal trace of the order ID as it is successfully validated by the AKS microservice and reported via ACI.

### Evidence 7.4: Reject Path UI

![Rejected Order Dashboard](docs/reject-path-ui.png)

Description: The frontend correctly communicates the rejection status when the validation activity identifies a quantity exceeding 100 units.

---

## Task 8: Write-up and Architecture Diagram (5 points)

### Evidence 8.1: Architecture Diagram

![System Architecture Diagram](docs/architecture-diagram.png)

Description: The diagram illustrates the service interdependencies across App Service, Durable Functions, AKS, ACI, and Blob Storage.

### Question 8.2: Service Selection

- **App Service**: Chosen for the React frontend to leverage managed platform features and seamless GitHub Actions integration.
- **Durable Functions**: Utilized to manage the complex, stateful orchestration required to chain separate cloud services.
- **AKS**: Selected to host the validator API as a dedicated, high-availability microservice.
- **ACI**: Optimal for the reporting job as a consumption-based, ephemeral container service that bills only during active execution.

### Question 8.3: ACI vs AKS

The AKS node pool incurs persistent costs to maintain availability for continuous validation requests. Conversely, ACI operates on a consumption-based model, incurring no idle costs and cleaning up resources automatically upon job completion.

### Question 8.4: Durable Functions vs Plain HTTP

Durable Functions provide robust state management and automated retries, preventing workflow disruptions during long-running tasks. They also eliminate the risk of client-side timeouts by enabling an asynchronous polling pattern.

### Question 8.5: Cost Review

![Resource Group Overview](docs/resource-group-overview.png)

Description: The AKS cluster is the primary cost driver due to the persistent virtual machine resources required for the node pool.

### Question 8.6: Challenges Faced

- **Environment-Specific Path Handling**: A notable challenge involved the incorrect conversion of Azure Resource IDs into Windows file paths by the Git Bash terminal. This was mitigated by utilizing the `MSYS_NO_PATHCONV=1` environment variable during CLI operations.
- **Log Verbositiy**: The high verbosity of Durable Function logs initially hindered monitoring. I addressed this by utilizing `grep` to filter the log stream for critical execution markers.

---