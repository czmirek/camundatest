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

## How to set up KeyCloak client for Zeebe

### Step 1 - Client scope
 
- Go to Client scopes
- Click "Create client scope"
  - Name: testaudience
  - Leave everything else as is
- Save
- In the list of existing client scopes, click on the scope with the name "roles"
- Click on tab "Mappers"
- Remove the first row that has "audience" in name by clicking on the menu in the right part of the row and choose "Delete"

This way we configured the audience token to be a single value and not array.

### Step 2 - Client
- Go to clients - Create client
  - Client ID - "zeebeclient"
  - Next
  - Client authentication: **ON**
  - Authorization: **OFF**
  - Authentication flow: pick only **service accounts roles**
  - Next --- leave everything in Login settings 
  - ...and Save

- Click on the newly created "zeebeclient"
- Click on the tab "Client scopes"
- Click on "Add client scope"
- Pick "testaudience" and save with assigned type "Default"



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