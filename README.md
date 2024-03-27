# Ansible Automation Platform Configuration as a Code

### Required variables to run playbook
| Variable                                   |  Type  | Description                                             | Mandatory |
|:-------------------------------------------|:------:|:--------------------------------------------------------|:---------:|
| group                                      | STRING | Available option: staging and production                |    YES    |
| org_name                                   | STRING | Organization name                                       |    YES    |
| org_description                            | STRING | Organization information                                |    NO     |
| org_galaxy_credentials                     |  LIST  | List of Private Hubs and community galaxy               |    YES    |
| credential_types                           |  LIST  | Credential types, example: Source Control, Machine etc. |    YES    |
| source_control_name                        | STRING | Source Control credential name                          |    YES    |
| source_control_description                 | STRING | Source Control credential information                   |    NO     |
| source_control_username                    | STRING | Source Control credential username                      |    YES    |
| source_control_password                    | STRING | Source Control credential password                      |    YES    | 
| machine_credential_name                    | STRING | Machine Credential name                                 |    YES    | 
| machine_credentials_description            | STRING | Machine Credential information                          |    NO     | 
| machine_credential_username                | STRING | Machine Credential username                             |    YES    | 
| machine_credential_password                | STRING | Machine Credential password                             |    NO     | 
| machine_credentials_private_key            | STRING | Machine Credential ssh private key                      |    YES    | 
| machine_credentials_private_key_passphrase | STRING | Machine Credential ssh private key passphrase           |    NO     | 
| machine_credentials_become_method          | STRING | Machine Credential become method                        |    NO     | 
| machine_credentials_become_username        | STRING | Machine Credential become user                          |    NO     | 
| machine_credentials_become_password        | STRING | Machine Credential become password                      |    NO     |

### Execution
> [!NOTE] 
> All sensitive data like passwords etc., provide as vault encrypted!!!
> Playbook is fully ready to use with AAP to run as Template or Workflow template and don't need any modification.
> All variable may be provided via Template or Workflow Survey, or as variables

- Variables input.yaml
```yaml
group: staging
org_name: ACME
org_description: 'ACME Inc.'
org_gaglaxy_credentials:
  - List 1
  - List 2
  - List 3
credential_types:
  - 'Source Control'
  - 'Machine'
source_control_name: 'git'
source_control_description: 'gitlab demo'
source_control_username: 'demouser'
source_control_password: 'demopass'
machine_credential_name: 'demo'
machine_credentials_description: 'demo key'
machine_credential_username: 'aap'
machine_credential_password:
machine_credentials_private_key:
  -----BEGIN PRIVATE KEY-----
  -----END PRIVATE KEY-----
machine_credentials_private_key_passphrase:
machine_credentials_become_method: 'sudo'
machine_credentials_become_username: 'root'
machine_credentials_become_password:
```
- Run
```yaml
# add below lines into caac.yml
vars_files:
  - input.yml

# run
ansible-playbook caac.yaml --ask-vault-password
```

