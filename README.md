# Camunda 8.4 OIDC POC

This repository is a POC for running Camunda components with the OIDC support documented for 8.4 here - https://docs.camunda.io/docs/self-managed/platform-deployment/helm-kubernetes/guides/connect-to-an-oidc-provider/

The requirements are following:

- We don't care about multitenancy
- We need to run only the following components:
  - Zeebe
  - Operate
  - Optimize
  - WebModeler
  - Tasklist

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

### ✅ Operate

The following ENV vars must be configured

- `CAMUNDA_IDENTITY_TYPE`
  - Must be set to `GENERIC`
- `CAMUNDA_IDENTITY_ISSUER`
  - URL of your OIDC authority
- `CAMUNDA_IDENTITY_ISSUER_BACKEND_URL`
  - URL of your OIDC authority
- `CAMUNDA_IDENTITY_CLIENT_ID`
  - A client ID for Operate to access OIDC authority
- `CAMUNDA_IDENTITY_CLIENT_SECRET`
  - A client secret for Operate to access OIDC authority
- `CAMUNDA_IDENTITY_AUDIENCE`
  - This is any string that MUST be present in the `aud` property of the JWT token
- `CAMUNDA_IDENTITY_REDIRECTROOTURL`
  - Host URL of Operate to which OIDC redirects to
- `SPRING_SECURITY_OAUTH2_RESOURCESERVER_JWT_ISSUER_URI`
  - URL of your OIDC authority
- `SPRING_SECURITY_OAUTH2_RESOURCESERVER_JWT_JWK_SET_URI`
  - OIDC JWKS endpoint

### 🛑 Optimize
todo

### 🛑 WebModeler
todo

### 🛑 Tasklist
todo