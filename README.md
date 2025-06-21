# Monitoring
Install Node_exporter
Download:
wget https://github.com/prometheus/node_exporter/releases/download/v1.8.0/node_exporter-1.8.0.linux-amd64.tar.gz

Ekstrak:
tar -xzf node_exporter-1.8.0.linux-amd64.tar.gz
cd node_exporter-1.8.0.linux-amd64

sudo useradd -rs /bin/false node_exporter
sudo cp node_exporter /usr/local/bin/

menjalankan sebagai service systemd:
cat <<EOF | sudo tee /etc/systemd/system/node_exporter.service
[Unit]
Description=Node Exporter
After=network.target

[Service]
User=node_exporter
Group=node_exporter
Type=simple
ExecStart=/usr/local/bin/node_exporter

[Install]
WantedBy=default.target
EOF

sudo systemctl daemon-reexec
sudo systemctl enable --now node_exporter

#setelah itu jalankan
docker compose up -d


