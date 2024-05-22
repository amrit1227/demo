```markdown
# Auth0 Connections Module

## Overview

This Terraform module creates and manages Auth0 connections and their associations with an Auth0 organization. The module supports a variety of connection options, including password policies, brute force protection, and multi-factor authentication (MFA).

## Usage

```hcl
module "auth0_connections" {
  source = "./path/to/this/module"

  organization_name = "your-organization"
  organization_id   = "your-organization-id"
  connections = [
    {
      name                       = "connection1"
      strategy                   = "auth0"
      is_domain_connection       = false
      assign_membership_on_login = false
      metadata                   = { key1 = "value1" }
      realms                     = ["realm1"]
      options = {
        password_policy               = "excellent"
        brute_force_protection        = true
        enabled_database_customization = false
        requires_username             = true
        disable_signup                = true
        import_mode                   = false
        custom_scripts                = { script1 = "value1" }
        password_history              = { enable = true, size = 5 }
        password_no_personal_info     = { enable = true }
        password_dictionary           = { enable = true, dictionary = ["word1", "word2"] }
        password_complexity_options   = { min_length = 10 }
        validation                    = { username = { min = 10, max = 40 } }
        mfa                           = { active = true, return_enroll_settings = true }
      }
    }
  ]
}
```

## Variables

| Name                                           | Type   | Description                                                    | Default          |
|------------------------------------------------|--------|----------------------------------------------------------------|------------------|
| `organization_name`                            | string | The name of the organization                                   |                  |
| `organization_id`                              | string | The ID of the organization                                     |                  |
| `connections`                                  | list   | A list of connection objects. Each object contains:            |                  |
| `connections.name`                             | string | The name of the connection                                     |                  |
| `connections.strategy`                         | string | The strategy used by the connection (e.g., "auth0")            |                  |
| `connections.is_domain_connection`             | bool   | Whether the connection is a domain connection                  | `false`          |
| `connections.assign_membership_on_login`       | bool   | Whether to assign membership on login                          | `false`          |
| `connections.metadata`                         | map    | Metadata for the connection                                    | `{}`             |
| `connections.realms`                           | list   | List of realms for the connection                              | `[]`             |
| `connections.options`                          | object | Configuration options for the connection, including:           | `{}`             |
| `connections.options.password_policy`          | string | The password policy                                            | `"excellent"`    |
| `connections.options.brute_force_protection`   | bool   | Whether to enable brute force protection                       | `true`           |
| `connections.options.enabled_database_customization`| bool | Whether to enable database customization                    | `false`          |
| `connections.options.requires_username`        | bool   | Whether a username is required                                 | `true`           |
| `connections.options.disable_signup`           | bool   | Whether to disable signup                                      | `true`           |
| `connections.options.import_mode`              | bool   | Whether to enable import mode                                  | `false`          |
| `connections.options.custom_scripts`           | map    | Custom scripts for the connection                              | `{}`             |
| `connections.options.password_history`         | object | Password history settings, including:                          | `{}`             |
| `connections.options.password_history.enable`  | bool   | Whether to enable password history                             | `true`           |
| `connections.options.password_history.size`    | number | The size of the password history                               | `5`              |
| `connections.options.password_no_personal_info`| object | Password no personal info settings, including:                 | `{}`             |
| `connections.options.password_no_personal_info.enable`| bool | Whether to enable password no personal info                | `true`           |
| `connections.options.password_dictionary`      | object | Password dictionary settings, including:                       | `{}`             |
| `connections.options.password_dictionary.enable`| bool   | Whether to enable password dictionary                          | `true`           |
| `connections.options.password_dictionary.dictionary`| list | The list of words for the password dictionary              | `[]`             |
| `connections.options.password_complexity_options`| object| Password complexity options, including:                        | `{}`             |
| `connections.options.password_complexity_options.min_length`| number | The minimum length for passwords                      | `10`             |
| `connections.options.validation`               | object | Validation settings, including:                                | `{}`             |
| `connections.options.validation.username`      | object | Username validation settings, including:                       | `{}`             |
| `connections.options.validation.username.min`  | number | The minimum length for usernames                               | `10`             |
| `connections.options.validation.username.max`  | number | The maximum length for usernames                               | `40`             |
| `connections.options.mfa`                      | object | Multi-factor authentication settings, including:               | `{}`             |
| `connections.options.mfa.active`               | bool   | Whether to activate MFA                                        | `true`           |
| `connections.options.mfa.return_enroll_settings`| bool   | Whether to return enroll settings for MFA                      | `true`           |

## Outputs

| Name                            | Description                                      |
|---------------------------------|--------------------------------------------------|
| `connection_ids`                | A map of Auth0 connection IDs                    |
| `organization_connections_ids`  | A map of Auth0 organization connection details, including connection IDs and the `assign_membership_on_login` flag |

## Providers

- `auth0`: This module requires the Auth0 provider.

## Example

To use this module, include it in your Terraform configuration as shown in the usage example above. Customize the `connections` variable to define the connections needed for your Auth0 organization.

## License

This module is open source and available under the MIT License.
```

Simply place this content in your `README.md` file in your GitHub repository.
