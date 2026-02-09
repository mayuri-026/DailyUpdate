SSH into EC2
Command: ssh -i key.pem ubuntu@EC2_IP
Meaning: Connects your local machine to the EC2 server securely.

Update server packages
Command: sudo apt update && sudo apt upgrade -y
Meaning: Updates Ubuntu packages to latest versions.

Install Git
Command: sudo apt install git -y
Meaning: Installs Git to clone repository.
Git is required to download the backend code from GitHub

Generate SSH key
Command: ssh-keygen -t ed25519
Meaning: Creates SSH key for GitHub authentication.

Clone repo
Command: git clone <repo_ssh_url>
Meaning: Downloads backend code from GitHub.

Install Python & tools
Command: sudo apt install python3 python3-pip python3-venv -y
Meaning: Installs Python and virtual environment tools.
Python → backend language

pip → installs dependencies

venv → isolates project libraries


Create virtual env
Command: python3 -m venv venv
Meaning: Creates isolated Python environment.

Activate venv
Command: source venv/bin/activate
Meaning: Activates Python virtual environment.
This activates the project environment so all backend packages install correctly


Install dependencies
Command: pip install -r requirements.txt
Meaning: Installs backend packages.

Run backend test
Command: uvicorn app.main:app --host 0.0.0.0 --port 8000
Meaning: Runs backend server manually.

Install PM2
Command: sudo npm install -g pm2
Meaning: Installs process manager.
Keeps backend running 24/7
Automatically restarts app if it crashes

Run backend in PM2
Command: pm2 start 'uvicorn app.main:app --host 0.0.0.0 --port 8000' --name anymoney-backend
Meaning: Runs backend permanently.
Now the backend runs continuously in the background like a production service.

Save PM2 config
Command: pm2 save
Meaning: Saves process list for reboot.
This ensures the backend restarts automatically after server reboots.

Enable PM2 startup
Command: pm2 startup
Meaning: Creates auto-start service.

Install NGINX
Command: sudo apt install nginx -y
Meaning: Installs reverse proxy server.
NGINX handles:
Public traffic
Security
Port forwarding (80/443 → 8000)

Reload NGINX
Command: sudo systemctl reload nginx
Meaning: Applies config changes.

Install SSL
Command: sudo certbot --nginx -d domain
Meaning: Installs HTTPS certificate.

Restart backend
Command: pm2 restart anymoney-backend
Meaning: Restarts backend after config change.
