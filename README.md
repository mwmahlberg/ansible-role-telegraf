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
| `telegraf_agent_global_tags`                     | [Tags][influxdb:tags] applied to all metrics                                                                                                           | none                        |
| `telegraf_agent_interval`                        | Default data collection interval for all inputs as [Go duration expression][go:duration]                                                               | `10s`                       |
| `telegraf_agent_flush_interval`                  | Default flushing interval for all outputs. You shouldn't set this below`telegraf_agent_interval`. [Go duration expression][go:duration]                | `10s`                       |
| `telegraf_agent_flush_jitter`                    | Jitter the flush interval by a random amount `0s < value < telegraf_agent_flush_jitter`. [Go duration expression][go:duration]                         | `0s`                        |
| `telegraf_agent_round_interval`                  | Rounds collection interval to `telegraf_agent_interval`, ie, if `telegraf_agent_interval` is "10s" then always collect on :00, :10, :20, etc.          | `false`                     |
| `telegraf_agent_collection_jitter`               | Collection jitter is used to jitter the collection by a random amount. [Go duration expression][go:duration]. Must be < than `telegraf_agent_interval` | `0s`                        |
| `telegraf_agent_metric.batch_size`               | Telegraf will send metrics to outputs in batches of at most `telegraf_agent_metric_batch_size`.                                                        | `1000`                      |
| `telegraf_agent_metric.buffer_limit`             | For failed writes, telegraf will cache metric_buffer_limit metrics for each output, and will flush this buffer on a successful write.                  | `100000`                    |
| `telegraf_agent_debug`                           | Run telegraf with debug log messages.                                                                                                                  | `false`                     |
| `telegraf_agent_quiet`                           | Run telegraf in quiet mode (error log messages only).                                                                                                  | `false`                     |
| `telegraf_agent_hostname`                        | Override default hostname, if empty the hostname will be automatically determined.                                                                     | none                        |
| `telegraf_agent_omit_hostname`                   | If set to true, do no set the "host" tag in the telegraf agent. ***Do not change unless you really know what you are doing.***                         | `false`                     |
| `telegraf_outputs_influxdb_urls`                 | A list of full HTTP URLs for your InfluxDB instance.                                                                                                   | `["http://127.0.0.1:8086"]` |
| `telegraf_outputs_influxdb_insecure_skip_verify` | When set to true, and `telegraf_outputs_influxdb_urls` contains `https` URLs, TLS is used, but the chain & host verification is skipped.               | `false`                     |
| `telegraf_outputs_influxdb_database`             | The target database for metrics; will be created as needed.                                                                                            | `metrics`                   |
| `telegraf_outputs_influxdb_retention_policy`     | Name of existing [retention policy][influx:retention_policy] to write to. If empty, telegraf writes to the default retention policy                    | none                        |
| `telegraf_outputs_influxdb_username`             | Username to authenticate telegraf against InfluxDB.                                                                                                    | none                        |
| `telegraf_outputs_influxdb_password`             | Password to authenticate telegraf against InfluxDB.                                                                                                    | none                        |

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: telegraf, telegraf_outputs_influxdb_username: 'me', telegraf_outputs_influxdb_password: 'secret' }

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
[influxdb:tags]: https://docs.influxdata.com/influxdb/v1.8/concepts/glossary/#tag
[go:duration]: https://pkg.go.dev/time?tab=doc#ParseDuration
