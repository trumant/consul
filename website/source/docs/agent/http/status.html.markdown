---
layout: "docs"
page_title: "Status (HTTP)"
sidebar_current: "docs-agent-http-status"
description: >
  The Status endpoints are used to get information about the status
  of the Consul cluster.
---

# Status HTTP Endpoint

The Status endpoints are used to get information about the status
of the Consul cluster.

Please note: this information is generally very low level
and not often useful for clients.

The following endpoints are supported:

* [`/v1/status/leader`](#status_leader) : Returns the current Raft leader
* [`/v1/status/peers`](#status_peers) : Returns the current Raft peer set
* [`/v1/status/info`](#status_info) : Returns debugging information useful for operators

### <a name="status_leader"></a> /v1/status/leader

This endpoint is used to get the Raft leader for the datacenter
in which the agent is running. It returns an address, such as:

```text
"10.1.10.12:8300"
```

### <a name="status_peers"></a> /v1/status/peers

This endpoint retrieves the Raft peers for the datacenter in which the
the agent is running. It returns a list of addresses, such as:

```javascript
[
  "10.1.10.12:8300",
  "10.1.10.11:8300",
  "10.1.10.10:8300"
]
```

This list of peers is strongly consistent and can be useful in determining when
a given server has successfully joined the cluster.

### <a name="status_info"></a> /v1/status/info

This endpoint retrieves useful runtime data on the Consul process and the
state of the Consul cluster. It returns a response like:

```javascript
{
  "agent": {
    "check_monitors": 0,
    "check_ttls": 0,
    "checks": 0,
    "services": 1,
  },
  "build": {
    "prerelease": "",
    "revision": "9a9cc934",
    "version": "0.5.2",
  }
  "consul": {
    "bootstrap": false,
    "known_datacenters": 3,
    "leader": false,
    "server": true,
  },
  "raft": {
    "applied_index": 111098,
    "commit_index": 111098,
    "fsm_pending": 0,
    "last_contact": "43.302939ms",
    "last_log_index": 111098,
    "last_log_term": 103796,
    "last_snapshot_index": 108465,
    "last_snapshot_term": 103796,
    "num_peers": 2,
    "state": "Follower",
    "term": 103796
  },
  "runtime": {
    "arch": "amd64",
    "cpu_count": 2,
    "goroutines": 82,
    "max_procs": 2,
    "os": "linux",
    "version": "go1.4.2"
  },
  "serf_lan": {
    "encrypted": true,
    "event_queue": 0,
    "event_time": 26,
    "failed": 0,
    "intent_queue": 0,
    "left": 0,
    "member_time": 302,
    "members": 14,
    "query_queue": 0,
    "query_time": 5
  },
  "serf_wan": {
    "encrypted": true,
    "event_queue": 0,
    "event_time": 1,
    "failed": 0,
    "intent_queue": 0,
    "left": 0,
    "member_time": 326,
    "members": 9,
    "query_queue": 0,
    "query_time": 1
  }
}
```
