## ansible sonatype nexus-oss Role
[![Build Status](https://travis-ci.org/ahelal/ansible-sonatype_nexus.svg)](https://travis-ci.org/ahelal/ansible-sonatype_nexus)


### Role variables

List of default variables available in the inventory:

```yaml
## Nexus Setup Setting Section
nexus_host               : "{{ansible_fqdn}}"
nexus_version            : "2.7.1"
nexus_download_URL       : "http://download.sonatype.com/nexus/oss/{{nexus_archive}}"
### Jetty
jetty_bind               : "0.0.0.0"
jetty_port               : "8081"
nexus_url                : "http://{{nexus_host}}:{{jetty_port}}"
### Nexus system user
nexus_user               : nexus
nexus_group              : nexus
nexus_home               : "/home/{{nexus_user}}"
### Directory & files
nexus_service_name       : "nexus"     ## Think twice before changing it :)
nexus_service_desc       : "nexusOSS"
nexus_sonatype_work_name : "sonatype-work"
nexus_dir_base           : "{{nexus_home}}"
nexus_dir_base_bundle    : "{{nexus_home}}/{{nexus_service_name}}"
nexus_dir_sonatype_work  : "{{nexus_dir_base}}/{{nexus_sonatype_work_name}}"
nexus_dir_plugins        : "{{nexus_dir_base_bundle}}/nexus/WEB-INF/plugin-repository"
nexus_dir_tmp            : "/tmp" # or override with "{{ tempdir.stdout }} in order to have be sure to download the file"
nexus_archive            : "nexus-{{nexus_version}}-bundle.tar.gz"

## Nexus Plugins Section
### p2 plugins
nexus_plugins_install            : False
nexus_plugins_p2_version         : "2.8.1-m1"
nexus_plugins_p2_url             : 'https://repository.sonatype.org/service/local/repositories/nexus_oss-1069/content/org/sonatype/nexus/plugins'
nexus_plugins_p2_dir             : "nexus-p2-repository-plugin/{{nexus_plugins_p2_version}}" 
nexus_plugins_p2_file            : "nexus-p2-repository-plugin-{{nexus_plugins_p2_version}}-bundle.zip"
nexus_plugins_p2_bridge_dir      : "nexus-p2-bridge-plugin/{{nexus_plugins_p2_version}}" 
nexus_plugins_p2_bridge_file     : "nexus-p2-bridge-plugin-{{nexus_plugins_p2_version}}-bundle.zip"
### Array of plugins to be installed
nexus_plugins:
   - url  : "{{nexus_plugins_p2_url}}/{{nexus_plugins_p2_dir}}/"
     file : "{{nexus_plugins_p2_file}}"

   - url  : "{{nexus_plugins_p2_url}}/{{nexus_plugins_p2_bridge_dir}}/"
     file : "{{nexus_plugins_p2_bridge_file}}"

## Nexus Setting Section
### Global Setting
nexus_globalConnectionSettings_connectionTimeout      : 40000
nexus_globalConnectionSettings_retrievalRetryCount    : 10
### Rest API
nexus_restApi_baseUrl                                 : "{{nexus_url}}/nexus"
nexus_restApi_forceBaseUrl                            : "true"
nexus_restApi_uiTimeout                               : "120000"
### http Proxy
nexus_httpProxy_enabled                               : "true"
nexus_httpProxy_port                                  : 8082
nexus_httpProxy_proxyPolicy                           : "strict"
### Routing
nexus_routing_resolveLinks                            : "true"

### smtp
nexus_smtpConfiguration_hostname                      : locahost
nexus_smtpConfiguration_port                          : 25
nexus_smtpConfiguration_username                      : ""
nexus_smtpConfiguration_password                      : ""
nexus_smtpConfiguration_systemEmailAddress            : "system@nexus.org"

```
