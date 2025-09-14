# Sentient ROMA Setup on Windows

This guide will help you set up **Sentient ROMA** on a Windows machine using Docker and VS Code.

---

## Prerequisites

1. **Docker Desktop**
   - Download and install: [Docker Desktop](https://www.docker.com/products/docker-desktop)
   - Make sure Docker is running after installation.
   - verify installation
  ```
  docker --version
docker compose version
 ```

2. **Git**
   - Download and install: [Git](https://git-scm.com/downloads)
   - Verify installation:

     ```
     git --version
     ```

3. **VS Code (optional but recommended)**
   - [VS Code](https://code.visualstudio.com/)
   - Install the **Docker** and **Git** extensions in VS Code.

---

## Step 1: Clone the Repository

Open **PowerShell** or **VS Code terminal** and run:

```
git clone https://github.com/sentient-agi/ROMA.git
cd ROMA
 ```

## Step 2: Set Up `.env` Files

Copy the example .env file to a real .env file:

### Backend `.env`

```
copy .env.example .env
 ```

## Step 3: Build and Run the Containers

Open **PowerShell** or terminal in the project root and run:

```
docker compose down -v   # Clean up any old containers
docker compose up --build
 ```
The first run may take some time to build.
You should see frontend and backend starting without errors.

## Step 6: Verify Containers Are Running

Run the following command to check active containers:

```
docker ps
```
You should see output similar to this:
```CONTAINER ID   IMAGE               PORTS
xxxxxxx        sentient-backend    0.0.0.0:5000->5000/tcp
xxxxxxx        sentient-frontend   0.0.0.0:3000->3000/tcp
```

## Step 7: Test the Application

1. Open your browser and go to: [http://localhost:3000](http://localhost:3000)
2. The frontend should load and connect to the backend automatically.
3. If you see **“Backend disconnected”**, check the backend logs:

```
docker logs <backend_container_name>
```


## Step 8: Useful Docker Commands

Stop containers:

```
docker compose down
```
Start containers in the background:
```
docker compose up -d
```

Restart containers:
```
docker compose restart
```

Rebuild containers after code changes:
```
docker compose down -v
docker compose up --build
```

⚠️ Use these commands to manage your containers efficiently during development.

## Tips

- Always use **LF line endings** for shell scripts on Windows.
- Ensure **`.env` files`** are correctly set.
- Use `docker compose logs` to debug issues.
- For frontend connection issues, confirm `VITE_API_URL` points to `http://localhost:5000`.


