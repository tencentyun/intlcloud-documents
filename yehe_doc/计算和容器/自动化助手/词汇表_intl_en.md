### Execution path
TAT stores the user command to the instance as a file and then execute it. For a Linux instance, the path is /tmp.

### Execution Status
- Instance-level execution status: the status of a command when it’s executed in one instance.
- Overall execution status: the status of a command when it’s executed in multiple instances.

### TAT agent
TAT agent is a light-weighted plugin that installed in Lighthouse instances. All commands are executed over this agent.