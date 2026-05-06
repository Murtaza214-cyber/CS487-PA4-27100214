<div align="center">

# PA4 Submission: TaskFlow Pipeline

<img alt="GitHub only" src="https://img.shields.io/badge/Submit-GitHub%20URL%20Only-10b981?style=for-the-badge">
<img alt="Total points" src="https://img.shields.io/badge/Total-100%20points-7c3aed?style=for-the-badge">

</div>

<div style="background:#f5f3ff;color:#111827;border-left:6px solid #6330bc;padding:14px 18px;border-radius:10px;margin:18px 0;">
Copy this file to <code style="color:#111827;background:#ddd6fe;padding:2px 4px;border-radius:4px;">SUBMISSION.md</code>. Put every screenshot in <code style="color:#111827;background:#ddd6fe;padding:2px 4px;border-radius:4px;">docs/</code>, embed it under the correct task, and write a short description below each image explaining what it proves. The grader should not need any file outside this repository.
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

- Use relative image paths, for example: `![AKS nodes](docs/aks-nodes.png)`.
- Every image must have a 1-3 sentence description below it.
- Azure Portal screenshots must show the resource name and enough page context to identify the service.
- CLI screenshots must show the command and output.
- Mask secrets such as function keys, ACR passwords, and storage connection strings.


## Task 1: App Service Web App (15 points)

### Evidence 1.1: Forked Repository

![Forked Repo](docs/github-fork.png)

[cite_start]Description: This screenshot shows the forked repository `CS487-PA4-27100214` under my GitHub profile, containing the project starter structure[cite: 4].

### Evidence 1.2: App Service Overview

![Web App Overview](docs/webapp-overview.png)

[cite_start]Description: The App Service `pa4-27100214` is running on a Node 22-lts runtime within the `rg-sp26-27100214` resource group in the `ukwest` region[cite: 5].

### Evidence 1.3: Deployment Center / GitHub Actions

![Deployment Center](docs/deployment-center.png)

[cite_start]Description: This proves the Web App is linked to my GitHub repository with successful deployment logs showing the GitHub Actions integration[cite: 6].

### Evidence 1.4: Live Web UI

![Live Web UI](docs/live-ui.png)

[cite_start]Description: This confirms the App Service is successfully serving the TaskFlow frontend dashboard at its public URL[cite: 7].

---

## Task 2: Azure Container Registry (15 points)

### Evidence 2.1: ACR Overview

![ACR Overview](docs/acr-overview.png)

[cite_start]Description: The container registry `pa427100214` is active on the Basic SKU within the `ukwest` region[cite: 10].

### Evidence 2.2: Docker Builds

![Docker Builds](docs/docker-builds.png)

[cite_start]Description: These logs show successful local Docker builds for the `validate-api`, `report-job`, and `func-app` images[cite: 11].

### Evidence 2.3: ACR Repositories

![ACR Repositories](docs/acr-repositories.png)

[cite_start]Description: The CLI output confirms that all three container images have been successfully pushed to the ACR repositories[cite: 13, 14].

---

## Task 3: Durable Function Implementation (12 points)

### Evidence 3.1: Completed Function Code

[function_app.py](function-app/function_app.py)

Description: The orchestration logic in the function code chains the validation and reporting activities to process orders sequentially.

### Evidence 3.2: Local Function Handler Listing

![Function Handlers](docs/function-handlers.png)

[cite_start]Description: This portal view confirms that all four function handlers (starter, orchestrator, and two activities) are discovered and enabled[cite: 16].

---

## Task 4: Function App Container Deployment (8 points)

### Evidence 4.1: Function App Container Configuration

![Function App Container Config](docs/func-container-config.png)

[cite_start]Description: The Function App is configured to use the `func-app:v1` image from the `pa427100214` private registry[cite: 15].

### Evidence 4.2: Orchestration Smoke Test

![Orchestration Smoke Test](docs/smoke-test.png)

[cite_start]Description: The `curl` output shows a successful orchestration start, providing the unique instance ID and status query URLs[cite: 17].

### Evidence 4.3: Expected Failed Status Before Downstream Wiring

![Expected Failure Status](docs/expected-failure.png)

[cite_start]Description: The status JSON shows an expected failure with a `KeyError: 'VALIDATE_URL'`, as the downstream environment variable was not yet configured[cite: 18].

---

## Task 5: AKS Validator (15 points)

### Evidence 5.1: AKS Cluster

![AKS Cluster Overview](docs/aks-overview.png)

[cite_start]Description: The AKS cluster `pa4-27100214` is active and healthy in the `ukwest` region[cite: 20].

### Evidence 5.2: Kubernetes Nodes and Pods

![K8s Pods](docs/k8s-pods.png)

