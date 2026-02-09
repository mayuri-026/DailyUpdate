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



FRONTEND 
SSH into EC2
ssh -i key.pem ubuntu@EC2_IP
Connects your local machine to the EC2 server.

Install Git
sudo apt update
sudo apt install git -y
Updates packages and installs Git to clone repositories.
Server वरील packages update राहावेत म्हणून

Generate SSH key
ssh-keygen -t ed25519
cat ~/.ssh/id_ed25519.pub
Creates a secure key to connect GitHub with the server.
हा SSH key GitHub आणि server मधला secure connection बनवतो

Clone repo
git clone git@github.com:TechJar05/Anymoney-Demat-Frontend.git
या step मध्ये मी frontend project EC2 server वर download करतो

cd Anymoney-Demat-Frontend-
Downloads project and enters folder.

Install Node & npm
sudo apt install nodejs npm -y
node -v
npm -v
Frontend build करण्यासाठी Node.js environment तयार करतो.

Installs Node environment for building frontend.
Install dependencies
npm install
Installs libraries required by the project.
Frontend project साठी लागणाऱ्या सगळ्या libraries install होतात.
Build frontend

npm run build
हा step frontend ला production-ready बनवतो

Creates optimized production files in dist folder.
Install nginx
sudo apt install nginx -y
sudo systemctl start nginx
sudo systemctl enable nginx
NGINX वापरून frontend website public access साठी serve करतो
Installs and starts web server.
Test & restart nginx

sudo nginx -t
sudo systemctl restart nginx
Applies configuration safely.
NGINX changes apply करण्याआधी test करतो

Fix permissions
sudo chown -R www-data:www-data /path/to/dist
sudo chmod -R 755 /home/ubuntu
Allows nginx to read files.
Web server ला frontend files access मिळण्यासाठी permissions देतो

Enable SSL
sudo apt install certbot python3-certbot-nginx -y
sudo certbot --nginx -d anymoneypro.in -d www.anymoneypro.in
Frontend website secure करण्यासाठी HTTPS enable करतो
Enables HTTPS.

Update deployment
git pull
npm install
npm run build
sudo systemctl restart nginx
Frontend मध्ये बदल झाले की हे steps वापरून update deploy करतो.
Updates site with latest code.

Debug commands
sudo tail -n 20 /var/log/nginx/error.log
sudo ss -tulpn
sudo systemctl status nginx
Error आली तर कारण शोधण्यासाठी

Server status check करण्यासाठी
Helps diagnose issues.



