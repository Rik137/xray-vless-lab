# xray-vless-lab

### Description
This project is intended for users who need a reliable and reproducible way to bypass internet censorship, DPI, and network restrictions.  
The repository contains a practical guide for deploying and basic configuration of Xray Core using the VLESS protocol. The main focus is on stable operation under active blocking conditions, minimal configuration, and understanding what is happening, rather than blindly copying ready-made solutions.  
The project is educational and practical, designed for self-deployment on your own server.

### Project Structure
The project uses two configuration files:  
- `server_config.json` — Xray configuration on the server (VPS)  
- `client_config.json` — client configuration (PC / smartphone)

The workflow is as follows:  
1. UUIDs and cryptographic keys are generated  
2. The generated values are inserted into both configuration files  
3. The server is started and restarted  
4. The client connects to the server

### Requirements
Before starting, make sure the following conditions are met:  
- Rented VPS in a jurisdiction without aggressive internet censorship (Europe, Asia, Latin America)  
- Operating system: Ubuntu 20.04+  
- SSH access to the server with root or sudo privileges  
- Basic understanding of Linux and network services

### Installing Xray
Installation is done from the official repository:  
```bash
sudo apt update
sudo apt install xray
```
After installation, the binary will be available at: /usr/bin/xray  
Generating UUIDs and Keys (mandatory)  
### Generating UUID  
The VLESS protocol requires a unique client UUID.  
```bash
xray uuid
```
Example output:  
```bash
e7b0c2a4-9f3d-4b6a-8d91-xxxxxxxxxxxx
```
This UUID is used on both the server and the client.  
Generating Keys (X25519 / Reality)  
For configurations with encryption (Reality / TLS), a key pair must be generated:  
```bash
xray x25519
```
Example output:  
```bash
Private key:  <PRIVATE_KEY>
Public key:   <PUBLIC_KEY>
```
Private key is used only on the server  
Public key is used in the client configuration  
Server Configuration  
Configuration File  
The main Xray configuration file on the server should be located at:  
```bash
/usr/local/etc/xray/config.json
```
Take the server_config.json file from the project and:  
Insert the generated UUID  
Insert the Private key  
Change the port if necessary  
Example fragment:  
```bash
{
  "id": "<UUID_here>"
}
```
Copy the file:  
```bash
sudo mkdir -p /usr/local/etc/xray
sudo cp server_config.json /usr/local/etc/xray/config.json
```
Then restart the service:  
sudo systemctl restart xray  
Starting and Checking the Server  
Add to autostart:  
```bash
sudo systemctl enable xray
```
Check status:  
```bash
sudo systemctl status xray
```
Check logs:  
```bash
journalctl -u xray -e
```
Check that the port is listening:
```bash
ss -tulnp | grep xray
```
### Client Configuration  
To connect to the server, a client application with VLESS / Xray support is required.  
Recommended Clients  

Windows / macOS / Linux  
v2rayN  
v2rayA  
iOS / macOS  
V2Box  
Android  
v2rayNG  
All listed clients support Xray and VLESS.  
Configuring the Client  
Open the client_config.json file and:  

Insert the same UUID used on the server  
Insert the Public key  
Specify your VPS IP or domain  
Specify the server port  
After that:  
Import the configuration into the client application  
Connect to the server  
Checking Operation  
After connecting the client:  
Test access to blocked resources  
Ensure traffic goes through the VPS  
In case of errors, check server logs instead of randomly changing the config  
Security and Notes  
Do not use standard ports unless necessary  
Restrict server access using ufw or iptables  
Do not store private keys in public repositories  
Regularly update the system and Xray  
This project does not provide a ready-made VPN service but offers tools and knowledge for self-deployment.  
