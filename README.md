# Log Enrichment & Threat-Aware GeoIP Pipeline using Logstash

A mini project demonstrating how to build, configure, and run an **enrichment pipeline** in **Logstash** to transform raw IP logs into enriched, context-rich security data.  

The pipeline uses **MaxMind GeoLite2** for geolocation enrichment and can be easily extended with threat intelligence lookups for SOC and IR workflows.

---

## Project Overview

This project ingests raw IP data, enriches it using the GeoIP database, and outputs JSON logs containing detailed geolocation metadata such as:

- Country, city, and region  
- Timezone  
- Latitude and longitude  
- Continent and ISO country code  

Enrichment pipelines like this are key components in **SOC operations**, turning raw indicators into actionable intelligence.

---

## Pipeline Design

**Input:**  
Raw IP list (JSON format) is read from `input.txt` using the Logstash **file input plugin**.

**Filter:**  
The **GeoIP plugin** enriches each IP with location metadata from the **MaxMind GeoLite2-City** database.

**Output:**  
Enriched events are written to both console (`rubydebug`) and `output.json` in JSON format.

---

## Project Structure

```
├── docker-compose.yml # Docker setup for Logstash container
├── pipeline/
│ └── logstash.conf # Pipeline configuration
├── logs/
│ ├── input.json # Raw IP list input
│ └── output.json # Enriched output (auto-generated)
└── geoip/
└── GeoLite2-City.mmdb # GeoIP database (MaxMind)
```

---

## 🚀 How to Use

### 1. Clone the repository
```bash
git clone https://github.com/atharimran728/Log-Enrichment-Threat-Aware-GeoIP-Pipeline-using-Logstash.git
cd Log-Enrichment-Threat-Aware-GeoIP-Pipeline-using-Logstash
```

### 2. Prepare directories and files

Ensure you have the following:

`logs/input.json` - contains IPs to enrich
Example:
```
[
  {"source_ip": "1.1.1.1"},
  {"source_ip": "8.8.8.8"},
  {"source_ip": "185.220.101.4"}
]
```
`geoip/GeoLite2-City.mmdb` - download [GeoLite2 City](https://github.com/P3TERX/GeoLite.mmdb?tab=readme-ov-file)

### 3. Run Logstash via Docker Compose

```
docker-compose up
```

This will:

Spin up a Logstash container
Load the pipeline from `pipeline/logstash.conf`
Enrich IPs from `logs/input.json`
Output enriched logs to `logs/output.json`

### 4. Check Results

Once the process completes, view the enriched JSON - `logs/output.json`.

## Learning Objectives

- Understand the role of enrichment in SOC pipelines
- Use Logstash filters for data enhancement
- Build and deploy modular pipelines using Docker
- Prepare foundation for integrating ThreatIntel enrichment (future extension)




