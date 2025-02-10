# Restoring a .tar Backup in PostgreSQL using pgAdmin 4

## Overview
This guide explains how to restore a **.tar** format PostgreSQL backup file using **pgAdmin 4**. A `.tar` backup is created using `pg_dump` and contains a structured database backup.

## Prerequisites
- **PostgreSQL** installed on your system
- **pgAdmin 4** installed
- A `.tar` backup file (e.g., `world.tar`)

## Steps to Restore a `.tar` Backup in pgAdmin 4

### **Step 1: Open pgAdmin 4**
1. Launch **pgAdmin 4**.
2. Connect to your PostgreSQL server.

### **Step 2: Create a Database (If Not Exists)**
If the database you want to restore does not exist:
1. Right-click on **Databases** → Click **Create** → **Database**.
2. Enter a name (e.g., `World`).
3. Click **Save**.

### **Step 3: Start the Restore Process**
1. Right-click on the **database** where you want to restore the backup.
2. Select **Restore...** from the menu.
3. In the **Restore Database** window:
   - **Filename**: Click **...** and select your `.tar` backup file (e.g., `C:\Users\kumar\Downloads\world.tar`).
   - **Format**: Ensure it is set to `Custom or tar`.
4. Click **Restore**.

### **Step 4: Verify the Restoration**
1. Open the **Query Tool** in pgAdmin.
2. Run:
   ```sql
   SELECT table_name FROM information_schema.tables WHERE table_schema = 'public';
   ```
3. Check if the tables from the backup exist.

## Alternative: Restore Using `pg_restore`
If pgAdmin fails, you can restore via the command line:
```sh
pg_restore --host "localhost" --port "5432" --username "postgres" --dbname "World" --verbose "C:\Users\kumar\Downloads\world.tar"
```
Ensure PostgreSQL's `bin` folder is added to the system `PATH`.

## Common Issues & Fixes
- **Error: `input file does not appear to be a valid archive`**
  - Ensure the backup was created using:
    ```sh
    pg_dump -F c -f world.tar -U postgres -d World
    ```
  - If the backup is a `.sql` file, use `psql` instead of `pg_restore`:
    ```sh
    psql -U postgres -d World -f "C:\Users\kumar\Downloads\world.sql"
    ```

## Conclusion
By following these steps, you can easily restore a PostgreSQL `.tar` backup using pgAdmin 4 or `pg_restore`.

### **Author**
- **Kumar Verma** | [GitHub](https://github.com/DataWizVerma) | [LinkedIn](https://www.linkedin.com/in/kumar-verma2002/)

