# Dynatrace-Tomcat-Agent-Ansible

An [Ansible](http://www.ansible.com) role for automated deployments of the [Dynatrace](http://www.bit.ly/dttrial) Java Agent for Apache Tomcat.

This role makes the Java Agent available to Apache Tomcat by injecting an *-agentpath* option into the ```CATALINA_OPTS``` (or any other) environment variable in a file (typically an executable script). It is assumed that this script either executes Tomcat directly or is sourced by another script before Tomcat is executed.

**Note**: Currently, we support only Linux hosts, support for installing Windows hosts is in the making.

## Download

The role is available via:

- [Ansible Galaxy](https://galaxy.ansible.com/list#/roles/2654)
- [GitHub](https://github.com/Dynatrace/Dynatrace-Tomcat-Agent-Ansible)

## Requirements

This roles requires an installation of the Dynatrace Java Agents package, which is provided by the following roles:

- [Dynatrace-Agents](https://galaxy.ansible.com/list#/roles/2620)
- [Dynatrace-Server](https://galaxy.ansible.com/list#/roles/2623)

## Role Variables

As defined in ```defaults/main.yml```:

| Name                                        | Default                                  | Description |
|---------------------------------------------|------------------------------------------|-------------|
| *dynatrace_tomcat_agent_env_var_name*       | CATALINA_OPTS                            | The name of the environment variable to be used for Agent injection. |
| **dynatrace_tomcat_agent_env_var_file_name** |                                         | The name of the file to be modified. |
| *dynatrace_tomcat_agent_name*               | apache-tomcat-agent                      | The name of the Java Agent as it appears in Dynatrace. |
| *dynatrace_tomcat_agent_collector_hostname* | localhost                                | The location of the collector the Agent shall connect to. |
| *dynatrace_tomcat_agent_collector_port*     | 9998                                     | The port on the collector the Agent shall connect to. |
| *dynatrace_tomcat_agent_linux_agent_path*   | /opt/dynatrace/agent/lib64/libdtagent.so | The path to the Agent libary. |

## Example Playbook

	- hosts: all
	  roles:
	    - { role: Dynatrace-Agents }
	    - { role: Dynatrace-Tomcat-Agent, dynatrace_tomcat_agent_env_var_file_name: /opt/tomcat/bin/catalina.sh }

## Additional Resources

- [Slide Deck: Automated Deployments](http://slideshare.net/MartinEtmajer/automated-deployments-slide-share)
- [Slide Deck: Introduction to Automated Deployments with Ansible](http://www.slideshare.net/MartinEtmajer/introduction-to-automated-deployments-with-ansible)

## Questions?

Feel free to post your questions on the Dynatrace Community's [Continuous Delivery Forum](https://community.dynatrace.com/community/pages/viewpage.action?pageId=46628921).

## License

Licensed under the MIT License. See the LICENSE file for details.
