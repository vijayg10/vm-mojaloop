# Deploying mojaloop in local machine using virtual box and vagrant

This vagrant file uses the automated scripts in the repository https://github.com/tdaly61/mini-loop

## Pre-requisites

Install the following softwares on your machine

- Git
- VirtualBox
- vagrant

## Deployment

Run the following commands to deploy mojaloop

```
git clone https://github.com/vijayg10/vm-mojaloop.git
cd vm-mojaloop
vagrant up
```
** This will take approximately 10-20min depending on the system configuration.

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


### Test system health in your browser after installation.

This will only work if you have an active helm chart deployment running.

Note: The examples below are only applicable to a local deployment. The entries should match the DNS values or ingress rules as configured in the values.yaml or otherwise matching any custom ingress rules configured.

ml-api-adapter health test: http://ml-api-adapter.local/health

central-ledger health test: http://central-ledger.local/health

## Look at the pods

- Login to the VM using the following command
  ```
  vagrant ssh
  ```

- From the VM, use the following command to get the pods in kubernetes
  ```
  kubectl get pods
  ```

## Execute helm tests

- Login to the VM using the following command
  ```
  vagrant ssh
  ```

- From the VM, use the following command to execute TTK test cases
  ```
  helm test ml --logs
  ```

## P2P transfer using Testing Toolkit

- After executing the `helm tests`, we can make a P2P transfer using testing toolkit UI
- Open your web browser and go to http://testing-toolkit.local/
- Go to 'Test Runner'
- Go to `Collection Manager`, click on `Import from Github` and import the folder 'golden_path/feature_tests/p2p_money_transfer'
- Select the file `p2p_money_transfer/p2p_happy_path.json` and close the 'Collection Manager'
- Click on `Run` button at the rop right corner and see the results
- After test case execution, edit the test case and look for the results tab in each request in the `Test case Editor`