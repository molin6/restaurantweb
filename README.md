# Restaurant Web Application
This project is a web application for restaurant management and browsing. It utilizes Python and integrates with SQL Server for data management, including handling menus.

# Deploying the VM on Azure

## Marketplace Selection
- In the marketplace, find SQL Server 2022 on Windows Server 2022 and choose the free SQL license version using SQL Server 2022 Developer.

## VM Size
- Select Standard B2s (2 vCPUs, 4 GiB memory).

## Authentication
- Set up a username and password (important to remember): Example: Username: RestaurantWebAdmin, Password: RestaurantAdmin1!

## Disks
- OS disk type: Standard HDD

## Network Settings
- Enable inbound ports for HTTP & RDP.

## Management
- Enable Auto Shutdown.

## SQL Server Settings
- Set Connectivity to Private within the virtual network, Port: 1433.
- Storage: CHANGE TO 8GiB for both Data Storage and Local Storage
- Enable SQL Authentication.

## Add a tag
- Enter your name as the tag

## Create the VM
- This could take a while. If it takes longer than expected, check the Azure dashboard.

# Connecting to the VM
- Go to "Connect" and download the RDP file, then open it. Ignore any trust warnings.

# Once Logged In
- Confirm any prompts to trust the network.
- Install the latest versions of **Git** and **Python** from their official websites.

# Setting Up SQL Server
1. **Open SQL Server Configuration Manager**
   - Navigate to SQL server network configuration and enable all protocols for MSSQLSERVER.

2. **Restart SQL Server**
   - Restart the SQL Server service, usually named SQL Server(MSSQLSERVER).

3. **Open SQL Server Management Studio**
   - Log in using Windows authentication, right-click on the server (at the top of the list), go to properties → Security, and change to SQL Server and Windows Authentication mode. Click OK. If this is already done, skip this step.

# Setting Up the Database
1. **In SQL Server Management Studio**
   - Create a database and a login with SQL Server Authentication. Assign the sysadmin role and map the user to your database with db_owner role.

# Setting Up the Website
1. **Open GitBash**
   - Use `cd` and `ls` to navigate. Clone the repository and navigate into it. Install requirements from `requirements.txt`.

2. **Testing the Setup**
   - Run `python manage.py runserver` and navigate to `localhost:8000` in the browser.

# Adding Credentials to the Webapp
- Rename `.env.sample` to `.env` and input your database name, username, and password. Leave the Port field blank.

# Finalizing Database Setup
1. **Migrate Database Schema**
   - Use `python manage.py makemigrations` and `python manage.py migrate` to apply the schema.

2. **Populating the Database**
   - Load the menu data with `python manage.py loaddata menu_data.json`.

# Making the Website Public

## In the VM
- Configure Windows Defender Firewall to allow inbound rules for all local ports.

## In the Azure Dashboard
- Add a new inbound security rule in the Network Security Group to allow traffic on port 8000.

## Running the Server
- Run `python manage.py runserver 0.0.0.0:8000` in the VM.

## Accessing the Website
- Use the VM's public IP address followed by `:8000` to access the website from anywhere.

# License

This work is licensed under the Creative Commons Attribution-NonCommercial 4.0 International Public License (CC BY-NC 4.0).

## You are free to:

- **Share** — copy and redistribute the material in any medium or format
- **Adapt** — remix, transform, and build upon the material

The licensor cannot revoke these freedoms as long as you follow the license terms.

## Under the following terms:

- **Attribution** — You must give appropriate credit, provide a link to the license, and indicate if changes were made. You may do so in any reasonable manner, but not in any way that suggests the licensor endorses you or your use.
- **NonCommercial** — You may not use the material for commercial purposes.
- **No additional restrictions** — You may not apply legal terms or technological measures that legally restrict others from doing anything the license permits.

## Notices:

You do not have to comply with the license for elements of the material in the public domain or where your use is permitted by an applicable exception or limitation.

No warranties are given. The license may not give you all of the permissions necessary for your intended use. For example, other rights such as publicity, privacy, or moral rights may limit how you use the material.

For the full license text and further information, please visit [Creative Commons Attribution-NonCommercial 4.0 International Public License](https://creativecommons.org/licenses/by-nc/4.0/legalcode).

