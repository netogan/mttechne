# Mttechne challenge

Document centralizing all challenge information.

## Solution design
![design-drwaio](https://raw.githubusercontent.com/netogan/mttechne/e2f1143e9857cb361ef65579eda1dbc4403e20c7/resources/fluxo-de-caixa.png)

## Modules
- [mttechne-cashflow-api](https://github.com/netogan/mttechne-cash-flow-api) - Responsible for managing cash flow.
- [mttechne-consolidation-api](https://github.com/netogan/mttechne-cash-flow-api) - Responsible for processing the consolidation generating a report.

## Patterns 
- Separation into logical layers (controller, domain, data, repository, integrations).
- Dependecy injection with .NET.
- DTO use for transference of the data from API and the data base.

## Some techs and libs used
- ``.NET 8``
- ``JWT``
- ``Swagger``
- ``Entity Framework Core``
- ``Bcrypt``
- ``iText7``
- ``Stubble``
- ``Quartz``
- ``RestSharp``
- ``PostgreSQL``
- ``SQLite``
- ``xUnit``
- ``Bogus``

## Auth by token in the cashflow-api module
To use the cash flow API features, authentication is required.

Endpoint to auth:
POST api/authentication/token
```
Body:
{
    "userName": "admin",
    "password": "adminpassword"
}
```

## Cluster Criation
Instructions for creating a kubernetes cluster in the docker desktop architecture

### Prerequisites
- Winget
- Docker Desktop
- Kubectl CLI

### Instalation

To install Winget (microsoft package manager) access the [link](https://learn.microsoft.com/pt-br/windows/package-manager/winget/#install-winget).

To install Docker Desktop 
```sh
winget install -e --id Docker.DockerDesktop
```

Install the Kubectl CLI to enter commands for deployments and other functionality.

```sh
winget install -e --id Kubernetes.kubectl
```

Deployment of the cashflow-api module in the solution directory, include configMap, service and postgreSQL.
```sh
kubectl apply -f .\k8s\cashflowapi-deployment.yaml
```

Deployment of the consolidation-api module in the solution directory, include configMap and service.
```sh
kubectl apply -f .\k8s\consolidation-deployment.yaml
```

## Health
The application has HealthCheck packages validating health, which can be accessed through the ```/api/health``` endpoint.
The deploy yaml manifests are configured with the ```livenessProbe``` and ```readinessProbe``` properties to ensure pods are running.
