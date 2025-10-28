# git
KCTRONICS Monitoring Stack - Prometheus + Grafana + Cloudflare Exporter
======================================================================

This package deploys a monitoring stack suitable for cloud/VM deployment (e.g., AWS EC2, GCP VM).
Services:
- Prometheus (9090)
- Grafana (3000) - default admin:admin
- Cloudflare Exporter (9588) - exposes metrics polled from origins and Cloudflare API

Deployment (Cloud VM / EC2)
1. Ensure Docker and Docker Compose are installed on the VM.
2. Upload this folder to the VM and run:
   docker-compose -f docker-compose.monitor.yml up -d --build
3. Set environment variable on the host for the Cloudflare exporter (optional):
   export CLOUDFLARE_API_TOKEN='your_token_here'
   The exporter will use it to poll Cloudflare Load Balancer info; otherwise it probes origins directly.
4. Open Grafana at http://<vm-ip>:3000 (admin/admin). Dashboard auto-provisioned:
   - KCTRONICS LMS Failover Dashboard

Notes
- Prometheus scrapes the exporter and also directly probes origin /health endpoints.
- Customize prometheus.yml if you have additional metrics or exporters.
- For production, secure Grafana (change admin password) and enable TLS via a reverse proxy (nginx or cloud load balancer).
