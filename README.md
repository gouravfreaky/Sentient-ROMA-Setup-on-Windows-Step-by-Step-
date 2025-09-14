# Sentient ROMA Setup on Windows

This guide will help you set up **Sentient ROMA** on a Windows machine using Docker and VS Code.

---

## Prerequisites

1. **Docker Desktop**
   - Download and install: [Docker Desktop](https://www.docker.com/products/docker-desktop)
   - Make sure Docker is running after installation.

2. **Git**
   - Download and install: [Git](https://git-scm.com/downloads)
   - Verify installation:

     ```powershell
     git --version
     ```

3. **VS Code (optional but recommended)**
   - [VS Code](https://code.visualstudio.com/)
   - Install the **Docker** and **Git** extensions in VS Code.

---

## Step 1: Clone the Repository

Open **PowerShell** or **VS Code terminal** and run:

```powershell
git clone https://github.com/sentient-agi/ROMA.git
cd ROMA
 ```

## Step 2: Set Up `.env` Files

Create or edit `.env` files for **backend** and **frontend**.

### Backend `.env`

```env
PORT=5000
HOST=0.0.0.0
OPENAI_API_KEY=your_openai_api_key_here
 ```

## Step 3: Fix Windows Line Endings for Backend Scripts

Windows can introduce **CRLF line endings**, which break Linux containers.

### Option A: Using VS Code

1. Open each backend `.sh` file (`startup.sh`, `entrypoint.sh`, etc.) in VS Code.
2. In the bottom-right corner of VS Code, change `CRLF` → `LF`.
3. Save the file.

### Option B: Using PowerShell to Fix All Scripts at Once

Run this in the project root:

```powershell
Get-ChildItem -Path . -Recurse -Include *.sh | ForEach-Object {
    (Get-Content $_.FullName) -replace "`r","" | Set-Content -NoNewline $_.FullName
}
 ```

⚠️ This will remove all Windows carriage returns (\r) from your shell scripts to ensure they run correctly inside Linux containers.

## Step 4: Ensure `docker-compose.yml` Is Correct

Check that the backend service has **ports exposed**:

```yaml
services:
  backend:
    build: ./backend
    env_file:
      - .env
    ports:
      - "5000:5000"
  frontend:
    build: ./frontend
    env_file:
      - .env
    ports:
      - "3000:3000"
    depends_on:
      - backend
 ```

⚠️ Make sure the backend ports match the PORT value in your backend .env file and the frontend is set to connect to the correct backend URL.

## Step 5: Build and Run the Containers

Open **PowerShell** or terminal in the project root and run:

```powershell
docker compose down -v   # Clean up any old containers
docker compose up --build
 ```
The first run may take some time to build images.
You should see frontend and backend starting without errors.

## Step 6: Verify Containers Are Running

Run the following command to check active containers:

```powershell
docker ps
```
You should see output similar to this:
```CONTAINER ID   IMAGE               PORTS
xxxxxxx        sentient-backend    0.0.0.0:5000->5000/tcp
xxxxxxx        sentient-frontend   0.0.0.0:3000->3000/tcp
```
