# Restaurant Web Application

## Overview

This project is a web application for restaurant management and browsing. It utilizes Python 3.9.0 and integrates with SQL Server for data management, including handling menus, customer reviews, and reservations.

## Prerequisites

- Python 3.9.0: Essential for compatibility with the project's dependencies.
- SQL Server: Used for database storage and management.

## Installation

1. **Clone the Repository**

    ```bash
    git clone https://github.com/molin6/restaurantweb.git
    ```

2. **Navigate to Project Directory**

    ```bash
    cd restaurantweb
    ```

3. **Install Dependencies**

    Ensure you're using Python 3.9.0 for this project:

    ```bash
    pip install -r requirements.txt
    ```

## Database Setup

1. **Environment Configuration**

    Configure your database connection by setting environment variables. Create a `.env` file in the project root and define the following variables:
    
    ```
    DATABASE_URL="Your_SQL_Server_Connection_String"
    ```

2. **Make Migrations**

    Generate the database schema:

    ```bash
    python manage.py makemigrations
    ```

3. **Migrate**

    Apply migrations to the database:

    ```bash
    python manage.py migrate
    ```

4. **Load Initial Data (Optional)**

    If you have initial data to load into the database:

    ```bash
    python manage.py loaddata <fixture_name>
    ```

## Running the Application

Start the web server:

```bash
python manage.py runserver
```
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

