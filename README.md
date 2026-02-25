# fitness-90-day-tracker
Offline-first PWA for tracking 90-day fitness programs

/app/backend/server.py
Now let me update the supervisor config to use npm (since the frontend uses npm, not yarn):
Action: $ cat > /etc/supervisor/conf.d/supervisord.conf << 'EOF'
# Next.js Frontend Configuration
[program:nextjs]
command=npm run dev
directory=/app/frontend
autostart=true
autorestart=true
environment=PORT="3000",NODE_ENV="development"
stderr_logfile=/var/log/supervisor/nextjs.err.log
stdout_logfile=/var/log/supervisor/nextjs.out.log
stopsignal=TERM
stopwaitsecs=30
stopasgroup=true
killasgroup=true

[program:backend]
command=/root/.venv/bin/uvicorn server:app --host 0.0.0.0 --port 8001 --workers 1 --reload
directory=/app/backend
autostart=true
autorestart=true
environment=APP_URL="https://52f093f9-8b5e-44c6-a043-cf13af143796.preview.emergentagent.com",INTEGRATION_PROXY_URL="https://integrations.emergentagent.com"
stderr_logfile=/var/log/supervisor/backend.err.log
stdout_logfile=/var/log/supervisor/backend.out.log
stopsignal=TERM
stopwaitsecs=30
stopasgroup=true
killasgroup=true

[program:mongodb]
command=/usr/bin/mongod --bind_ip_all
autostart=true
autorestart=true
stderr_logfile=/var/log/mongodb.err.log
stdout_logfile=/var/log/mongodb.out.log
EOF

Observation: Exit code: 0
