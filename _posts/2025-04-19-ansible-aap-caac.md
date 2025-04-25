# CONFIGURATION AS CODE

## Logical concept

***Configuration as code*** is defined as the practice of managing application configuration files in a repository. In the case of Ansible Automation Platform, these configuration files establish the settings we wish to apply across our Ansible Automation Platform environments.

While ***configuration as code* **provides numerous benefits and best practices that can be applied across an Ansible Automation Platform environment, in order to streamline and automate the delivery of the
configurations to multiple Ansible Automation Platform sites automatically, immediately and consistently, it must be pair with configuration as code solution with Git webhooks.

***Git webhooks*** are defined as a method for notifications to be delivered to an external web server whenever certain actions occur on a repository or organization.
With the solution of configuration as code and Git webhooks, one can setup a Ansible Automation Platform workflow that immediately updates all of Ansible Automation Platform sites simultaneously with the exact configurations across all the platforms.

The Admin/user updates the configuration details of AAP on the GitLab repository. After approval via merge request, the updated repository triggers a web hook event to sync with the AAP controllers projects. The AAP then configures the updated details on the controller based on the sync changes.

![casc workflow](Repo_images/AAP2_flow.jpg)

## How to implement CaaC

To best implement the CaaC we have considered provider-consumer model. you may correlatate this with Hub-Spoke model, where all the core functionality is with the cetralized provider/Hub and consumers/Spoke serve the limited features with reference to Provider.

This approach will include a **central playbook** (Provider_Org repo) which will be used to make changes to automation controller, though the actual configuration will be stored in separate repositories(caac Consumer_Orgs repo) to allow for separation of concerns between different organizations

This way we are able to build in separation of duties where the automation controller owners/Admin can set out CaaC mechanisms but allow the other organizations to make use of them.

**CaaC structure**

1. Git project to host CaaC Provider_Org and Consumer_Orgs repos.
2. Ansible automation platoform (AAP) to host provider and consumer organizations.
3. Ansible CLI for initial Provider_Org setup


![caac physical design](Repo_images/caac_physical_design.jpg)

1. Gitlab project shall host all the CaaC repo for provider and Consumer Orgs
2. CaaC main collection shall be part of Provider_org repo and mapped with provider_org project.
3. Config files to enable new org CaaC automation shall be updated in provider_org **host_vars** 
4. Consumer_Orgs specific files should be created/added in host_vars of Consumer_orgs repo.
5. **Automate the Automation**- Inital provider_Org shall be created with the help of Ansible CLI (current approch).
6. Any new consumer org base automation of landing zone shall be created with provider_org job template.
7. All the Consumer_org specific requirement like creating new project inventory shall be triggered through consumer specific job template.

## Description of **Provider_Org** repository

This is the master repository(collection) which centrally manage and enable ***Configuration as code*** for teams/organizations hosted on ansible automation platform 2.1 and above.

**Provider_Org Repository structure** :-

The repository's directory structure includes the following elements: **roles, host_vars,collections/Requirement.yml, controller_config.yml, inventory for controller**.

```python
    CAC_AAP_REPO
    ├── playbooks
    │    └── plays4_controller
    │        ├── collections
    │        ├── host_vars
    │        │   ├── config_Provider_Org_dev
    │        │   └── config_Provider_Org_prod
    │        └── roles
    │        │     └── controller_config
    │        ├── inv_Provider_Org_dev
    │        ├── inv_Provider_Org_prod
    │        └── controller_config.yml
    ├── Repo_images
    └── README.MD

     
```

