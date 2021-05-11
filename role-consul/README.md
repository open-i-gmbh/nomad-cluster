Role Name
=========

This Role is used to provision consul cluster

Requirements
------------

The Vms to be up and running

Role Variables
--------------

Default Vars:

consul_version: 1.9.0  ## Should be the Consul latest stable Version
consul_webui_version: 1.9.0  ## Webui latest stable Version

consul_server: true  ## It istall all agent as servers by default
consul_client: false  ## Same as the last one and that is overwriten in the vars dir for the client servers.
consul_webui: true  ## It install the webui by defaut


Vars:

consul_url: https://releases.hashicorp.com/consul/{{ consul_version }}/consul_{{ consul_version }}_linux_amd64.zip

consul_webui_url: https://releases.hashicorp.com/consul/{{ consul_webui_version }}/consul_{{
consul_webui_version }}_web_ui.zip

consul_download_dir: /tmp

consul_install_dir: /usr/bin

consul_config_dir: /var/lib/consul/conf

consul_data_dir: /var/lib/consul

consul_webui_install_dir: /opt/consul-webui

consul_user: root  ## Use root to bind to port 53

consul_group: root

consul_service_name: consul   ## The systemd service name for consul

consul_ui_dir: "{{ consul_webui_install_dir }}/dist"