[cite_start]Description: This proves the cluster node is ready and the `validate-deployment` pod is successfully running[cite: 20, 21].

### Evidence 5.3: Kubernetes Service

![K8s Service](docs/k8s-service.png)

[cite_start]Description: The `validate-service` is exposed as a LoadBalancer with a public external IP address on port 8080[cite: 22].

### Evidence 5.4: Validator API Tests

![Validator API Tests](docs/api-tests.png)

[cite_start]Description: Testing the endpoint confirms it correctly validates orders and rejects quantities exceeding 100[cite: 23].

### Evidence 5.5: Function App `VALIDATE_URL`

![Validate URL Config](docs/validate-url-config.png)

[cite_start]Description: The Function App settings now include the `VALIDATE_URL` pointing to the AKS LoadBalancer's IP[cite: 23].

### Evidence 5.6: AKS Idle Behavior

![AKS Nodes](docs/aks-nodes.png)

Description: The AKS nodes remain in a "Ready" state while idle, ensuring immediate availability for incoming validation requests.

---

## Task 6: ACI Report Job (15 points)

### Evidence 6.1: Blob Container

![Blob Container](docs/blob-container.png)

[cite_start]Description: The `reports` container was successfully created in blob storage to host the generated PDF files[cite: 24].

### Evidence 6.2: Manual ACI Run

![Manual ACI Run](docs/manual-aci.png)

[cite_start]Description: The `ci-report-test` container reached a "Succeeded" state, proving the image is viable for one-off job execution[cite: 26].

### Evidence 6.3: ACI Logs

![ACI Logs](docs/aci-logs.png)

[cite_start]Description: The logs show the report job successfully used its credentials to generate the report and interact with storage[cite: 26].

### Evidence 6.4: Generated PDF

![Generated PDF](docs/generated-pdf.png)

[cite_start]Description: The storage browser proves that `TEST-001.pdf` was written to the `reports` container by the ACI job[cite: 26].

### Evidence 6.5: Function App Managed Identity and IAM

![Managed Identity](docs/managed-identity.png)

[cite_start]Description: This confirms that the User Assigned Identity is correctly associated with the Function App for resource management[cite: 25].

### Evidence 6.6: Report App Settings

![Report Settings](docs/report-settings.png)

[cite_start]Description: The Function App is configured with all necessary `REPORT_*` and `ACR_*` environment variables for Task 6 orchestration[cite: 25].

---

## Task 7: End-to-End Pipeline (15 points)

### Evidence 7.1: Web App Wiring

![Web App Wiring](docs/frontend-wiring.png)

[cite_start]Description: The App Service is now wired to the Function App's orchestrator and status webhooks[cite: 8].

### Evidence 7.2: Happy Path UI

![Happy Path UI](docs/happy-path.png)

[cite_start]Description: The frontend successfully displays the "Completed" status and provides a download link for a valid order[cite: 26].

### Evidence 7.3: Backend Participation

![Backend Logs](docs/backend-participation.png)

[cite_start]Description: These logs trace a single order ID as it is validated by AKS and processed by a dynamically spawned ACI[cite: 26].

### Evidence 7.4: Reject Path UI

![Reject Path UI](docs/reject-path.png)

[cite_start]Description: The UI correctly displays a "Rejected" message for an order with a quantity exceeding the allowed limit[cite: 26].

---

## Task 8: Write-up and Architecture Diagram (5 points)

### Evidence 8.1: Architecture Diagram

![Architecture Diagram](docs/architecture-diagram.png)

Description: The diagram illustrates the full TaskFlow flow from GitHub through App Service, Durable Functions, AKS, and ACI.

### Question 8.2: Service Selection

- **App Service**: Chosen for the frontend due to its seamless CI/CD integration and managed scaling for web applications.
- **Durable Functions**: Selected to manage the complex, multi-step state of the order pipeline, ensuring reliable execution of sequential tasks.
- **AKS**: Used for the validator API to maintain a persistent, high-performance microservice capable of handling continuous requests.
- **ACI**: Utilized for reporting because it provides serverless container execution—billing only when the report is being generated and cleaning up immediately after.

### Question 8.3: ACI vs AKS

AKS nodes remain running and billing while idle, whereas ACI only costs money during the actual execution of the container. AKS is better for long-running services (Validator), while ACI is optimal for ephemeral jobs (Reporting).

### Question 8.4: Durable Functions vs Plain HTTP

Durable Functions provide automatic state management and checkpoints, preventing "zombie" states if a single step fails. They also solve the issue of HTTP timeouts by allowing the client to poll for status rather than maintaining a long-running connection.

### Question 8.5: Cost Review

![Cost Management](docs/cost-review.png)

Description: AKS is currently the most expensive service because it requires dedicated virtual machines to be running in the node pool at all times.

### Question 8.6: Challenges Faced

---