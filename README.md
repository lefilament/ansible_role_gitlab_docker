docker_gitlab
==============

This role deploys GitLab on Docker
The main repo for this role is on [Le Filament GitLab](https://sources.le-filament.com/lefilament/ansible-roles/docker_gitlab.git)

Requirements
------------

None

Role Variables
--------------

Variables from default directory :
* domain: domain belonging to customer
* git_url: URL on which GitLab will be listening
* Mail configuration :
  * real_mailserver: Whether to authorize e-mail from GitLab or not (if set to true - by default, the following variables need to be defined, otherwise a mailhog instance will be deployed for blocking e-mails)
  * mailserver: SMTP server to use for sending e-mails (defaults to smtp.{{ domain }})
  * smtpport: SMTP server port (defaults to 465)
  * smtpuser: SMTP username (defaults to smtpuser)
  * smtppass: SMTP user password (defaults to veryUnsecurePassToBeModified)
  * git_mail_from: from address used in e-mail sent from GitLab (defaults to git@{{ domain }})
* SSO integration :
  * enable_omniauth: whether or not configure SSO integration (defaults to false)
  * sso_url: URL for SSO server
  * sso_oidc_gitlab_id: OpenID connect identifier defined for gitlab
  * sso_oidc_gitlab_secret: OpenID connect secret defined for gitlab
* Backups (for backups to be deployed, host needs to be in maintenance_contract group) :
  * swift parameters for 2 object storage instances where backups should be pushed daily
  * git_backup_pass : Passphrase for encryption of backups


Dependencies
------------

This role requires the following Ansible collection :
* community.docker

This Docker role supposes that Traefik is deployed as an inverseproxy in front of the deployed Dockers.
The following role is used by Le Filament for deploying Traefik : docker_server (https://sources.le-filament.com/lefilament/ansible-roles/docker_server)

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: docker_gitlab }
      vars:
         - { domain: "example.org" }
         - { git_url: "git.example.org" }
         - { real_mailserver: false }
         - { enable_omniauth: false }

License
-------

AGPL-3

Author Information
------------------

Le Filament (https://le-filament.com)