1. **roles Directory**
    These are imported roles from redhat official colection (<https://github.com/redhat-cop/controller_configuration>) for AAP controller, specifically curated as per our requirement.changes are highlighted in role specific readme whereever is applicable.

    ```python
    **roles**
    └── **controller_config****
        ├── ad_hoc_command_cancel
        ├── applications
        ├── credential_input_sources
        ├── credential_types
        ├── credentials
        ├── dispatch
        ├── execution_environments
        ├── filetree_create
        ├── filetree_read
        ├── groups
        ├── hosts
        ├── instance_groups
        ├── instances
        ├── inventories
        ├── inventory_source_updates
        ├── inventory_sources
        ├── job_launch
        ├── job_templates
        ├── jobs_cancel
        ├── labels
        ├── license
        ├── notification_templates
        ├── object_diff
        ├── organizations
        ├── project_update
        ├── projects
        ├── roles
        ├── schedules
        ├── settings
        ├── teams
        ├── users
        ├── workflow_job_templates
        └── workflow_launch

    ```  

    In the roles directory, we have defined the controller_config-related roles that encompass a comprehensive configuration for the AAP controller config and its specification, which can be easily managed using these roles.

    Each role contains detailed information about tasks, defaults, vars, etc., with a primary focus on the tasks file that contains the source task of the role. there are test example that can be refered for future use.

2. **Project Inventory file**
    to pass the org specifc variables to aap controller, a project inventory is defined to stadardize the cosumption.
    
    ```python
        CAC_AAP_REPO
        ├── playbooks
            └── plays4_controller
                ├── inv_Provider_Org_prod
                └── inv_Provider_Org_dev

    ``` 
    inventory files are created for each AAP environment. Each file has dummy controller hostname as per naming convention.***config_your org name_aap env_type***
    **Example ** config_Provider_Org_prod. 
    
    ***make sure directory under host_vars is created with same name as hostname else host vars specific to inventory wont be read.***

    content of inventory file
    ```
        config_Provider_Org_prod    ansible_connection=local**
    ```
3. **host_vars Provider_Org Directory**
   
    Inside the **host_vars**, two sub directories are created to mange prod and dev AAP controller environment. under environment directories role specifc config files are defined. data of these files will be used by project inventory source.

    ```python
    host_vars
    ├── config_Provider_Org_dev
    │   └── example.yml
    └── config_Provider_Org_prod
        ├── controller_ad_hoc_commands.yml
        ├── controller_ad_hoc_commands_cancel.yml
        ├── controller_applications.yml
        ├── controller_auth.yml
        ├── controller_cancel_jobs.yml
        ├── controller_configuration_dispatcher_roles.yml
        ├── controller_credential_input_sources.yml
        ├── controller_credential_types.yml
        ├── controller_credentials.yml
        ├── controller_execution_environments.yml
        ├── controller_hosts.yml
        ├── controller_instance_groups.yml
        ├── controller_instances.yml
        ├── controller_inventories.yml
        ├── controller_inventory_sources.yml
        ├── controller_job_templates.yml
        ├── controller_labels.yml
        ├── controller_launch_jobs.yml
        ├── controller_notifications.yml
        ├── controller_organizations.yml
        ├── controller_project_updates.yml
        ├── controller_projects.yml
        ├── controller_roles.yml
        ├── controller_schedules.yml
        ├── controller_settings.yml
        ├── controller_teams.yml
        ├── controller_user_accounts.yml
        ├── controller_vault.yml
        ├── controller_workflow_launch_jobs.yml
        └── controller_workflows.yml
    ```  
4.  **Controller_config.yml**
   This is the main.yml file and will be used to for cental automation and creation of caac for Provider_Org and other consumer orgs.
   

## Description of **Consumer_Orgs** repository

The consumer org repository is abstracted version of Provider_Org. the main purpose of this repository is to host org/team specific variables or requirement files. Thus assure, Consumer_Orgs has freedom to request the aap resources without impacting the core functionality of cenralize automation codebase hosted in Provider_Org repo.

```python
shared_org_cac_aap_repo
├── README.md
└── config_files
    ├── host_vars
    │   ├── config_shared_org_dev
    │   └── config_shared_org_prod
    │       ├── controller_credential_types.yml
    │       └── controller_projects.yml
    ├── inv_shared_org_dev
    └── inv_shared_org_prod
```

## How to request and provision AAP resources using CaaC

### Request flow- Initial setup for Provider_Org

In scenario where you have just downloaded our CaaC collection repo use this flow to create your first Provider_org. This would be centralize place from where landing zones for new Consumer orgs will be created. Also, make sure Consumer orgs refer to provider_org project for CaaC code execution  

![Initial CLI config](Repo_images/Provider_Org_cli_provisioned.jpg)

```python

## CLI command to create resources for your first organzarion (provider_org)
ansible-playbook controller_config.yml -i inv_provider_org_prod -e "controller_username='your_username' controller_password='your_password'" --ask-vault-pass --tags  settings,organizations,projects,users,inventories,inventory_sources,credential_types,credentials,job_templates

```

### Request flow- CaaC enabler for Consumer_Orgs

This flow will help you to create resources required to enable CaaC automation for any new Consumer Org.

![new consumer org](Repo_images/request_flow4_new_consumer_org.jpg)

### Request flow- AAP resources from within Consumer_Orgs

This flow will help you to create resources within Consumer orgs using CaaC automation.

![consumer org](Repo_images/request_flow4_resources_within_consumer_org.jpg)

# Branch strategy

**master branch** - This branch is an main branch for ***All the Environment*** Environment.

**develop branch** - This branch is an fetcher branch of master branch and used for ***new resource request/feature*** Environment. Merging updates happens on further develop branch to master branch.

**Note** - Make sure that **master** branch is maintained by promising *Administrator*.

# Pre-requisites

* A user with **root** privileges needs to integrate the AAP controller with the GitLab repository.

* To perform the configuration as a code the mandatory Ansible collection is ***awx.awx***

* To manage the playbook over the AAP controller it requires a **project** to config over the gitlab repo, a **job template** to config webhooks
      with integration of gitlab repo and a **vault credential** to encrypt the vault data.

* The controller CIL uses the **REST API** to create the mandatory fields, eliminating the need for manual creation.
