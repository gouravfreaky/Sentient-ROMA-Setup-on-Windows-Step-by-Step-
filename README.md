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
---
## Step 2: Set Up `.env` Files

Create or edit `.env` files for **backend** and **frontend**.

### Backend `.env`

```env
PORT=5000
HOST=0.0.0.0
OPENAI_API_KEY=your_openai_api_key_here
