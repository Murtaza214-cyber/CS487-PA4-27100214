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

### Evidence 3.2: Local Function Handler Listing

![Portal Function List](docs/portal-functions-list.png)

Description: The Azure Portal displays the discovered function triggers, confirming the presence of the `http_starter`, `my_orchestrator`, and both activity handlers.

---

## Task 4: Function App Container Deployment (8 points)

### Evidence 4.1: Function App Container Configuration

![Function App Container Settings 1](docs/func-container-settings-1.png)
![Function App Container Settings 2](docs/func-container-settings-2.png)

Description: The Deployment Center settings confirm the Function App is configured to pull the authenticated `func-app:v1` image from the `pa427100214` registry.

![Functions list](docs/functions-list.png)
Description: Screenshot of the Functions list in the Portal showing http_starter, my_orchestrator, validate_activity, report_activity

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
![Validation](docs/curl-validate.png)

Description: The API demonstrates correct behavior by approving valid quantities and rejecting orders that exceed the defined threshold of 100 units.

### Evidence 5.5: Function App `VALIDATE_URL`

![Function App CLI Config](docs/az-function-config-cli.png)
![Function App Portal Settings](docs/portal-env-validate-url.png)

Description: The environment variable `VALIDATE_URL` has been successfully applied to the Function App, enabling connectivity to the AKS LoadBalancer.


---

## Task 6: ACI Report Job (15 points)

### Evidence 6.1: Blob Container

![Blob Container Creation](docs/az-storage-container-create.png)

Description: The Azure CLI output confirms the successful creation of the `reports` container within the storage account.

### Evidence 6.2: Manual ACI Run

![Manual ACI Test State](docs/Screenshot%20of%20az%20container%20show.png.png)

Description: The `ci-report-test` instance reached a "Succeeded" state, verifying that the `report-job` image can execute successfully in a serverless environment.

### Evidence 6.3: ACI Logs

![Reporting Job Logs](docs/View%20logs%20from%20the%20container.png)


### Evidence 6.4: Generated PDF

![Storage Browser Reports](docs/storage-browser-reports.png)

Description:

### Evidence 6.5: Function App Managed Identity and IAM

![Portal Identity View](docs/portal-identity-managed.png)

Description: The evidence displays the User Assigned Managed Identity associated with the Function App to facilitate secure resource management.

### Evidence 6.6: Report App Settings

![Report Environment Variables](docs/report-app-settings-portal.png)

Description: The configuration demonstrates that all required reporting and identity variables have been formally applied to the Function App.

---

## Task 7: End-to-End Pipeline (15 points)

### Evidence 7.1: Happy Path UI

![UI Submission Form](docs/happy-path-ui-form.png)
![UI Running Status](docs/happy-path-ui-running.png)
![UI Completion Status](docs/happy-path-ui-completed.png)
![Generated PDF locally](docs/pdf-report-opened.png)

Description: The dashboard demonstrates a complete orchestration cycle, successfully processing a valid order and providing a functional PDF report link.

### Evidence 7.3: Backend Participation

![Log Stream Trace](docs/participation-trace.png)
![Log Stream Trace](docs/participation-trace-2.png)
![Validate Activity Trace](docs/validate-activity-trace.png)
![Report Activity Trace](docs/report-activity-trace.png)
![Presence of Reports in Container](docs/test-container.png)
Description: The filtered log stream provides a formal trace of the order ID as it is successfully validated by the AKS microservice and reported via ACI.

### Evidence 7.4: Reject Path UI

![Rejected Order Dashboard](docs/reject-path-ui.png)
![Rejected trace](docs/Rejected%20trace.png)
![Rejected trace](docs/Rejected%20trace%202.png.png)

Description: The frontend correctly communicates the rejection status when the validation activity identifies a quantity exceeding 100 units.

### Evidence 7.5: Resource Group
![Resource Group](docs/resource-group.png)
---


## Task 8: Write-up and Architecture Diagram (5 points)

### Evidence 8.1: Architecture Diagram

![System Architecture Diagram](docs/architecture-diagram.png)

Description: The diagram illustrates the service interdependencies across App Service, Durable Functions, AKS, ACI, and Blob Storage.

### Question 8.2: Service Selection

- **App Service**: Chosen for the frontend to leverage managed platform features and seamless GitHub Actions integration.
- **Durable Functions**: Utilized to manage the complex, stateful orchestration required to chain separate cloud services.
- **AKS**: Selected to host the validator API as a dedicated, high-availability microservice.
- **ACI**: Optimal for the reporting job as a consumption-based, ephemeral container service that bills only during active execution.

### Question 8.3: ACI vs AKS

The AKS node pool incurs persistent costs to maintain availability for continuous validation requests. Conversely, ACI operates on a consumption-based model, incurring no idle costs and cleaning up resources automatically upon job completion.

### Question 8.4: Durable Functions vs Plain HTTP

Durable Functions provide robust state management and automated retries, preventing workflow disruptions during long-running tasks. They also eliminate the risk of client-side timeouts by enabling an asynchronous polling pattern.

### Question 8.5: Cost Review

![Resource Group Overview](docs/resource-group-overview.png)

Description: As of May 6, 2026, the total actual consumption for this assignment is $1.78, with a projected monthly forecast of $12.47. Although the App Service Web App currently appears as the primary cost driver ($1.60) due to initial provisioning and security overhead, the AKS cluster is architecturally the most expensive resource in the pipeline. While its current cost appears negligible in this short-term snapshot, AKS relies on persistent Virtual Machine nodes that incur continuous hourly charges. In a sustained deployment, these fixed compute costs would significantly exceed the consumption-based billing models of the Function App and ACI instances.

### Question 8.6: Challenges Faced

A primary challenge involved subscription security policies blocking the default storage connection string for the Function App. I resolved this by implementing a Managed Identity (mi-pa4-27100214) and updating environment variables to authenticate via Client ID and Account Name. Additionally, the GitHub Actions pipeline failed initially due to configuration errors in the deployment YAML file. I successfully debugged the workflow logs and corrected the YAML file to restore the automated CI/CD path for the App Service.
---