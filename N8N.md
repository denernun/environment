## N8N
```bash
$ sudo nano /etc/systemd/system/n8n.service
$ sudo systemctl daemon-reload
$ sudo systemctl restart n8n.service
$ sudo systemctl status n8n.service
```
## SERVICE
```text
[Unit]
Description=n8n workflow automation platform
Documentation=https://docs.n8n.io/
After=network.target

[Service]
User=ubuntu
Group=ubuntu
WorkingDirectory=/home/ubuntu
Environment=NODE_ENV=production
Environment=N8N_HOST=localhost
Environment=N8N_PORT=5678
Environment=N8N_PROTOCOL=http
Environment=N8N_ENCRYPTION_KEY=797642d8-add1-4d6e-8e1f-92c96c47d51d
Environment=N8N_SECURE_COOKIE=false
Environment=N8N_ENFORCE_SETTINGS_FILE_PERMISSIONS=true
Environment=N8N_RUNNERS_ENABLED=true
# Environment=DB_TYPE=postgres
# Environment=DB_POSTGRESQL_HOST=localhost
# Environment=DB_POSTGRESQL_PORT=5432
# Environment=DB_POSTGRESQL_DATABASE=n8n
# Environment=DB_POSTGRESQL_USER=postgres
# Environment=DB_POSTGRESQL_PASSWORD=Soft@010203@2021

ExecStart=/usr/bin/n8n start
Restart=on-failure
StandardOutput=journal
StandardError=journal

[Install]
WantedBy=multi-user.target
```
