# UCP (Universal Control Plane)

Universal Control Plane (UCP) is the enterprise-grade cluster management solution from Docker. You install it on-premises or in your virtual private cloud, and it helps you manage your Docker cluster and applications through a single interface.

https://docs.mirantis.com/docker-enterprise/v3.0/dockeree-products/ucp.html

## client bundles

allows you to manage and run UCP via the docker commandline with the proper authentication.

- UCP, go to admin, My Profile, Client Bundles

## Logging

`http://man.hubwiz.com/docset/Docker.docset/Contents/Resources/Documents/docs.docker.com/ee/ucp/admin/configure/create-audit-logs.html`

Logging levels
To allow more control to administrators over the audit logging, three audit logging levels are provided:

### None

audit logging is disabled

### Metadata

includes the following:

- Method and API endpoint for the request
- UCP user who made the request
- Response Status (success or failure)
- Timestamp of the call
- Object ID of any created or updated resource (for create or update API calls). We do not include names of created or updated resources
- License Key
- Remote Address

### Request

 includes all fields from the Metadata level as well as the request payload.

### Enabling UCP Audit Logging

UCP audit logging can be enabled via the UCP web user interface, the UCP API or via the UCP configuration file.

Enabling UCP Audit Logging via UI

- Log in to the UCP Web User Interface
- Navigate to Admin Settings
- Select Audit Logs
- In the Configure Audit Log Level section, select the relevant logging level
