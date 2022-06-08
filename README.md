# Deploying mojaloop in local machine using virtual box and vagrant

## Pre-requisites

- Git
- VirtualBox
- vagrant

## Deployment

Run the following commands to deploy mojaloop

```
git clone https://github.com/vijayg10/vm-mojaloop.git
vagrant up
```

## Verifying the deployment

### Update your /etc/hosts

Include the following lines (or alternatively combine them) to the host config.
```
vi /etc/hosts
```
```
# Mojaloop Demo
127.0.0.1   ml-api-adapter.local central-ledger.local account-lookup-service.local account-lookup-service-admin.local quoting-service.local central-settlement-service.local transaction-request-service.local central-settlement.local bulk-api-adapter.local moja-simulator.local sim-payerfsp.local sim-payeefsp.local sim-testfsp1.local sim-testfsp2.local sim-testfsp3.local sim-testfsp4.local mojaloop-simulators.local finance-portal.local operator-settlement.local settlement-management.local testing-toolkit.local testing-toolkit-specapi.local
```

** Windows the file can be updated in notepad - need to open with Administrative privileges. File location C:\Windows\System32\drivers\etc\hosts.


### Test system health in your browser after installation. This will only work if you have an active helm chart deployment running.

Note: The examples below are only applicable to a local deployment. The entries should match the DNS values or ingress rules as configured in the values.yaml or otherwise matching any custom ingress rules configured.

ml-api-adapter health test: http://ml-api-adapter.local/health

central-ledger health test: http://central-ledger.local/health
