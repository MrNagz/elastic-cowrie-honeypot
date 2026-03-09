        Internet Attackers
                │
                ▼
        ┌────────────────┐
        │  Cowrie SSH    │
        │  Honeypot VPS  │
        └───────┬────────┘
                │
                ▼
        ┌────────────────┐
        │ Elastic Agent  │
        │ Log Shipper    │
        └───────┬────────┘
                │
                ▼
        ┌────────────────┐
        │ Elasticsearch  │
        │ + GeoIP        │
        └───────┬────────┘
                │
                ▼
        ┌────────────────┐
        │ Kibana         │
        │ Dashboards     │
        │ Detections     │
        └────────────────┘
