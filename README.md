# my-netbird-experience

Hi there, 

I am using Netbird since Mid-2023 in a self hosted environment and want to share my experience. 


## Monitoring

I designed some Dashboards with grafana. I used chatgpt for the base and then extended it. 


Here’s a **short, clean bullet-list description** of the dashboard:

### Netbird Relay – App Metrics Dashboard

![CleanShot 2025-11-19 at 14.57.42@2x](<res/CleanShot 2025-11-19 at 14.57.42@2x.jpg>)

First, this is a dashboard showing some metrics about hte netbird relay. You find it in the `res/dasboards` directory of the repo. 

#### Top-level metrics (stat panels)

* **Peers (total):** Total number of peers connected to the relay.
* **Peers (active):** Peers currently active / exchanging data.
* **Peers (idle):** Peers connected but not active.
* **RX rate:** Incoming traffic in bytes/sec (5-minute rate).
* **TX rate:** Outgoing traffic in bytes/sec (5-minute rate).

#### Latency metrics (timeseries)

* **Peer authentication latency:** p50, p90, p99, and average time to authenticate peers.
* **Peer store latency:** p50, p90, p99, and average time to store peer info.

#### Traffic over time

* **RX vs. TX throughput chart:** Historical incoming/outgoing relay traffic.

#### Peer population over time

* Time series of:

  * **Total peers**
  * **Active peers**
  * **Idle peers**
    grouped by relay instance.

#### Dashboard variables

* **Datasource:** Choose Prometheus instance.
* **Job:** Filter metrics by Prometheus job.
* **Instance:** Filter metrics by relay server instance.

### Netbird Management & Signal – App Metrics (Summary)

This dashboard give you some insights of the management and signal service. It's still WIP, not all metrics are displayed properly, yet. You find it in the `res/dasboards` directory of the repo. 

![CleanShot 2025-11-19 at 15.07.11@2x.jpg](<res/CleanShot 2025-11-19 at 15.07.11@2x.jpg>)


#### Top-level load & concurrency

* **Registrations rate (req/s):** How many peers register per second.
* **Mgmt gRPC connected streams:** Number of active management gRPC streams.
* **HTTP RPS (mgmt):** Overall HTTP request rate to the management API.
* **Store tx rate (ops/s):** How many store (DB) transactions are executed per second.

#### Latency: registration, RPC, network map

* **Peer registration delay (ms):** p50, p90, p99, avg time for a peer to register.
* **Signal RPC duration (ms) by method:** p50/p90/p99 latency per gRPC method.
* **Network map calc duration (ms):** p50/p90/p99/avg time to build peer network map.
* **Account peers update duration (ms):** p50/p90/p99/avg for updating account peers.
* **Mgmt gRPC sync duration (ms):** p50/p90/p99/avg for sync gRPC requests.
* **Store transaction duration (ms):** p90 and avg DB transaction latency.
* **Update channel internal timings (µs):** Avg times for network-map calc, posture checks, creating/checking channels, sending updates, converting to sync response.

#### Traffic & payload characteristics

* **RPC request size (bytes, avg):** Average request size per RPC method.
* **RPC response size (bytes, avg):** Average response size per RPC method.
* **Network map object count (avg):** Average number of objects (peers/routes/rules) in network map.
* **Update channel queue depth:** Average size of the update queue.

#### HTTP behavior & health

* **HTTP request rate by endpoint & method:** RPS breakdown per API endpoint + method.
* **HTTP request latency p90 (ms) by endpoint & method:** Slowest HTTP paths at p90.
* **Overall HTTP latency (read vs write):** Average latency split by read/write type.
* **HTTP responses by status code (rate):** Rate of responses grouped by HTTP status (e.g. 200, 4xx, 5xx).

#### Identity provider (IdP) integration

* **IDP request rate:** Request rate for `authenticate` and `get_accounts` calls.

#### Dashboard controls

* **Variables:** `Datasource`, `Job`, `Instance` to filter by environment / service / node.
* **Time range:** Last 6 hours, auto-refresh every 30 seconds.
