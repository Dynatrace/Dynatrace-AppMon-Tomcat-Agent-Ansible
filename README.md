# Dynatrace-Tomcat-Agent-Ansible

An [Ansible](http://www.ansible.com) role for automated deployments of the [Dynatrace](http://www.bit.ly/dttrial) Java Agent for Apache Tomcat.

This role makes the Java Agent available to Apache Tomcat by injecting an *-agentpath* option into the ```CATALINA_OPTS``` (or any other) environment variable in a file (typically an executable script). It is assumed that this script either executes Tomcat directly or is sourced by another script before Tomcat is executed. Please note that this role might need some tweaking to fit your particular use-case. **You will have to restart your application after placing the agent.**

## Download

The role is available via:

- [Ansible Galaxy](https://galaxy.ansible.com/list#/roles/2654)
- [GitHub](https://github.com/Dynatrace/Dynatrace-Tomcat-Agent-Ansible)

## Dependencies

This roles depends on the following roles:

- [Dynatrace-Java-Agent](https://galaxy.ansible.com/list#/roles/2653)

## Role Variables

As defined in ```defaults/main.yml```:

| Name                                               | Default                                  | Description |
|----------------------------------------------------|------------------------------------------|-------------|
| *dynatrace_tomcat_agent_env_var_name*              | CATALINA_OPTS                            | The name of the environment variable to be used for Agent injection. |
| *dynatrace_tomcat_agent_env_var_file_name*         | **required**                             | The name of the file to be modified. |
| *dynatrace_tomcat_agent_env_var_file_insert_after* | BOF                                      | A regex, BOF or EOF for *begin-of-file* and *end-of-file*, respectively. If a given regex is not matched, the *-agentpath* option will be appended to the file. |
| *dynatrace_tomcat_agent_name*                      | apache-tomcat-agent                      | The name of the Java Agent as it appears in Dynatrace. |
| *dynatrace_tomcat_agent_collector_hostname*        | localhost                                | The location of the collector the Agent shall connect to. |
| *dynatrace_tomcat_agent_collector_port*            | 9998                                     | The port on the collector the Agent shall connect to. |
| *dynatrace_tomcat_agent_linux_agent_path*          | /opt/dynatrace/agent/lib64/libdtagent.so | The path to the Agent libary. |
| *dynatrace_tomcat_agent_state*                     | present                                  | Whether the Agent shall be ```present``` or ```absent```. |

## Example Playbook

	- hosts: all
	  roles:
	    - role: dynatrace.Dynatrace-Tomcat-Agent
	      dynatrace_tomcat_agent_env_var_file_name: /opt/tomcat/bin/catalina.sh
	      dynatrace_tomcat_agent_env_var_file_insert_after: '#!/bin/sh'

## Testing

We use [Test Kitchen](http://kitchen.ci) to automatically test our automated deployments with [Serverspec](http://serverspec.org):

1) Install Kitchen and its dependencies from within the project's directory:

```
gem install bundler
bundle install
```

2) Run tests

```
kitchen test
```

## Additional Resources

- [Blog: How to Automate Enterprise Application Monitoring with Ansible](http://apmblog.dynatrace.com/2015/03/04/how-to-automate-enterprise-application-monitoring-with-ansible/)
- [Blog: How to Automate Enterprise Application Monitoring with Ansible - Part II](http://apmblog.dynatrace.com/2015/04/23/how-to-automate-enterprise-application-monitoring-with-ansible-part-ii/)
- [Slide Deck: Automated Deployments](http://slideshare.net/MartinEtmajer/automated-deployments-slide-share)
- [Slide Deck: Automated Deployments (of Dynatrace) with Ansible](http://www.slideshare.net/MartinEtmajer/automated-deployments-with-ansible)
- [Slide Deck: Testing Ansible Roles with Test Kitchen, Serverspec and RSpec](http://www.slideshare.net/MartinEtmajer/testing-ansible-roles-with-test-kitchen-serverspec-and-rspec-48185017)
- [Tutorials: Automated Deployments (of Dynatrace) with Ansible](https://community.compuwareapm.com/community/display/LEARN/Tutorials+on+Automated+Deployments#TutorialsonAutomatedDeployments-ansible)

## Questions?

Feel free to post your questions on the Dynatrace Community's [Continuous Delivery Forum](https://community.dynatrace.com/community/pages/viewpage.action?pageId=46628921).

## License

Licensed under the MIT License. See the LICENSE file for details.
[![analytics](https://www.google-analytics.com/collect?v=1&t=pageview&_s=1&dl=https%3A%2F%2Fgithub.com%2FdynaTrace&dp=%2FDynatrace-Tomcat-Agent-Ansible&dt=Dynatrace-Tomcat-Agent-Ansible&_u=Dynatrace~&cid=github.com%2FdynaTrace&tid=UA-54510554-5&aip=1)]()
