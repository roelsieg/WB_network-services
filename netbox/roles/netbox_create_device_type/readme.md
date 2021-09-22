# Netbox

**NOTE**:
This role was created from scratch It still needs to properly be verified and documented.


## Parameters

- value                                     : for a value

The variable `value` is passed through 'extra vars' and used to create an object.

The variable `variable` is generated in this role and creates a standard name for an object.

## Usage

```yaml
- include_role:
    name: netbox_create_device_type
  loop: "{{ device_types }}"
  loop_control:
    loop_var: dt
```

## Dependencies

- [collection] netbox.netbox
