# Kubernetes automated dashboard

The following automated dashboards exist for AppSignal for Kubernetes:

- [Nodes](#nodes)
- [Pods](#pods)

## Nodes

The Nodes dashboard uses Kubernetes node metrics extracted from the `/api/v1/nodes/<NODE>/proxy/stats/summary` API endpoint via [AppSignal for Kubernetes](https://github.com/appsignal/appsignal-kubernetes).
The following metrics are reported through this automated dashboard:

- node_cpu_usage_nano_cores
- node_memory_usage_bytes
- node_memory_available_bytes
- node_swap_available_bytes
- node_swap_usage_bytes
- node_fs_available_bytes
- node_fs_used_bytes
- node_network_rx_bytes
- node_network_tx_bytes
- node_fs_inodes
- node_fs_inodes_free
- node_fs_inodes_used
- node_rlimit_maxpid
- node_rlimit_curproc

## Pods

The Nodes dashboard uses Kubernetes node metrics extracted from the `/api/v1/nodes/<NODE>/proxy/stats/summary` API endpoint via [AppSignal for Kubernetes](https://github.com/appsignal/appsignal-kubernetes).
The following metrics are reported through this automated dashboard:

- pod_cpu_usage_nano_cores
- pod_cpu_usage_core_nano_seconds
- pod_memory_working_set_bytes
- pod_swap_available_bytes
- pod_swap_usage_bytesc
