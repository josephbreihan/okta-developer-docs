---
title: ASA Projects
category: asa
---

# ASA Projects API

## Get Started


| Product  | API Basics  | API Namespace        |
|----------|-------------|----------------------|
| [Advanced Server
Access](https://www.okta.com/products/advanced-server-access/) | [How the ASA API works](../introduction/) | `https://app.scaleft.com/v1/`

An ASA Project is a collection of ASA Servers and ASA Users that have access to those Servers through ASA Groups.


## Projects API Operations


The Projects API has the following operations:
* [List Projects for a Team](#list-projects-for-a-team)
* [Create a Project](#create-a-project)
* [Fetch a Project](#fetch-a-project)
* [Delete a Project](#delete-a-project)
* [Update a Project](#update-a-project)
* [List Client Configuration Options for a Project](#list-client-configuration-options-for-a-project)
* [Add Client Configuration Options for a Project](#add-client-configuration-options-for-a-project)
* [Remove a Client Configuration Option from a Project](#remove-a-client-configuration-option-from-a-project)
* [List Cloud Accounts in a Project](#list-cloud-accounts-in-a-project)
* [Add a Cloud Account to a Project](#add-a-cloud-account-to-a-project)
* [Remove a Cloud Account from a Project](#remove-a-cloud-account-from-a-project)
* [List all the ASA Groups in a Project](#list-all-the-asa-groups-in-a-project)
* [Add an ASA Group to a Project](#add-an-asa-group-to-a-project)
* [Retrieve ASA Group details for a single Project](#retrieve-asa-group-details-for-a-single-project)
* [Remove an ASA Group from a Project](#remove-an-asa-group-from-a-project)
* [Change the Project properties of an ASA Project Group](#change-the-project-properties-of-an-asa-project-group)
* [Fetch a Preauthorization](#fetch-a-preauthorization)
* [Create a Preauthorization](#create-a-preauthorization)
* [Lists the Preauthorizations for a Project](#lists-the-preauthorizations-for-a-project)
* [Update a Preauthorization](#update-a-preauthorization)
* [List Server Enrollment Tokens within a Project](#list-server-enrollment-tokens-within-a-project)
* [Create a Server Enrollment Token for a Project](#create-a-server-enrollment-token-for-a-project)
* [Fetch a Server Enrollment Token from a Project](#fetch-a-server-enrollment-token-from-a-project)
* [Delete a Server Enrollment Token from a Project](#delete-a-server-enrollment-token-from-a-project)
* [List Server Users in a Project](#list-server-users-in-a-project)
* [List Servers in a Project](#list-servers-in-a-project)
* [Add an Unmanaged Server to a Project](#add-an-unmanaged-server-to-a-project)
* [Get a Server object](#get-a-server-object)
* [Remove a Server from a Project](#remove-a-server-from-a-project)


### List Projects for a Team

<ApiOperation method="GET" url="https://app.scaleft.com/v1/teams/${team_name}/projects" />


#### Request path parameters

| Parameter | Type        | Description   |
| --------- | ----------- | ------------- |
| `team_name`   | string | The name of your Team. |


#### Request query parameters

| Parameter | Type   | Description |
| --------- | ------------- | -------- |
| `count`   |  integer | (Optional) The number of objects per page. |
| `descending`   |  boolean | (Optional) The object order. |
| `offset`   |  string | (Optional) The page offset. |
| `prev`   |  boolean | (Optional) The direction of paging. |
| `self`   |  boolean | (Optional) If true, only lists the Projects that this ASA User has been assigned. |


#### Request body

This endpoint has no request body.

#### Response body
This endpoint returns a list of objects with the following fields and a `200` code on a successful call.
| Parameter | Type        | Description          |
|----------|-------------|----------------------|
| `create_server_users`   | boolean | (Optional) Whether or not to create Server Users for ASA Users in this Project. Defaults to `False`. If left false, the ASA User is responsible for ensuring that users matching the names of the Server Users in ASA exist on the server. |
| `force_shared_ssh_users`   | boolean | (Optional) If true, new Server Users will not be created for each ASA User in the Project. Instead they will share a single standard user and a single admin user. Defaults to `False`. |
| `forward_traffic`   | boolean | Whether or not to require all traffic in Project to be forwarded through selected Gateways. Defaults to `False`. Warning: Currently requires a feature flag to be enabled. |
| `name`   | string | The name of the Project. |
| `rdp_session_recording`   | boolean | Whether or not to enable rdp recording on all Servers in this Project. Defaults to `False`. Warning: Currently requires a feature flag to be enabled. |
| `require_preauth_for_creds`   | boolean | (Optional) Whether or not to require preauthorization before an ASA User can retrieve credentials to log in. Defaults to `False`. |
| `shared_admin_user_name`   | string | (Optional) The name for a shared admin user on Servers in this Project. If `force_shared_ssh_users` is `True`, this must be provided. |
| `shared_standard_user_name`   | string | (Optional) The name for a shared standard user on Servers in this names Project. If `force_shared_ssh_users` is `True`, this must be provided. |
| `ssh_session_recording`   | boolean | Whether or not to enable ssh recording on all Servers in this Project. Defaults to `False`. Warning: Currently requires a feature flag to be enabled. |

#### Usage example

##### Request

```bash
curl -v -X GET \
-H "Authorization: Bearer ${jwt}" \
https://app.scaleft.com/v1/teams/${team_name}/projects```

##### Response
```json
{
	"list": [
		{
			"create_server_users": true,
			"deleted_at": "0001-01-01T00:00:00Z",
			"force_shared_ssh_users": false,
			"id": "84a4310e-ebd0-4f97-9d54-9178c863e875",
			"name": "the-sound-and-the-fury",
			"next_unix_gid": 63001,
			"next_unix_uid": 60001,
			"require_preauth_for_creds": true,
			"shared_admin_user_name": null,
			"shared_standard_user_name": null,
			"team": "william-faulkner",
			"user_on_demand_period": null
		},
		{
			"create_server_users": true,
			"deleted_at": "0001-01-01T00:00:00Z",
			"force_shared_ssh_users": false,
			"id": "84a4310e-ebd0-4f97-9d54-9178c863e875",
			"name": "the-sound-and-the-fury",
			"next_unix_gid": 63001,
			"next_unix_uid": 60001,
			"require_preauth_for_creds": true,
			"shared_admin_user_name": null,
			"shared_standard_user_name": null,
			"team": "william-faulkner",
			"user_on_demand_period": null
		}
	]
}
```
### Create a Project

<ApiOperation method="POST" url="https://app.scaleft.com/v1/teams/${team_name}/projects" />
Create a Project

#### Request path parameters

| Parameter | Type        | Description   |
| --------- | ----------- | ------------- |
| `team_name`   | string | The name of your Team. |


#### Request query parameters

This endpoint has no query parameters.

#### Request body

This endpoint requires an object with the following fields.
| Parameter | Type        | Description          |
|----------|-------------|----------------------|
| `create_server_users`   | boolean | (Optional) Whether or not to create Server Users for ASA Users in this Project. Defaults to `False`. If left false, the ASA User is responsible for ensuring that users matching the names of the Server Users in ASA exist on the server. |
| `force_shared_ssh_users`   | boolean | (Optional) If true, new Server Users will not be created for each ASA User in the Project. Instead they will share a single standard user and a single admin user. Defaults to `False`. |
| `forward_traffic`   | boolean | Whether or not to require all traffic in Project to be forwarded through selected Gateways. Defaults to `False`. Warning: Currently requires a feature flag to be enabled. |
| `name`   | string | The name of the Project. |
| `rdp_session_recording`   | boolean | Whether or not to enable rdp recording on all Servers in this Project. Defaults to `False`. Warning: Currently requires a feature flag to be enabled. |
| `require_preauth_for_creds`   | boolean | (Optional) Whether or not to require preauthorization before an ASA User can retrieve credentials to log in. Defaults to `False`. |
| `shared_admin_user_name`   | string | (Optional) The name for a shared admin user on Servers in this Project. If `force_shared_ssh_users` is `True`, this must be provided. |
| `shared_standard_user_name`   | string | (Optional) The name for a shared standard user on Servers in this names Project. If `force_shared_ssh_users` is `True`, this must be provided. |
| `ssh_session_recording`   | boolean | Whether or not to enable ssh recording on all Servers in this Project. Defaults to `False`. Warning: Currently requires a feature flag to be enabled. |

#### Response body
This endpoint returns an object with the following fields and a `201` code on a successful call.
| Parameter | Type        | Description          |
|----------|-------------|----------------------|
| `create_server_users`   | boolean | (Optional) Whether or not to create Server Users for ASA Users in this Project. Defaults to `False`. If left false, the ASA User is responsible for ensuring that users matching the names of the Server Users in ASA exist on the server. |
| `force_shared_ssh_users`   | boolean | (Optional) If true, new Server Users will not be created for each ASA User in the Project. Instead they will share a single standard user and a single admin user. Defaults to `False`. |
| `forward_traffic`   | boolean | Whether or not to require all traffic in Project to be forwarded through selected Gateways. Defaults to `False`. Warning: Currently requires a feature flag to be enabled. |
| `name`   | string | The name of the Project. |
| `rdp_session_recording`   | boolean | Whether or not to enable rdp recording on all Servers in this Project. Defaults to `False`. Warning: Currently requires a feature flag to be enabled. |
| `require_preauth_for_creds`   | boolean | (Optional) Whether or not to require preauthorization before an ASA User can retrieve credentials to log in. Defaults to `False`. |
| `shared_admin_user_name`   | string | (Optional) The name for a shared admin user on Servers in this Project. If `force_shared_ssh_users` is `True`, this must be provided. |
| `shared_standard_user_name`   | string | (Optional) The name for a shared standard user on Servers in this names Project. If `force_shared_ssh_users` is `True`, this must be provided. |
| `ssh_session_recording`   | boolean | Whether or not to enable ssh recording on all Servers in this Project. Defaults to `False`. Warning: Currently requires a feature flag to be enabled. |

#### Usage example

##### Request

```bash
curl -v -X POST \
-H "Authorization: Bearer ${jwt}" \
--data '{
	"create_server_users": true,
	"deleted_at": null,
	"force_shared_ssh_users": false,
	"id": "",
	"name": "the-sound-and-the-fury",
	"next_unix_gid": null,
	"next_unix_uid": 0,
	"require_preauth_for_creds": true,
	"shared_admin_user_name": null,
	"shared_standard_user_name": null,
	"team": "william-faulkner",
	"user_on_demand_period": null
}' \
https://app.scaleft.com/v1/teams/${team_name}/projects```

##### Response
```json
{
	"create_server_users": true,
	"deleted_at": "0001-01-01T00:00:00Z",
	"force_shared_ssh_users": false,
	"id": "84a4310e-ebd0-4f97-9d54-9178c863e875",
	"name": "the-sound-and-the-fury",
	"next_unix_gid": 63001,
	"next_unix_uid": 60001,
	"require_preauth_for_creds": true,
	"shared_admin_user_name": null,
	"shared_standard_user_name": null,
	"team": "william-faulkner",
	"user_on_demand_period": null
}
```
### Fetch a Project

<ApiOperation method="GET" url="https://app.scaleft.com/v1/teams/${team_name}/projects/${project_name}" />


#### Request path parameters

| Parameter | Type        | Description   |
| --------- | ----------- | ------------- |
| `project_name`   | string | The Project name. |
| `team_name`   | string | The name of your Team. |


#### Request query parameters

This endpoint has no query parameters.

#### Request body

This endpoint has no request body.

#### Response body
This endpoint returns an object with the following fields and a `200` code on a successful call.
| Parameter | Type        | Description          |
|----------|-------------|----------------------|
| `create_server_users`   | boolean | (Optional) Whether or not to create Server Users for ASA Users in this Project. Defaults to `False`. If left false, the ASA User is responsible for ensuring that users matching the names of the Server Users in ASA exist on the server. |
| `force_shared_ssh_users`   | boolean | (Optional) If true, new Server Users will not be created for each ASA User in the Project. Instead they will share a single standard user and a single admin user. Defaults to `False`. |
| `forward_traffic`   | boolean | Whether or not to require all traffic in Project to be forwarded through selected Gateways. Defaults to `False`. Warning: Currently requires a feature flag to be enabled. |
| `name`   | string | The name of the Project. |
| `rdp_session_recording`   | boolean | Whether or not to enable rdp recording on all Servers in this Project. Defaults to `False`. Warning: Currently requires a feature flag to be enabled. |
| `require_preauth_for_creds`   | boolean | (Optional) Whether or not to require preauthorization before an ASA User can retrieve credentials to log in. Defaults to `False`. |
| `shared_admin_user_name`   | string | (Optional) The name for a shared admin user on Servers in this Project. If `force_shared_ssh_users` is `True`, this must be provided. |
| `shared_standard_user_name`   | string | (Optional) The name for a shared standard user on Servers in this names Project. If `force_shared_ssh_users` is `True`, this must be provided. |
| `ssh_session_recording`   | boolean | Whether or not to enable ssh recording on all Servers in this Project. Defaults to `False`. Warning: Currently requires a feature flag to be enabled. |

#### Usage example

##### Request

```bash
curl -v -X GET \
-H "Authorization: Bearer ${jwt}" \
https://app.scaleft.com/v1/teams/${team_name}/projects/${project_name}```

##### Response
```json
{
	"create_server_users": true,
	"deleted_at": "0001-01-01T00:00:00Z",
	"force_shared_ssh_users": false,
	"id": "84a4310e-ebd0-4f97-9d54-9178c863e875",
	"name": "the-sound-and-the-fury",
	"next_unix_gid": 63001,
	"next_unix_uid": 60001,
	"require_preauth_for_creds": true,
	"shared_admin_user_name": null,
	"shared_standard_user_name": null,
	"team": "william-faulkner",
	"user_on_demand_period": null
}
```
### Delete a Project

<ApiOperation method="DELETE" url="https://app.scaleft.com/v1/teams/${team_name}/projects/${project_name}" />


#### Request path parameters

| Parameter | Type        | Description   |
| --------- | ----------- | ------------- |
| `project_name`   | string | The Project name. |
| `team_name`   | string | The name of your Team. |


#### Request query parameters

This endpoint has no query parameters.

#### Request body

This endpoint has no request body.

#### Response body
This endpoint returns a `204 No Content` response on a successful call.


#### Usage example

##### Request

```bash
curl -v -X DELETE \
-H "Authorization: Bearer ${jwt}" \
https://app.scaleft.com/v1/teams/${team_name}/projects/${project_name}```

##### Response
```json
HTTP 204 No Content
```
### Update a Project

<ApiOperation method="PUT" url="https://app.scaleft.com/v1/teams/${team_name}/projects/${project_name}" />


#### Request path parameters

| Parameter | Type        | Description   |
| --------- | ----------- | ------------- |
| `project_name`   | string | The Project name. |
| `team_name`   | string | The name of your Team. |


#### Request query parameters

This endpoint has no query parameters.

#### Request body

This endpoint requires an object with the following fields.
| Parameter | Type        | Description          |
|----------|-------------|----------------------|
| `create_server_users`   | boolean | (Optional) Whether or not to create Server Users for ASA Users in this Project. Defaults to `False`. If left false, the ASA User is responsible for ensuring that Users matching the Server User names in ASA exist on the server. |
| `forward_traffic`   | boolean | Whether or not to require all traffic in Project to be forwarded through selected Gateways. Defaults to `False`. Warning: Currently requires a feature flag to be enabled. |
| `rdp_session_recording`   | boolean | Whether or not to enable rdp recording on all Servers in this Project. Defaults to `False`. Warning: Currently requires a feature flag to be enabled. |
| `require_preauth_for_creds`   | boolean | (Optional) Whether or not to require preauthorization before an ASA User can retrieve credentials to log in. Defaults to `False`. |
| `ssh_session_recording`   | boolean | Whether or not to enable ssh recording on all Servers in this Project. Defaults to `False`. Warning: Currently requires a feature flag to be enabled. |

#### Response body
This endpoint returns a `204 No Content` response on a successful call.


#### Usage example

##### Request

```bash
curl -v -X PUT \
-H "Authorization: Bearer ${jwt}" \
--data '{
	"create_server_users": true,
	"next_unix_gid": 63011,
	"next_unix_uid": 60011,
	"require_preauth_for_creds": false,
	"user_on_demand_period": null
}' \
https://app.scaleft.com/v1/teams/${team_name}/projects/${project_name}```

##### Response
```json
HTTP 204 No Content
```
### List Client Configuration Options for a Project

<ApiOperation method="GET" url="https://app.scaleft.com/v1/teams/${team_name}/projects/${project_name}/client_config_options" />
Use Client Configuration Options to automatically pass settings to any Client logging into a server in this Project.

#### Request path parameters

| Parameter | Type        | Description   |
| --------- | ----------- | ------------- |
| `project_name`   | string | The Project name. |
| `team_name`   | string | The name of your Team. |


#### Request query parameters

This endpoint has no query parameters.

#### Request body

This endpoint has no request body.

#### Response body
This endpoint returns a list of objects with the following fields and a `200` code on a successful call.
| Parameter | Type        | Description          |
|----------|-------------|----------------------|
| `config_key`   | string | The Client Configuration Option to change. |
| `config_value`   | object | The value to be applied to Clients' configurations. |
| `id`   | string | The UUID of the Client Configuration Option. |

#### Usage example

##### Request

```bash
curl -v -X GET \
-H "Authorization: Bearer ${jwt}" \
https://app.scaleft.com/v1/teams/${team_name}/projects/${project_name}/client_config_options```

##### Response
```json
{
	"list": [
		{
			"config_key": "ssh.insecure_forward_agent",
			"config_value": "host",
			"id": "f332114d-38a8-446b-b346-0c58544d8381"
		},
		{
			"config_key": "ssh.port_forward_method",
			"config_value": "netcat",
			"id": "22c0b45a-2e50-45c8-851c-41af91326579"
		}
	]
}
```
### Add Client Configuration Options for a Project

<ApiOperation method="POST" url="https://app.scaleft.com/v1/teams/${team_name}/projects/${project_name}/client_config_options" />


#### Request path parameters

| Parameter | Type        | Description   |
| --------- | ----------- | ------------- |
| `project_name`   | string | The Project name. |
| `team_name`   | string | The name of your Team. |


#### Request query parameters

This endpoint has no query parameters.

#### Request body

This endpoint requires an object with the following fields.
| Parameter | Type        | Description          |
|----------|-------------|----------------------|
| `config_key`   | string | The Client Configuration Option to change. |
| `config_value`   | object | The value to be applied to Clients' configurations. |
| `id`   | string | The UUID of the Client Configuration Option. |

#### Response body
This endpoint returns an object with the following fields and a `200` code on a successful call.
| Parameter | Type        | Description          |
|----------|-------------|----------------------|
| `config_key`   | string | The Client Configuration Option to change. |
| `config_value`   | object | The value to be applied to Clients' configurations. |
| `id`   | string | The UUID of the Client Configuration Option. |

#### Usage example

##### Request

```bash
curl -v -X POST \
-H "Authorization: Bearer ${jwt}" \
--data '{
	"config_key": "ssh.insecure_forward_agent",
	"config_value": "host",
	"id": ""
}' \
https://app.scaleft.com/v1/teams/${team_name}/projects/${project_name}/client_config_options```

##### Response
```json
{
	"config_key": "ssh.insecure_forward_agent",
	"config_value": "host",
	"id": "f332114d-38a8-446b-b346-0c58544d8381"
}
```
### Remove a Client Configuration Option from a Project

<ApiOperation method="DELETE" url="https://app.scaleft.com/v1/teams/${team_name}/projects/${project_name}/client_config_options/${client_config_options_id}" />


#### Request path parameters

| Parameter | Type        | Description   |
| --------- | ----------- | ------------- |
| `client_config_options_id`   | string | The UUID of the Client Config Options. |
| `project_name`   | string | The Project name. |
| `team_name`   | string | The name of your Team. |


#### Request query parameters

This endpoint has no query parameters.

#### Request body

This endpoint has no request body.

#### Response body
This endpoint returns a `204 No Content` response on a successful call.


#### Usage example

##### Request

```bash
curl -v -X DELETE \
-H "Authorization: Bearer ${jwt}" \
https://app.scaleft.com/v1/teams/${team_name}/projects/${project_name}/client_config_options/${client_config_options_id}```

##### Response
```json
HTTP 204 No Content
```
### List Cloud Accounts in a Project

<ApiOperation method="GET" url="https://app.scaleft.com/v1/teams/${team_name}/projects/${project_name}/cloud_accounts" />


#### Request path parameters

| Parameter | Type        | Description   |
| --------- | ----------- | ------------- |
| `project_name`   | string | The Project name. |
| `team_name`   | string | The name of your Team. |


#### Request query parameters

This endpoint has no query parameters.

#### Request body

This endpoint has no request body.

#### Response body
This endpoint returns a list of objects with the following fields and a `200` code on a successful call.
| Parameter | Type        | Description          |
|----------|-------------|----------------------|
| `account_id`   | string | The provider-specific account ID. |
| `description`   | string | (optional) Human-readable description of the account. |
| `id`   | string | UUID of the Cloud Account. |
| `provider`   | string | A provider. For now, only accepts `aws` or `gce`, case sensitive. |

#### Usage example

##### Request

```bash
curl -v -X GET \
-H "Authorization: Bearer ${jwt}" \
https://app.scaleft.com/v1/teams/${team_name}/projects/${project_name}/cloud_accounts```

##### Response
```json
{
	"list": [
		{
			"account_id": "123456789012",
			"description": "Dev AWS account",
			"id": "f588c61d-ae92-490d-825a-3b66f92e7444",
			"provider": "aws"
		},
		{
			"account_id": "630225935076",
			"description": "Dev GCE account",
			"id": "ac81534c-eaae-40e4-9478-5ac77ad16bea",
			"provider": "gce"
		}
	]
}
```
### Add a Cloud Account to a Project

<ApiOperation method="POST" url="https://app.scaleft.com/v1/teams/${team_name}/projects/${project_name}/cloud_accounts" />
Adding a Cloud Account to a Project allows servers created in that account to register with Okta Advanced Server Access without using a Server Enrollment Token. This is only possible on cloud providers that expose cryptographically signed instance metadata so this is currently restricted to AWS and GCE.

#### Request path parameters

| Parameter | Type        | Description   |
| --------- | ----------- | ------------- |
| `project_name`   | string | The Project name. |
| `team_name`   | string | The name of your Team. |


#### Request query parameters

This endpoint has no query parameters.

#### Request body

This endpoint has no request body.

#### Response body
This endpoint returns an object with the following fields and a `200` code on a successful call.
| Parameter | Type        | Description          |
|----------|-------------|----------------------|
| `account_id`   | string | The provider-specific account ID. |
| `description`   | string | (optional) Human-readable description of the account. |
| `id`   | string | UUID of the Cloud Account. |
| `provider`   | string | A provider. For now, only accepts `aws` or `gce`, case sensitive. |

#### Usage example

##### Request

```bash
curl -v -X POST \
-H "Authorization: Bearer ${jwt}" \
https://app.scaleft.com/v1/teams/${team_name}/projects/${project_name}/cloud_accounts```

##### Response
```json
{
	"account_id": "123456789012",
	"description": "Dev AWS account",
	"id": "f588c61d-ae92-490d-825a-3b66f92e7444",
	"provider": "aws"
}
```
### Remove a Cloud Account from a Project

<ApiOperation method="DELETE" url="https://app.scaleft.com/v1/teams/${team_name}/projects/${project_name}/cloud_accounts/${cloud_account_id}" />


#### Request path parameters

| Parameter | Type        | Description   |
| --------- | ----------- | ------------- |
| `cloud_account_id`   | string | The UUID of the Cloud Account. |
| `project_name`   | string | The Project name. |
| `team_name`   | string | The name of your Team. |


#### Request query parameters

This endpoint has no query parameters.

#### Request body

This endpoint has no request body.

#### Response body
This endpoint returns a `204 No Content` response on a successful call.


#### Usage example

##### Request

```bash
curl -v -X DELETE \
-H "Authorization: Bearer ${jwt}" \
https://app.scaleft.com/v1/teams/${team_name}/projects/${project_name}/cloud_accounts/${cloud_account_id}```

##### Response
```json
HTTP 204 No Content
```
### List all the ASA Groups in a Project

<ApiOperation method="GET" url="https://app.scaleft.com/v1/teams/${team_name}/projects/${project_name}/groups" />


#### Request path parameters

| Parameter | Type        | Description   |
| --------- | ----------- | ------------- |
| `project_name`   | string | The Project name. |
| `team_name`   | string | The name of your Team. |


#### Request query parameters

This endpoint has no query parameters.

#### Request body

This endpoint has no request body.

#### Response body
This endpoint returns a list of objects with the following fields and a `200` code on a successful call.
| Parameter | Type        | Description          |
|----------|-------------|----------------------|
| `create_server_group`   | boolean | True if you want `sftd` to create a corresponding local (unix or windows) group on the end server. Regardless, Server Users will still be created as long as `create_server_users` is set to true on the Project. |
| `deleted_at`   | string | Time of removal from the Project. Null if not removed. |
| `group_id`   | string | The UUID that corresponds to the ASA Group. |
| `name`   | string | The name of the ASA Group. |
| `server_access`   | boolean | True if members of this ASA Group have access to the Project Servers. |
| `server_admin`   | boolean | True if members of this ASA Group have sudo permissions on the Project Servers. |
| `server_group_name`   | string | If `create_server_group` is true, the name of the server group. |
| `unix_gid`   | integer | If `create_server_group` is true, the GID of the server group created. |

#### Usage example

##### Request

```bash
curl -v -X GET \
-H "Authorization: Bearer ${jwt}" \
https://app.scaleft.com/v1/teams/${team_name}/projects/${project_name}/groups```

##### Response
```json
{
	"list": [
		{
			"create_server_group": true,
			"deleted_at": null,
			"group": "compsons",
			"group_id": "087bc3dd-c9fd-42d1-a21b-e595d1eaf124",
			"name": "compsons",
			"profile_attributes": {
				"unix_gid": 63000,
				"unix_group_name": "sft_compsons",
				"windows_group_name": "sft_compsons"
			},
			"removed_at": null,
			"server_access": false,
			"server_admin": true,
			"server_group_name": null,
			"unix_gid": null
		}
	]
}
```
### Add an ASA Group to a Project

<ApiOperation method="POST" url="https://app.scaleft.com/v1/teams/${team_name}/projects/${project_name}/groups" />
Adds a pre-existing ASA Group to the Project, enabling server access, with either user or admin permissions and the option to sync an ASA Group to the servers in the Project.

#### Request path parameters

| Parameter | Type        | Description   |
| --------- | ----------- | ------------- |
| `project_name`   | string | The Project name. |
| `team_name`   | string | The name of your Team. |


#### Request query parameters

This endpoint has no query parameters.

#### Request body

This endpoint requires an object with the following fields.
| Parameter | Type        | Description          |
|----------|-------------|----------------------|
| `create_server_group`   | boolean | True if you want `sftd` to create a corresponding local (unix or windows) group on the end server. Regardless, Server Users will still be created as long as `create_server_users` is set to true on the Project. |
| `deleted_at`   | string | Time of removal from the Project. Null if not removed. |
| `group_id`   | string | The UUID that corresponds to the ASA Group. |
| `name`   | string | The name of the ASA Group. |
| `server_access`   | boolean | True if members of this ASA Group have access to the Project Servers. |
| `server_admin`   | boolean | True if members of this ASA Group have sudo permissions on the Project Servers. |
| `server_group_name`   | string | If `create_server_group` is true, the name of the server group. |
| `unix_gid`   | integer | If `create_server_group` is true, the GID of the server group created. |

#### Response body
This endpoint returns a `204 No Content` response on a successful call.


#### Usage example

##### Request

```bash
curl -v -X POST \
-H "Authorization: Bearer ${jwt}" \
--data '{
	"create_server_group": true,
	"deleted_at": null,
	"group": "compsons",
	"group_id": "",
	"name": "compsons",
	"removed_at": null,
	"server_access": true,
	"server_admin": false,
	"server_group_name": null,
	"unix_gid": null
}' \
https://app.scaleft.com/v1/teams/${team_name}/projects/${project_name}/groups```

##### Response
```json
HTTP 204 No Content
```
### Retrieve ASA Group details for a single Project

<ApiOperation method="GET" url="https://app.scaleft.com/v1/teams/${team_name}/projects/${project_name}/groups/${group_name}" />
Returns details for an ASA Group on an Project.

#### Request path parameters

| Parameter | Type        | Description   |
| --------- | ----------- | ------------- |
| `group_name`   | string | The ASA Group name. |
| `project_name`   | string | The Project name. |
| `team_name`   | string | The name of your Team. |


#### Request query parameters

This endpoint has no query parameters.

#### Request body

This endpoint has no request body.

#### Response body
This endpoint returns an object with the following fields and a `200` code on a successful call.
| Parameter | Type        | Description          |
|----------|-------------|----------------------|
| `create_server_group`   | boolean | True if you want `sftd` to create a corresponding local (unix or windows) group on the end server. Regardless, Server Users will still be created as long as `create_server_users` is set to true on the Project. |
| `deleted_at`   | string | Time of removal from the project. Null if not removed. |
| `group_id`   | string | The UUID that corresponds to the ASA Group. |
| `name`   | string | The name of the ASA Group. |
| `profile_attributes`   | string | If `create_server_group` is true, the Attributes that will be synced to the server. |
| `server_access`   | boolean | True if members of this ASA Group have access to the Project Servers. |
| `server_admin`   | boolean | True if members of this ASA Group have sudo permissions on the Project Servers. |
| `server_group_name`   | string | If `create_server_group` is true, the name of the server group. |
| `unix_gid`   | integer | If `create_server_group` is true, the GID of the server group created. |

#### Usage example

##### Request

```bash
curl -v -X GET \
-H "Authorization: Bearer ${jwt}" \
https://app.scaleft.com/v1/teams/${team_name}/projects/${project_name}/groups/${group_name}```

##### Response
```json
{
	"create_server_group": true,
	"deleted_at": null,
	"group": "compsons",
	"group_id": "087bc3dd-c9fd-42d1-a21b-e595d1eaf124",
	"name": "compsons",
	"profile_attributes": {
		"unix_gid": 63000,
		"unix_group_name": "sft_compsons",
		"windows_group_name": "sft_compsons"
	},
	"removed_at": null,
	"server_access": false,
	"server_admin": true,
	"server_group_name": null,
	"unix_gid": null
}
```
### Remove an ASA Group from a Project

<ApiOperation method="DELETE" url="https://app.scaleft.com/v1/teams/${team_name}/projects/${project_name}/groups/${group_name}" />


#### Request path parameters

| Parameter | Type        | Description   |
| --------- | ----------- | ------------- |
| `group_name`   | string | The ASA Group name. |
| `project_name`   | string | The Project name. |
| `team_name`   | string | The name of your Team. |


#### Request query parameters

This endpoint has no query parameters.

#### Request body

This endpoint has no request body.

#### Response body
This endpoint returns a `204 No Content` response on a successful call.


#### Usage example

##### Request

```bash
curl -v -X DELETE \
-H "Authorization: Bearer ${jwt}" \
https://app.scaleft.com/v1/teams/${team_name}/projects/${project_name}/groups/${group_name}```

##### Response
```json
HTTP 204 No Content
```
### Change the Project properties of an ASA Project Group

<ApiOperation method="PUT" url="https://app.scaleft.com/v1/teams/${team_name}/projects/${project_name}/groups/${group_name}" />


#### Request path parameters

| Parameter | Type        | Description   |
| --------- | ----------- | ------------- |
| `group_name`   | string | The ASA Group name. |
| `project_name`   | string | The Project name. |
| `team_name`   | string | The name of your Team. |


#### Request query parameters

This endpoint has no query parameters.

#### Request body

This endpoint requires an object with the following fields.
| Parameter | Type        | Description          |
|----------|-------------|----------------------|
| `create_server_group`   | boolean | True if you want `sftd` to create a corresponding local (unix or windows) group on the end server. Regardless, Server Users will still be created as long as `create_server_users` is set to true on the Project. |
| `deleted_at`   | string | Time of removal from the Project. Null if not removed. |
| `group_id`   | string | The UUID that corresponds to the ASA Group. |
| `name`   | string | The name of the ASA Group. |
| `server_access`   | boolean | True if members of this ASA Group have access to the Project Servers. |
| `server_admin`   | boolean | True if members of this ASA Group have sudo permissions on the Project Servers. |
| `server_group_name`   | string | If `create_server_group` is true, the name of the server group. |
| `unix_gid`   | integer | If `create_server_group` is true, the GID of the server group created. |

#### Response body
This endpoint returns a `204 No Content` response on a successful call.


#### Usage example

##### Request

```bash
curl -v -X PUT \
-H "Authorization: Bearer ${jwt}" \
--data '{
	"create_server_group": true,
	"deleted_at": null,
	"group": "compsons",
	"group_id": "",
	"name": "compsons",
	"removed_at": null,
	"server_access": false,
	"server_admin": true,
	"server_group_name": null,
	"unix_gid": null
}' \
https://app.scaleft.com/v1/teams/${team_name}/projects/${project_name}/groups/${group_name}```

##### Response
```json
HTTP 204 No Content
```
### Fetch a Preauthorization

<ApiOperation method="GET" url="https://app.scaleft.com/v1/teams/${team_name}/projects/${project_name}/preauthorizations" />
A Preauthorization is a time-limited grant for an ASA User to access resources in a specific Project.

#### Request path parameters

| Parameter | Type        | Description   |
| --------- | ----------- | ------------- |
| `project_name`   | string | The Project name. |
| `team_name`   | string | The name of your Team. |


#### Request query parameters

This endpoint has no query parameters.

#### Request body

This endpoint has no request body.

#### Response body
This endpoint returns an object with the following fields and a `200` code on a successful call.
| Parameter | Type        | Description          |
|----------|-------------|----------------------|
| `disabled`   | boolean | `true` if the Preauthorization is disabled. |
| `expires_at`   | string | The Preauthorization will cease to work after the `expires_at` date. |
| `id`   | string | The UUID of the Preauthorization. |
| `projects`   | array | The Projects that the Preauthorization is valid for. |
| `servers`   | array | The Servers that the Preauthorization is valid for. |
| `user_name`   | string | The username of the ASA User that the Preauthorization is for. |

#### Usage example

##### Request

```bash
curl -v -X GET \
-H "Authorization: Bearer ${jwt}" \
https://app.scaleft.com/v1/teams/${team_name}/projects/${project_name}/preauthorizations```

##### Response
```json
{
	"disabled": false,
	"expires_at": "2020-07-28T18:30:00Z",
	"id": "566b0fa9-f3ef-4825-a390-16d1766764a0",
	"projects": [
		"the-sound-and-the-fury"
	],
	"servers": null,
	"user_name": "jason.compson"
}
```
### Create a Preauthorization

<ApiOperation method="POST" url="https://app.scaleft.com/v1/teams/${team_name}/projects/${project_name}/preauthorizations" />


#### Request path parameters

| Parameter | Type        | Description   |
| --------- | ----------- | ------------- |
| `project_name`   | string | The Project name. |
| `team_name`   | string | The name of your Team. |


#### Request query parameters

This endpoint has no query parameters.

#### Request body

This endpoint requires an object with the following fields.
| Parameter | Type        | Description          |
|----------|-------------|----------------------|
| `disabled`   | boolean | `true` if the Preauthorization is disabled. |
| `expires_at`   | string | The Preauthorization will cease to work after the `expires_at` date. |
| `id`   | string | The UUID of the Preauthorization. |
| `projects`   | array | The Projects that the Preauthorization is valid for. |
| `servers`   | array | The Servers that the Preauthorization is valid for. |
| `user_name`   | string | The username of the ASA User that the Preauthorization is for. |

#### Response body
This endpoint returns a `204 No Content` response on a successful call.


#### Usage example

##### Request

```bash
curl -v -X POST \
-H "Authorization: Bearer ${jwt}" \
--data '{
	"disabled": false,
	"expires_at": "2020-07-28T18:30:00Z",
	"id": "",
	"projects": [
		"the-sound-and-the-fury"
	],
	"servers": null,
	"user_name": "jason.compson"
}' \
https://app.scaleft.com/v1/teams/${team_name}/projects/${project_name}/preauthorizations```

##### Response
```json
HTTP 204 No Content
```
### Lists the Preauthorizations for a Project

<ApiOperation method="GET" url="https://app.scaleft.com/v1/teams/${team_name}/projects/${project_name}/preauthorizations/${authorization_id}" />


#### Request path parameters

| Parameter | Type        | Description   |
| --------- | ----------- | ------------- |
| `authorization_id`   | string | The UUID of the Authorization. |
| `project_name`   | string | The Project name. |
| `team_name`   | string | The name of your Team. |


#### Request query parameters

| Parameter | Type   | Description |
| --------- | ------------- | -------- |
| `count`   |  integer | (Optional) The number of objects per page. |
| `descending`   |  boolean | (Optional) The object order. |
| `include_expired`   |  boolean | (Optional)  |
| `offset`   |  string | (Optional) The page offset. |
| `prev`   |  boolean | (Optional) The direction of paging. |
| `project`   |  string | (Optional)  |


#### Request body

This endpoint has no request body.

#### Response body
This endpoint returns a list of objects with the following fields and a `200` code on a successful call.
| Parameter | Type        | Description          |
|----------|-------------|----------------------|
| `disabled`   | boolean | `true` if the Preauthorization is disabled. |
| `expires_at`   | string | The Preauthorization will cease to work after the `expires_at` date. |
| `id`   | string | The UUID of the Preauthorization. |
| `projects`   | array | The Projects that the Preauthorization is valid for. |
| `servers`   | array | The Servers that the Preauthorization is valid for. |
| `user_name`   | string | The username of the ASA User that the Preauthorization is for. |

#### Usage example

##### Request

```bash
curl -v -X GET \
-H "Authorization: Bearer ${jwt}" \
https://app.scaleft.com/v1/teams/${team_name}/projects/${project_name}/preauthorizations/${authorization_id}```

##### Response
```json
{
	"list": [
		{
			"disabled": false,
			"expires_at": "2020-07-28T18:30:00Z",
			"id": "566b0fa9-f3ef-4825-a390-16d1766764a0",
			"projects": [
				"the-sound-and-the-fury"
			],
			"servers": null,
			"user_name": "jason.compson"
		}
	]
}
```
### Update a Preauthorization

<ApiOperation method="PUT" url="https://app.scaleft.com/v1/teams/${team_name}/projects/${project_name}/preauthorizations/${authorization_id}" />


#### Request path parameters

| Parameter | Type        | Description   |
| --------- | ----------- | ------------- |
| `authorization_id`   | string | The UUID of the Authorization. |
| `project_name`   | string | The Project name. |
| `team_name`   | string | The name of your Team. |


#### Request query parameters

This endpoint has no query parameters.

#### Request body

This endpoint requires an object with the following fields.
| Parameter | Type        | Description          |
|----------|-------------|----------------------|
| `disabled`   | boolean | `true` if the Preauthorization is disabled. |
| `expires_at`   | string | The Preauthorization will cease to work after the `expires_at` date. |
| `id`   | string | The UUID of the Preauthorization. |
| `projects`   | array | The Projects that the Preauthorization is valid for. |
| `servers`   | array | The Servers that the Preauthorization is valid for. |
| `user_name`   | string | The username of the ASA User that the Preauthorization is for. |

#### Response body
This endpoint returns an object with the following fields and a `200` code on a successful call.
| Parameter | Type        | Description          |
|----------|-------------|----------------------|
| `disabled`   | boolean | `true` if the Preauthorization is disabled. |
| `expires_at`   | string | The Preauthorization will cease to work after the `expires_at` date. |
| `id`   | string | The UUID of the Preauthorization. |
| `projects`   | array | The Projects that the Preauthorization is valid for. |
| `servers`   | array | The Servers that the Preauthorization is valid for. |
| `user_name`   | string | The username of the ASA User that the Preauthorization is for. |

#### Usage example

##### Request

```bash
curl -v -X PUT \
-H "Authorization: Bearer ${jwt}" \
--data '{
	"disabled": true,
	"expires_at": "2020-07-28T18:30:00Z",
	"id": "",
	"projects": [
		"the-sound-and-the-fury"
	],
	"servers": null,
	"user_name": "jason.compson"
}' \
https://app.scaleft.com/v1/teams/${team_name}/projects/${project_name}/preauthorizations/${authorization_id}```

##### Response
```json
{
	"disabled": true,
	"expires_at": "2020-07-28T18:30:00Z",
	"id": "566b0fa9-f3ef-4825-a390-16d1766764a0",
	"projects": [
		"the-sound-and-the-fury"
	],
	"servers": null,
	"user_name": "jason.compson"
}
```
### List Server Enrollment Tokens within a Project

<ApiOperation method="GET" url="https://app.scaleft.com/v1/teams/${team_name}/projects/${project_name}/server_enrollment_tokens" />


#### Request path parameters

| Parameter | Type        | Description   |
| --------- | ----------- | ------------- |
| `project_name`   | string | The Project name. |
| `team_name`   | string | The name of your Team. |


#### Request query parameters

This endpoint has no query parameters.

#### Request body

This endpoint has no request body.

#### Response body
This endpoint returns a list of objects with the following fields and a `200` code on a successful call.
| Parameter | Type        | Description          |
|----------|-------------|----------------------|
| `created_by_user`   | string | The ASA User that created this Server Enrollment Token. |
| `description`   | string | A human-readable description of why this Server Enrollment Token was created. |
| `id`   | string | The UUID that corresponds to the Server Enrollment Token. |
| `issued_at`   | string | Time of creation. |
| `token`   | object | A token used to enroll an ASA Server. |

#### Usage example

##### Request

```bash
curl -v -X GET \
-H "Authorization: Bearer ${jwt}" \
https://app.scaleft.com/v1/teams/${team_name}/projects/${project_name}/server_enrollment_tokens```

##### Response
```json
HTTP 204 No Content
```
### Create a Server Enrollment Token for a Project

<ApiOperation method="POST" url="https://app.scaleft.com/v1/teams/${team_name}/projects/${project_name}/server_enrollment_tokens" />


#### Request path parameters

| Parameter | Type        | Description   |
| --------- | ----------- | ------------- |
| `project_name`   | string | The Project name. |
| `team_name`   | string | The name of your Team. |


#### Request query parameters

This endpoint has no query parameters.

#### Request body

This endpoint requires an object with the following fields.
| Parameter | Type        | Description          |
|----------|-------------|----------------------|
| `created_by_user`   | string | The ASA User that created this Server Enrollment Token. |
| `description`   | string | A human-readable description of why this Server Enrollment Token was created. |
| `id`   | string | The UUID that corresponds to the Server Enrollment Token. |
| `issued_at`   | string | Time of creation. |
| `token`   | object | A token used to enroll an ASA Server. |

#### Response body
This endpoint returns an object with the following fields and a `201` code on a successful call.
| Parameter | Type        | Description          |
|----------|-------------|----------------------|
| `created_by_user`   | string | The ASA User that created this Server Enrollment Token. |
| `description`   | string | A human-readable description of why this Server Enrollment Token was created. |
| `id`   | string | The UUID that corresponds to the Server Enrollment Token. |
| `issued_at`   | string | Time of creation. |
| `token`   | object | A token used to enroll an ASA Server. |

#### Usage example

##### Request

```bash
curl -v -X POST \
-H "Authorization: Bearer ${jwt}" \
https://app.scaleft.com/v1/teams/${team_name}/projects/${project_name}/server_enrollment_tokens```

##### Response
```json
HTTP 204 No Content
```
### Fetch a Server Enrollment Token from a Project

<ApiOperation method="GET" url="https://app.scaleft.com/v1/teams/${team_name}/projects/${project_name}/server_enrollment_tokens/${server_enrollment_token_id}" />


#### Request path parameters

| Parameter | Type        | Description   |
| --------- | ----------- | ------------- |
| `project_name`   | string | The Project name. |
| `server_enrollment_token_id`   | string | The UUID of the Server Enrollment Token. |
| `team_name`   | string | The name of your Team. |


#### Request query parameters

This endpoint has no query parameters.

#### Request body

This endpoint has no request body.

#### Response body
This endpoint returns an object with the following fields and a `200` code on a successful call.
| Parameter | Type        | Description          |
|----------|-------------|----------------------|
| `created_by_user`   | string | The ASA User that created this Server Enrollment Token. |
| `description`   | string | A human-readable description of why this Server Enrollment Token was created. |
| `id`   | string | The UUID that corresponds to the Server Enrollment Token. |
| `issued_at`   | string | Time of creation. |
| `token`   | object | A token used to enroll an ASA Server. |

#### Usage example

##### Request

```bash
curl -v -X GET \
-H "Authorization: Bearer ${jwt}" \
https://app.scaleft.com/v1/teams/${team_name}/projects/${project_name}/server_enrollment_tokens/${server_enrollment_token_id}```

##### Response
```json
HTTP 204 No Content
```
### Delete a Server Enrollment Token from a Project

<ApiOperation method="DELETE" url="https://app.scaleft.com/v1/teams/${team_name}/projects/${project_name}/server_enrollment_tokens/${server_enrollment_token_id}" />


#### Request path parameters

| Parameter | Type        | Description   |
| --------- | ----------- | ------------- |
| `project_name`   | string | The Project name. |
| `server_enrollment_token_id`   | string | The UUID of the Server Enrollment Token. |
| `team_name`   | string | The name of your Team. |


#### Request query parameters

This endpoint has no query parameters.

#### Request body

This endpoint has no request body.

#### Response body
This endpoint returns a `204 No Content` response on a successful call.


#### Usage example

##### Request

```bash
curl -v -X DELETE \
-H "Authorization: Bearer ${jwt}" \
https://app.scaleft.com/v1/teams/${team_name}/projects/${project_name}/server_enrollment_tokens/${server_enrollment_token_id}```

##### Response
```json
HTTP 204 No Content
```
### List Server Users in a Project

<ApiOperation method="GET" url="https://app.scaleft.com/v1/teams/${team_name}/projects/${project_name}/server_users" />
A Server User is a representation of a given ASA User that that will be realized on an end server.

#### Request path parameters

| Parameter | Type        | Description   |
| --------- | ----------- | ------------- |
| `project_name`   | string | The Project name. |
| `team_name`   | string | The name of your Team. |


#### Request query parameters

This endpoint has no query parameters.

#### Request body

This endpoint has no request body.

#### Response body
This endpoint returns a list of objects with the following fields and a `200` code on a successful call.
| Parameter | Type        | Description          |
|----------|-------------|----------------------|
| `admin`   | boolean | True if Server User has sudo permissions. |
| `id`   | string | UUID of Server User API object. |
| `server_user_name`   | string | The username that will be realized on Unix servers. |
| `status`   | string | Status of the Server User. |
| `type`   | string | Whether this is a Service or Human User. |
| `unix_gid`   | integer | Unix GID of the Server User. |
| `unix_uid`   | integer | Unix UID of the Server User. |
| `user_name`   | string | The username of the corresponding ASA User. |
| `windows_server_user_name`   | string | The username that will be realized on Windows servers. |

#### Usage example

##### Request

```bash
curl -v -X GET \
-H "Authorization: Bearer ${jwt}" \
https://app.scaleft.com/v1/teams/${team_name}/projects/${project_name}/server_users```

##### Response
```json
{
	"list": [
		{
			"admin": true,
			"id": "10d678ff-b8ec-42cf-be30-6690c8dc9c9f",
			"server_user_name": "benjy",
			"status": "ACTIVE",
			"type": "human",
			"unix_gid": 63001,
			"unix_uid": 60001,
			"user_name": "benjycompson",
			"windows_server_user_name": "benjy"
		},
		{
			"admin": false,
			"id": "35d0a5bc-0891-4e1d-badb-aae8c94fe455",
			"server_user_name": "quentin",
			"status": "DELETED",
			"type": "human",
			"unix_gid": 63002,
			"unix_uid": 60002,
			"user_name": "quentincompson",
			"windows_server_user_name": "quentin"
		}
	]
}
```
### List Servers in a Project

<ApiOperation method="GET" url="https://app.scaleft.com/v1/teams/${team_name}/projects/${project_name}/servers" />
The Servers enrolled in this Project

#### Request path parameters

| Parameter | Type        | Description   |
| --------- | ----------- | ------------- |
| `project_name`   | string | The Project name. |
| `team_name`   | string | The name of your Team. |


#### Request query parameters

This endpoint has no query parameters.

#### Request body

This endpoint has no request body.

#### Response body
This endpoint returns a list of objects with the following fields and a `200` code on a successful call.
| Parameter | Type        | Description          |
|----------|-------------|----------------------|
| `alt_names`   | array | Any alternative hostnames of the Server. |
| `bastion`   | string | Specifies the bastion-host Clients will automatically use when connecting to this host. |
| `canonical_name`   | string | Specifies the name Clients should use/see when connecting to this host. Overrides the name found with hostname. |
| `cloud_provider`   | string | The cloud provider of the Server, if one exists. |
| `deleted_at`   | string | The time the Server was deleted from the Project. |
| `hostname`   | string | The hostname of the Server. |
| `id`   | string | The UUID corresponding to the Server. |
| `instance_details`   | object | Information the cloud provider provides of the Server, if one exists. |
| `last_seen`   | string | The last time the Server made a request to the ASA platform. |
| `managed`   | boolean | True if the Server is managed by 'sftd'. Unmanaged Servers are used in configurations where users may have a bastion, for example, that they don't want/can't connect to through 'sftd'. With an Unmanaged Server record to represent this box, ASA will know it exists and to use it as a bastion hop. |
| `os`   | string | The particular OS of the Server. |
| `os_type`   | string | Can either be Linux or Windows. |
| `project_name`   | string | The Project that the Server belongs to. |
| `registered_at`   | string | The time the Server was registered to the Project. |
| `services`   | array | Can either be ssh or rdp. |
| `sftd_version`   | string | The version of 'sftd' the Server is running. |
| `ssh_host_keys`   | array | The host keys used to authenticate the Server. |
| `state`   | string | Can be either `ACTIVE` or `INACTIVE`. |
| `team_name`   | string | The name of the Team. |

#### Usage example

##### Request

```bash
curl -v -X GET \
-H "Authorization: Bearer ${jwt}" \
https://app.scaleft.com/v1/teams/${team_name}/projects/${project_name}/servers```

##### Response
```json
{
	"list": [
		{
			"access_address": null,
			"alt_names": null,
			"bastion": null,
			"broker_host_certs": null,
			"canonical_name": null,
			"cloud_provider": null,
			"deleted_at": "0001-01-01T00:00:00Z",
			"hostname": "harvard",
			"id": "48571026-6d34-4463-8ef3-0e6a69a3758c",
			"instance_details": null,
			"last_seen": "0001-01-01T00:00:00Z",
			"managed": true,
			"os": "Ubuntu 16.04",
			"os_type": "linux",
			"project_name": "the-sound-and-the-fury",
			"registered_at": "0001-01-01T00:00:00Z",
			"services": [
				"ssh"
			],
			"sftd_version": "1.44.4",
			"ssh_host_keys": null,
			"state": "INACTIVE",
			"team_name": "william-faulkner"
		},
		{
			"access_address": null,
			"alt_names": null,
			"bastion": null,
			"broker_host_certs": null,
			"canonical_name": null,
			"cloud_provider": null,
			"deleted_at": "0001-01-01T00:00:00Z",
			"hostname": "jefferson",
			"id": "42a9df1d-acaa-4d72-a558-c0f7ea1c34c3",
			"instance_details": null,
			"last_seen": "0001-01-01T00:00:00Z",
			"managed": true,
			"os": "Ubuntu 16.04",
			"os_type": "linux",
			"project_name": "the-sound-and-the-fury",
			"registered_at": "0001-01-01T00:00:00Z",
			"services": [
				"ssh"
			],
			"sftd_version": "1.44.4",
			"ssh_host_keys": null,
			"state": "INACTIVE",
			"team_name": "william-faulkner"
		}
	]
}
```
### Add an Unmanaged Server to a Project

<ApiOperation method="POST" url="https://app.scaleft.com/v1/teams/${team_name}/projects/${project_name}/servers" />
Unmanaged Servers don't use Advanced Server Access for authentication, but still receive Client Configuration Options. Create an Unmanaged Server in order to control the options your team members use to connect to appliances, especially bastions which can't fully utilize Advanced Server Access.

#### Request path parameters

| Parameter | Type        | Description   |
| --------- | ----------- | ------------- |
| `project_name`   | string | The Project name. |
| `team_name`   | string | The name of your Team. |


#### Request query parameters

This endpoint has no query parameters.

#### Request body

This endpoint requires an object with the following fields.
| Parameter | Type        | Description          |
|----------|-------------|----------------------|
| `access_address`   | string | The access address of the Server. |
| `alt_names`   | array | (Optional) Alternative names of the Server. |
| `hostname`   | string | The hostname of the Server. |

#### Response body
This endpoint returns an object with the following fields and a `200` code on a successful call.
| Parameter | Type        | Description          |
|----------|-------------|----------------------|
| `alt_names`   | array | Any alternative hostnames of the Server. |
| `bastion`   | string | Specifies the bastion-host Clients will automatically use when connecting to this host. |
| `canonical_name`   | string | Specifies the name Clients should use/see when connecting to this host. Overrides the name found with hostname. |
| `cloud_provider`   | string | The cloud provider of the Server, if one exists. |
| `deleted_at`   | string | The time the Server was deleted from the Project. |
| `hostname`   | string | The hostname of the Server. |
| `id`   | string | The UUID corresponding to the Server. |
| `instance_details`   | object | Information the cloud provider provides of the Server, if one exists. |
| `last_seen`   | string | The last time the Server made a request to the ASA platform. |
| `managed`   | boolean | True if the Server is managed by 'sftd'. Unmanaged Servers are used in configurations where users may have a bastion, for example, that they don't want/can't connect to through 'sftd'. With an Unmanaged Server record to represent this box, ASA will know it exists and to use it as a bastion hop. |
| `os`   | string | The particular OS of the Server. |
| `os_type`   | string | Can either be Linux or Windows. |
| `project_name`   | string | The Project that the Server belongs to. |
| `registered_at`   | string | The time the Server was registered to the Project. |
| `services`   | array | Can either be ssh or rdp. |
| `sftd_version`   | string | The version of 'sftd' the Server is running. |
| `ssh_host_keys`   | array | The host keys used to authenticate the Server. |
| `state`   | string | Can be either `ACTIVE` or `INACTIVE`. |
| `team_name`   | string | The name of the Team. |

#### Usage example

##### Request

```bash
curl -v -X POST \
-H "Authorization: Bearer ${jwt}" \
--data '{
	"access_address": "1.2.3.4",
	"alt_names": [
		"bastion"
	],
	"hostname": "bastion.dev.com"
}' \
https://app.scaleft.com/v1/teams/${team_name}/projects/${project_name}/servers```

##### Response
```json
{
	"access_address": null,
	"alt_names": null,
	"bastion": null,
	"broker_host_certs": null,
	"canonical_name": null,
	"cloud_provider": null,
	"deleted_at": "0001-01-01T00:00:00Z",
	"hostname": "bastion.dev.com",
	"id": "478a5763-faea-449b-ba3f-40f61ea9e2c5",
	"instance_details": null,
	"last_seen": "0001-01-01T00:00:00Z",
	"managed": false,
	"os": "",
	"os_type": null,
	"project_name": "the-sound-and-the-fury",
	"registered_at": "0001-01-01T00:00:00Z",
	"services": [],
	"sftd_version": null,
	"ssh_host_keys": null,
	"state": "ACTIVE",
	"team_name": "william-faulkner"
}
```
### Get a Server object

<ApiOperation method="GET" url="https://app.scaleft.com/v1/teams/${team_name}/projects/${project_name}/servers/${server_id}" />


#### Request path parameters

| Parameter | Type        | Description   |
| --------- | ----------- | ------------- |
| `project_name`   | string | The Project name. |
| `server_id`   | string | The UUID of the Server. |
| `team_name`   | string | The name of your Team. |


#### Request query parameters

This endpoint has no query parameters.

#### Request body

This endpoint has no request body.

#### Response body
This endpoint returns an object with the following fields and a `200` code on a successful call.
| Parameter | Type        | Description          |
|----------|-------------|----------------------|
| `alt_names`   | array | Any alternative hostnames of the Server. |
| `bastion`   | string | Specifies the bastion-host Clients will automatically use when connecting to this host. |
| `canonical_name`   | string | Specifies the name Clients should use/see when connecting to this host. Overrides the name found with hostname. |
| `cloud_provider`   | string | The cloud provider of the Server, if one exists. |
| `deleted_at`   | string | The time the Server was deleted from the Project. |
| `hostname`   | string | The hostname of the Server. |
| `id`   | string | The UUID corresponding to the Server. |
| `instance_details`   | object | Information the cloud provider provides of the Server, if one exists. |
| `last_seen`   | string | The last time the Server made a request to the ASA platform. |
| `managed`   | boolean | True if the Server is managed by 'sftd'. Unmanaged Servers are used in configurations where users may have a bastion, for example, that they don't want/can't connect to through 'sftd'. With an Unmanaged Server record to represent this box, ASA will know it exists and to use it as a bastion hop. |
| `os`   | string | The particular OS of the Server. |
| `os_type`   | string | Can either be Linux or Windows. |
| `project_name`   | string | The Project that the Server belongs to. |
| `registered_at`   | string | The time the Server was registered to the Project. |
| `services`   | array | Can either be ssh or rdp. |
| `sftd_version`   | string | The version of 'sftd' the Server is running. |
| `ssh_host_keys`   | array | The host keys used to authenticate the Server. |
| `state`   | string | Can be either `ACTIVE` or `INACTIVE`. |
| `team_name`   | string | The name of the Team. |

#### Usage example

##### Request

```bash
curl -v -X GET \
-H "Authorization: Bearer ${jwt}" \
https://app.scaleft.com/v1/teams/${team_name}/projects/${project_name}/servers/${server_id}```

##### Response
```json
{
	"access_address": null,
	"alt_names": null,
	"bastion": null,
	"broker_host_certs": null,
	"canonical_name": null,
	"cloud_provider": null,
	"deleted_at": "0001-01-01T00:00:00Z",
	"hostname": "harvard",
	"id": "48571026-6d34-4463-8ef3-0e6a69a3758c",
	"instance_details": null,
	"last_seen": "0001-01-01T00:00:00Z",
	"managed": true,
	"os": "Ubuntu 16.04",
	"os_type": "linux",
	"project_name": "the-sound-and-the-fury",
	"registered_at": "0001-01-01T00:00:00Z",
	"services": [
		"ssh"
	],
	"sftd_version": "1.44.4",
	"ssh_host_keys": null,
	"state": "INACTIVE",
	"team_name": "william-faulkner"
}
```
### Remove a Server from a Project

<ApiOperation method="DELETE" url="https://app.scaleft.com/v1/teams/${team_name}/projects/${project_name}/servers/${server_id}" />


#### Request path parameters

| Parameter | Type        | Description   |
| --------- | ----------- | ------------- |
| `project_name`   | string | The Project name. |
| `server_id`   | string | The UUID of the Server. |
| `team_name`   | string | The name of your Team. |


#### Request query parameters

This endpoint has no query parameters.

#### Request body

This endpoint has no request body.

#### Response body
This endpoint returns a `204 No Content` response on a successful call.


#### Usage example

##### Request

```bash
curl -v -X DELETE \
-H "Authorization: Bearer ${jwt}" \
https://app.scaleft.com/v1/teams/${team_name}/projects/${project_name}/servers/${server_id}```

##### Response
```json
HTTP 204 No Content
```

