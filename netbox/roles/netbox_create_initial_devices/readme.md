# Netbox

**NOTE**:
This role is intended to be idempotent which means it is used for initial provisioning.
For this reason it should skip anything that is already created. For updating already existing
objects use `netbox_update_*` roles or make adjustments manually in netbox.

**NOTE**:
This role was created from scratch It still needs to properly be verified and documented.




## Parameters

- value                                     : for a value

The variable `value` is passed through 'extra vars' and used to create an object.

The variable `variable` is generated in this role and creates a standard name for an object.

## Usage

We call this role in the playbook `pb_netbox_create_initial_config` like this:

```yaml
- include_role:
    name: netbox_create_initial_devices
```

The playbook `pb_netbox_create_initial_devices` should be called with a provisioning file parsed
through extra_vars when calling the playbook

```bash
ansible-playbook pb_netbox_create_initial_config.yml -i ./inventory/development/hosts --extra-\
vars"file_preamble=unique_name"
```

```text
───provision_data
    ├───{{file_preamble}}_initial_organization.yml
    ├───{{file_preamble}}_initial_devices.yml
    ├───{{file_preamble}}_initial_ipam.yml
    └───{{file_preamble}}_initial_extra.yml
```

## Dependencies

- [collection] netbox.netbox
