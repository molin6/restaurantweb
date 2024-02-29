# Deploying the VM on Azure
In this assignment, you are going to deploy a virtual machine on Azure and set up a web server with a database. The web server will be running a Django application and the database will be running SQL Server.  This is an example of Infrastructure as a Service (IaaS) deployment, because we are going to take responsibility for the operating system and the software running on it, including the web server and the database.  In subsequent assignments, we will look at Platform as a Service (PaaS) deployments, where the cloud provider takes responsibility for the operating system and the software running on it, and we only need to worry about the application code.

## Prerequisites
You will need an Azure account and tenant.  You can sign up for a free account at [https://azure.microsoft.com/en-us/free/](https://azure.microsoft.com/en-us/free/).  Additionally, you will need to get the code from the repository at [https://github.com/MLDERES/ISYS5333].

## Instructions
1. Create a new virtual machine on Azure.
2. Configure SQL Server on the virtual machine.
3. Install the latest versions of Git and Python on the virtual machine.
4. Set up the database for the web application.
5. Set up the web application.
6. Make the website public.
7. Submit the URL of the website.

## Hints:
### Creating the Virtual Machine
- In the marketplace, find SQL Server 2022 on Windows Server 2022 and choose the free SQL license version using SQL Server 2022 Developer.
  - Select a small VM size, but not too small (since this application is not expected to have a lot of traffic).  A D2s_v3 with 2 vCPUs and 8 GB RAM should be sufficient.
  - Ensure that you are picking Standard HDD for the OS disk type (and a very small size, like 32GB).
  - Enable inbound ports for HTTP and RDP. (80 and 3389)
  - Enable Auto Shutdown.
  - Remember the username and password you set up for the VM.
  - On the Networking screen, select 'Delete public IP and NIC when VM is deleted'.
  
### SQL Server Settings
Now that the VM is setup, we need to configure SQL Server to allow remote connections and to allow SQL Server Authentication.  Since we are running the SQL server and the Web Server on the same machine, we will need to allow remote connections to the SQL Server.  We will also need to allow SQL Server Authentication, since the Django application uses SQL Server Authentication to connect to the database.

- Set Connectivity to Private within the virtual network, Port: 1433.
- Enable SQL Authentication.
- Storage: **CHANGE TO 8GiB for both Data Storage and Local Storage**.  Select 'Change Configuration' from the Storage section of the SQL Server settings.

### Connecting to the VM
#### Installing the latest versions of Git and Python
After creating the VM, you will need to connect to it using RDP and install the latest versions of Git and Python.  The setup is likely to take a few minutes (or longer), so be patient.  If it takes longer than expected, check the Azure dashboard to see if there are any issues.

Once the setup is complete you can connect to it using RDP and install the latest versions of Git and Python from their official websites.
- Confirm any prompts to trust the network.
- Install the latest versions of **Git** and **Python** from their official websites.

#### Setting Up SQL Server
1. Open SQL Server Configuration Manager and enable all protocols for MSSQLSERVER.
    - Navigate to SQL server network configuration and enable all protocols for MSSQLSERVER.
2. Restart SQL Server
   - Restart the SQL Server service, usually named SQL Server(MSSQLSERVER).
3. Open SQL Server Management Studio
   - Log in using Windows authentication, right-click on the server (at the top of the list), go to properties → Security, and change to SQL Server and Windows Authentication mode. Click OK. If this is already done, skip this step.
4. Setting Up the Database
    - In SQL Server Management Studio, create a database and a login with SQL Server Authentication. Assign the sysadmin role and map the user to your database with db_owner role.

### Setting Up the Website
At this point we need to set up the website.  We will need to clone the repository and install the requirements from `requirements.txt`.  We will also need to set up the database schema and load the menu data.  Once this is complete, we need to ensure that the website is accessible from the public internet.

- Clone the repository and navigate into it. Install requirements from `requirements.txt` (using `pip install -r requirements.txt`).
- Rename `.env.sample` to `.env` and input your database name, username, and password. Leave the Port field blank.
- Use `python manage.py makemigrations` and `python manage.py migrate` to apply the schema.
- Load the menu data with `python manage.py loaddata menu_data.json`.

#### Making the Website Public
**In the VM:**
- Configure Windows Defender Firewall to allow inbound rules for all local ports. (A quick Google search will show you how to do this.)
- 
- Add a new inbound security rule in the Network Security Group to allow traffic on port 8000.

## Running the Server
- Run `python manage.py runserver 0.0.0.0:8000` in the VM.

## Accessing the Website
- Use the VM's public IP address followed by `:8000` to access the website from anywhere.