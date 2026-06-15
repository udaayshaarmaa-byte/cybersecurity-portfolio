# SIEM Process, Log Ingestion & Searching (Splunk & Chronicle)
---

## 1. SIEM Recap  The Three-Step Process

**SIEM** = an application that collects and analyses log data to monitor critical activities in an organization.

| Step | What happens |
|---|---|
| **1. Collect & aggregate** | SIEM collects event data from data sources across the environment |
| **2. Normalize** | Raw data (in many different formats) is converted into a **standard, consistent format**  only relevant info retained |
| **3. Analyze (index)** | Normalized data is organized and indexed so it can be searched, correlated, and analysed for patterns of unusual activity |

> {Normalization is the step that turns "a pile of differently-formatted logs" into "one searchable dataset." Without it, every source would need its own query syntax.}

### Common SIEM platforms
| Platform | Vendor | Flow |
|---|---|---|
| **Splunk Enterprise Security** | Splunk | Collects data → processes & stores in an **index** → accessed via search |
| **Chronicle (Google SecOps)** | Google Cloud | Data forwarded to Chronicle → **normalized** → indexed → searchable |

---

## 2. Log Ingestion

**Log ingestion** = the process of collecting and importing data from log sources into a SIEM tool.

- The SIEM creates a **copy** of the event data and retains it in its own storage  this means the SIEM can analyse/process data **without modifying original source logs**.
- Ingested data includes things like authentication attempts and network activity.

### Methods of ingestion

| Method | Notes |
|---|---|
| **Manual upload** | Inefficient/time-consuming at scale (networks can have thousands of devices) |
| **Log forwarders** | Software that automates collecting and sending log data |

- Some OSes have **native log forwarders**; otherwise install **third-party** forwarding software.
- Forwarder is configured to specify **which logs** to forward and **where** to send them (e.g. to the SIEM).
- SIEM tools may use **proprietary** forwarders or integrate with **open-source** ones  choice depends on org requirements and infrastructure compatibility.

---

## 3. Searching in Splunk (SPL)

**SPL** = Search Processing Language  Splunk's query language, used via the **Search & Reporting** app to search/retrieve events from **indexes**.

### Basic search
```
index=main fail
```
- `index=main`  retrieve events from the index named `main` (an index stores collected/processed event data)
- `fail`  search term; returns any event containing "fail"

### Pipes (`|`)
Pipes chain commands  output of one command becomes input to the next (same concept as Linux bash piping).

```
index=main fail | chart count by host
```
- `index=main fail`  retrieve events matching "fail" from index `main`
- `|`  passes those results into the next command
- `chart count by host`  transforms results into a chart of event **counts grouped by host**  useful for spotting hosts with excessive failures

### Wildcards (`*`)
```
index=main fail*
```
- `*` after `fail` matches any characters following it → returns "fail", "failed", "failure", etc.
- Expands results to catch events that label things differently.

### Exact phrase searches
- Use **double quotes** to match an exact phrase, e.g. `"login failure"` matches only that exact phrase  not "failure" or "login" separately.

### Excluding results
- `host!=www1`  excludes events from host `www1` from the results.

### Raw log search (demo walkthrough)
```
buttercupgames error OR fail*
```
- `buttercupgames`  specifies the index
- `error OR fail*`  Boolean **OR** searches for either term; `*` wildcard expands "fail" matches
- Narrow with a **time range** (e.g. last 30 days) for faster, more relevant results
- Results view includes:
  - **Timeline**  visual count of events over time (helps spot peaks/patterns)
  - **Events viewer**  list of matching events with timestamps, raw log data, and source info (hostname, source, source type)

> **Raw log search** has **slower performance** than structured search because it extracts log data fields *during* the search process itself.

> {General rule: the more specific the query (index, keywords, time range), the faster and more relevant the results. Broad queries like "failed login" across all indexed data will be slow and noisy.}

---

## 4. Searching in Google SecOps (Chronicle)

Two search types:

| Search type | Searches | Speed | When to use |
|---|---|---|---|
| **UDM Search** (default) | Ingested, parsed, **normalized** data (Unified Data Model) | Faster  structured/indexed data | Default choice for most searches |
| **Raw Log Search** | Raw, **unparsed** logs | Slower | When info isn't in normalized data, or to troubleshoot ingestion issues; supports **regular expressions** |

### Unified Data Model (UDM)
Every UDM event contains common fields:

| Field | Description |
|---|---|
| **Entities** | "Nouns"  context about the device/user/process involved (hostname, username, IP, etc.). Every UDM event has at least one. |
| **Event metadata** | Basic description  event type, timestamps, etc. |
| **Network metadata** | Network-related info and protocol details |
| **Security results** | Security outcome of the event (e.g. "virus detected and quarantined") |

### Example UDM searches
```
metadata.event_type = "USER_LOGIN"
```
- Searches for authentication-related events (user logins).

```
metadata.event_type = "USER_LOGIN" AND security_result.action = "BLOCK"
```
- `AND`  logical operator requiring both conditions
- `security_result.action = "BLOCK"`  the login attempt was **blocked/failed**
- Together: finds **failed login events**

### Search results UI
- **Bar graph timeline**  visualizes failed login events over time, helps spot patterns
- **Event list**  timestamps + **asset** (device name) per event
- Click an event → view the **raw log** for more detail
- **Quick Filters** (left panel)  e.g. `target.ip` lets you filter results down to a specific IP

### Detection rules in Chronicle
- **YARA-L**  Chronicle's language for writing detection rules against ingested log data (e.g. rules to detect data exfiltration activity).

---

## Key Terms

| Term | Definition |
|---|---|
| SIEM | Application that collects and analyses log data to monitor critical activities |
| Log ingestion | Process of collecting and importing data from log sources into a SIEM |
| Normalization | Converting collected data into a consistent, standard format |
| Index (Splunk) | Storage location for collected/processed event data |
| Log forwarder | Software that automates collecting and sending log data to a SIEM |
| SPL | Search Processing Language  Splunk's query language |
| Pipe (`\|`) | Chains commands, passing output of one as input to the next |
| Wildcard (`*`) | Matches any characters; expands search results |
| Raw log search | Searches unparsed/raw log data; slower, supports regex (in Chronicle) |
| UDM | Unified Data Model  Chronicle's normalized event format |
| UDM Search | Default Chronicle search over normalized/indexed data |
| Entities | UDM field providing context on device/user/process (required in every event) |
| Event metadata | UDM field describing event type, timestamps, etc. |
| Network metadata | UDM field with network/protocol details |
| Security results | UDM field describing the security outcome of an event |
| YARA-L | Chronicle's language for writing detection rules |
| Quick Filters | Chronicle UI feature for refining search results by field value |

---