# Camunda 8.4 OIDC POC

This repository is a POC for running Camunda components with the OIDC support documented for 8.4 here - https://docs.camunda.io/docs/self-managed/platform-deployment/helm-kubernetes/guides/connect-to-an-oidc-provider/

The requirements are following:

- We don't care about multitenancy
- We need to run only the following components:
  - Zeebe
  - Operate
  - Optimize
  - WebModeler

## How to set up

- You need to create your OIDC provider. It can be KeyCloak, IdentityServer, does not matter as far as it can do OIDC.
- Look in the `docker-compose-core.yaml` file and replace the URL where needed.
- `docker compose -f docker-compose-core.yaml up --detach` for running
- `docker compose -f docker-compose-core.yaml down` for stopping and removing

## Progress

### ✅ Zeebe

The following ENV vars must be configured
      
- `ZEEBE_BROKER_GATEWAY_SECURITY_AUTHENTICATION_IDENTITY_ISSUERBACKENDURL`
  - This is the URL of your OIDC authority
- `ZEEBE_BROKER_GATEWAY_SECURITY_AUTHENTICATION_IDENTITY_AUDIENCE`
    - This is any string that MUST be present in the `aud` property of the JWT token
- `ZEEBE_BROKER_GATEWAY_SECURITY_AUTHENTICATION_IDENTITY_TYPE`
    - Must be set to `keycloak` although it is a generic OIDC
- `ZEEBE_BROKER_GATEWAY_SECURITY_AUTHENTICATION_IDENTITY_BASEURL`
    - This is the URL of your OIDC authority

### 🛑 Operate
todo 

Cannot make this work following docs, Operate throws exception when OIDC redirects back.


### 🛑 Optimize
todo

### 🛑 WebModeler
todo