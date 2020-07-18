ansible-role-telegraf
=====================

An [Ansible][ansible] role to deploy InfluxData's [Telegraf][influx:telegraf] agent.

Requirements
------------

none

Role Variables
--------------

| Name                                             | Description                                                                                                                                            | Default Value               |
| ------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------- |
| `telegraf.agent.global_tags`                     | [Tags][influxdb:tags] applied to all metrics                                                                                                           | none                        |
| `telegraf.agent.interval`                        | Default data collection interval for all inputs as [Go duration expression][go:duration]                                                               | `10s`                       |
| `telegraf.agent.flush_interval`                  | Default flushing interval for all outputs. You shouldn't set this below`telegraf.agent.interval`. [Go duration expression][go:duration]                | `10s`                       |
| `telegraf.agent.flush_jitter`                    | Jitter the flush interval by a random amount `0s < value < telegraf.agent.flush_jitter`. [Go duration expression][go:duration]                         | `0s`                        |
| `telegraf.agent.round_interval`                  | Rounds collection interval to `telegraf.agent.interval`, ie, if `telegraf.agent.interval` is "10s" then always collect on :00, :10, :20, etc.          | `false`                     |
| `telegraf.agent.collection_jitter`               | Collection jitter is used to jitter the collection by a random amount. [Go duration expression][go:duration]. Must be < than `telegraf.agent.interval` | `0s`                        |
| `telegraf.agent.metric.batch_size`               | Telegraf will send metrics to outputs in batches of at most `telegraf.agent.metric.batch_size`.                                                        | `1000`                      |
| `telegraf.agent.metric.buffer_limit`             | For failed writes, telegraf will cache metric_buffer_limit metrics for each output, and will flush this buffer on a successful write.                  | `100000`                    |
| `telegraf.agent.debug`                           | Run telegraf with debug log messages.                                                                                                                  | `false`                     |
| `telegraf.agent.quiet`                           | Run telegraf in quiet mode (error log messages only).                                                                                                  | `false`                     |
| `telegraf.agent.hostname`                        | Override default hostname, if empty the hostname will be automatically determined.                                                                     | none                        |
| `telegraf.agent.omit_hostname`                   | If set to true, do no set the "host" tag in the telegraf agent. ***Do not change unless you really know what you are doing.***                         | `false`                     |
| `telegraf.outputs.influxdb.urls`                 | A list of full HTTP URLs for your InfluxDB instance.                                                                                                   | `["http://127.0.0.1:8086"]` |
| `telegraf.outputs.influxdb.insecure_skip_verify` | When set to true, and `telegraf.outputs.influxdb.urls` contains `https` URLs, TLS is used, but the chain & host verification is skipped.               | `false`                     |
| `telegraf.outputs.influxdb.database`             | The target database for metrics; will be created as needed.                                                                                            | `metrics`                   |
| `telegraf.outputs.influxdb.retention_policy`     | Name of existing [retention policy][influx:retention_policy] to write to. If empty, telegraf writes to the default retention policy                    | none                        |
| `telegraf.outputs.influxdb.username`             | Username to authenticate telegraf against InfluxDB.                                                                                                    | none                        |
| `telegraf.outputs.influxdb.password`             | Password to authenticate telegraf against InfluxDB.                                                                                                    | none                        |

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: telegraf, telegraf.outputs.influxdb.username: 'me', telegraf.outputs.influxdb.password: 'secret' }

License
-------

ansible-role-telegraf - Role to deploy InfluxData's telegraf
Copyright (C) 2020  Markus W Mahlberg

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program.  If not, see <https://www.gnu.org/licenses/>.


[ansible]: https://docs.ansible.com/ansible/latest/index.html
[influx:telegraf]: https://docs.influxdata.com/telegraf/v1.14/
[influx:retention_policy]: https://docs.influxdata.com/influxdb/v1.8/concepts/glossary/#retention-policy-rp
[go:duration]: https://pkg.go.dev/time?tab=doc#ParseDuration
