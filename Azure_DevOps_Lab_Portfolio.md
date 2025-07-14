# Azure DevOps Lab Portfolio

This lab portfolio showcases your hands-on experience with Azure DevOps practices using GitHub, Bicep, Azure App Services, Traffic Manager, and Chaos Studio.

---

## Lab 01 – Agile Planning and Management Using GitHub

### Objectives
- Create and manage GitHub issues and boards.
- Track work with milestones and labels.

### Artifacts
- GitHub project board created.
- Issues labeled and tracked via milestones.

---

## Lab 02 – Implement Flow of Work with GitHub

### Objectives
- Fork a repository and create a feature branch.
- Modify code, commit, and create a pull request.

### Git Commands Used
```bash
mkdir myWebApp
cd myWebApp
git init
git config --global user.name "John Doe"
git config --global user.email "john.doe@contoso.com"
```

### Actions
- Edited and committed changes via Visual Studio Code.
- Created and merged feature branches.

---

## Lab 03 – Implement CI/CD with GitHub Actions and IaC with Bicep

### Objectives
- Define GitHub Actions workflows.
- Use Bicep to provision Azure App Services.

### Key Concepts
- Infrastructure as Code (IaC) with Bicep.
- CI/CD using GitHub Actions.

---

## Lab 04 – Enhance Resiliency with Traffic Manager & Chaos Studio

### Scenario
Your team supports an online retail store experiencing intermittent regional outages. This lab configures Traffic Manager to distribute workloads and Chaos Studio to simulate failure scenarios.

### Tools
- **Azure Traffic Manager**: Global DNS-based load balancer
- **Azure Chaos Studio**: Fault injection to test app resilience

### Part 1 – Configure Traffic Manager
```bash
az network traffic-manager profile create \
  --name devopsfoundationstmprofile \
  --resource-group rg-devops-foundations \
  --routing-method Priority \
  --ttl 5 \
  --protocol HTTPS \
  --port 443 \
  --path "/" \
  --unique-dns-name <unique_name>
```

- Added endpoints for East US (priority 1) and West Europe (priority 2)
- Enabled health checks

### Part 2 – Simulate Failure with Chaos Studio
```bash
az chaos experiment create \
  --name DevOps_Foundations_Labs_Experiment_01 \
  --resource-group rg-devops-foundations \
  --location westeurope \
  --experiment-file experiment.json
```

- Stopped East US App Service for 10 minutes.
- Verified Traffic Manager rerouted traffic to West Europe.

### Validation Commands
```bash
nslookup <your_traffic_manager_profile>.trafficmanager.net
```

Run multiple times after 5 seconds to observe failover.

---

## Resource Cleanup
```bash
az group delete --name rg-devops-foundations --yes --no-wait
az group delete --name rg-eshoponweb-eastus --yes --no-wait
az group delete --name rg-eshoponweb-westeurope --yes --no-wait
```

---

## Portfolio Value
This lab sequence demonstrates:
- Git and GitHub proficiency
- CI/CD pipeline design
- Infrastructure automation with Bicep
- Cloud-native resiliency testing

---

## Optional Enhancements
- Add badge for GitHub Actions status.
- Deploy as GitHub Pages documentation site.
- Include architecture diagrams (available upon request).

---

**Author:** CÇĆČĊ  
**Role:** IT & DevOps Professional

> "Resilience isn't a nice-to-have. It's built, tested, and proven—before failure ever happens."