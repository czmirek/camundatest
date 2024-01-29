# Camunda 8.4 OIDC POC

This repository is a POC for running Camunda components with the OIDC support documented for 8.4 here - https://docs.camunda.io/docs/self-managed/platform-deployment/helm-kubernetes/guides/connect-to-an-oidc-provider/

The requirements are following:

- We don't care about multitenancy
- We need to run only the following components:
  - Zeebe
  - Operate
  - Optimize
  - WebModeler

## Progress

### ✅ Zeebe

The following ENV vars must be configured
      
- ZEEBE_BROKER_GATEWAY_SECURITY_AUTHENTICATION_IDENTITY_ISSUERBACKENDURL
  - This is the URL of your OIDC authority
- ZEEBE_BROKER_GATEWAY_SECURITY_AUTHENTICATION_IDENTITY_AUDIENCE
    - This is any string that MUST be present in the `aud` property of the JWT token
- ZEEBE_BROKER_GATEWAY_SECURITY_AUTHENTICATION_IDENTITY_TYPE=keycloak
    - Must be set to `keycloak` although it is a generic OIDC
- ZEEBE_BROKER_GATEWAY_SECURITY_AUTHENTICATION_IDENTITY_BASEURL
    - This is the URL of your OIDC authority

### 🛑 Operate
todo 

Cannot make this work following docs, Operate throws exception when OIDC redirects back.


### 🛑 Optimize
todo

### 🛑 WebModeler
todo