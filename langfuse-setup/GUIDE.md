# LangFuse Setup Guide - Simple & Clear

> This guide helps you run LangFuse on your PC to debug LangFlow flows and trace tool calls from local models (LM Studio).

---

## Quick Overview - What You'll Do

```
1. Start Docker Container → LangFuse runs at localhost:3000
                            ↓
2. Create Account       → Sign up in web browser
                            ↓
3. Get API Keys         → Settings → API Keys → Copy pk-lf-... and sk-lf-...
                            ↓
4. Set Windows Env Vars → Win+R → sysdm.cpl → Advanced → Environment Variables
                            ↓
5. Restart LangFlow     → Close and reopen so it reads the new variables
                            ↓
6. View Traces          → Run flows, see them at localhost:3000/traces
```

**Time Required:** 10-15 minutes for first-time setup

---

## What You'll Get

- LangFuse running at: **http://localhost:3000**
- Traces from your LangFlow runs
- Deep insights into tool calls and agent loops
- Easy debugging when flows fail

---

## Step 1: Start LangFuse (First Time)

### Open Command Prompt / PowerShell

1. Press `Win + R`
2. Type `cmd` and press Enter
3. Navigate to the setup folder:
   ```bash
   cd c:\d\langfuse-setup
   ```

### Start the Docker Containers

Run this command:
```bash
docker-compose up -d
```

**What this does:**
- `-d` means "run in background"
- Starts LangFuse and its database
- Takes 30-60 seconds the first time (downloads images)

### Check It's Running

```bash
docker-compose ps
```

You should see:
- `langfuse-server` - Status: Up
- `langfuse-db` - Status: Up

---

## Step 2: Access LangFuse Web UI

1. Open your web browser
2. Go to: **http://localhost:3000**
3. You'll see the LangFuse login page

### Create Your Account (First Time Only)

1. Click **"Sign Up"** or **"Create Account"**
2. Enter your email (can be fake like `me@localhost.com`)
3. Enter a password
4. Click **"Create Account"**
5. You'll be logged in automatically

---

## Step 3: Get Your API Keys (DETAILED)

These keys let LangFlow send traces to LangFuse. This is the most important step!

### ⚠️ IMPORTANT: Where to Find API Keys in LangFuse

```
Web Browser (localhost:3000)
    │
    ├─ Left Sidebar
    │   ├─ Dashboard
    │   ├─ Traces
    │   ├─ Sessions
    │   ├─ ...
    │   └─ ⚙️ Settings  ← CLICK HERE
    │
    └─ Settings Page Opens
        ├─ Tab: General
        ├─ Tab: Team
        ├─ Tab: API Keys  ← CLICK HERE
        │
        └─ "Create new API key" button ← CLICK HERE
            │
            └─ Dialog shows your keys:
                ├─ Public Key:  pk-lf-xxxxx...
                └─ Secret Key:  sk-lf-xxxxx... (COPY NOW - shown only once!)
```

### Finding Your API Keys - Step by Step:

**After you log in to http://localhost:3000:**

1. **Look at the top-left sidebar** - you'll see menu items like:
   - Dashboard
   - Traces
   - Sessions
   - Users
   - (etc.)

2. **Scroll down in the left sidebar** until you find **"Settings"**
   - It might be near the bottom
   - Has a gear/cog icon ⚙️

3. **Click "Settings"** - this opens the settings page

4. **In the Settings page**, look for tabs or menu items:
   - You should see options like "General", "Team", **"API Keys"**, etc.
   - **Click on "API Keys"** tab

5. **On the API Keys page:**
   - You'll see a button that says **"Create new API key"** or **"+ New API key"**
   - Click that button

6. **A dialog/form appears** asking:
   - **Name**: Give it a name like "LangFlow Integration" (helps you remember what it's for)
   - Click **"Create"** or **"Generate"**

7. **IMPORTANT - Copy your keys NOW!**
   - You'll see a screen showing:
     - **Secret Key**: A long string starting with `sk-lf-...` (this is shown ONLY ONCE!)
     - **Public Key**: Another string starting with `pk-lf-...`
   - **Copy BOTH keys immediately** - the secret key won't be shown again!

### What Your Keys Look Like:

```
Public Key:  pk-lf-1234567890abcdef1234567890abcdef
Secret Key:  sk-lf-9876543210zyxwvu9876543210zyxwvu
Host:        http://localhost:3000
```

### Save These Keys Somewhere Safe!

**Do this NOW before closing the dialog:**

1. Open Notepad (press `Win + R`, type `notepad`, press Enter)
2. Paste your keys like this:

```
LANGFUSE_PUBLIC_KEY=pk-lf-YOUR-ACTUAL-PUBLIC-KEY-HERE
LANGFUSE_SECRET_KEY=sk-lf-YOUR-ACTUAL-SECRET-KEY-HERE
LANGFUSE_HOST=http://localhost:3000
```

3. Save this file as `langfuse-keys.txt` on your Desktop

**You'll need these in Step 4!**

### Alternative Location for API Keys:

Some LangFuse versions have the API keys under:
- **Settings → Projects → (Your Project Name) → API Keys**

If you can't find "API Keys" directly under Settings, look for a "Projects" section first.

---

## Step 4: Set Environment Variables (DETAILED)

Now we'll tell LangFlow to send traces to your local LangFuse instance by setting Windows environment variables.

### Why Environment Variables?

Environment variables are settings that programs can read. LangFlow automatically looks for these variables to connect to LangFuse. Once you set them, LangFlow will automatically send traces - no code changes needed!

---

## METHOD 1: System-Wide Environment Variables (RECOMMENDED)

This makes LangFlow always connect to LangFuse, no matter how you start it.

### Step-by-Step for Windows 10/11:

**1. Open Environment Variables Window:**

- Press `Windows Key + R` (opens "Run" dialog)
- Type: `sysdm.cpl`
- Press `Enter`
- A window called "System Properties" opens

**2. Navigate to Environment Variables:**

- You'll see several tabs at the top
- Click the **"Advanced"** tab
- At the bottom, click the button **"Environment Variables..."**
- A new window opens with two sections:
  - Top: "User variables for [YourName]" ← **We'll use this section**
  - Bottom: "System variables" (ignore this)

**3. Add LANGFUSE_PUBLIC_KEY:**

- In the **"User variables"** section (top half), click **"New..."** button
- A small dialog opens with two fields:
  - **Variable name:** Type exactly: `LANGFUSE_PUBLIC_KEY`
  - **Variable value:** Paste your public key (the one starting with `pk-lf-...`)
- Click **"OK"**

**4. Add LANGFUSE_SECRET_KEY:**

- Click **"New..."** again in the User variables section
- **Variable name:** Type exactly: `LANGFUSE_SECRET_KEY`
- **Variable value:** Paste your secret key (the one starting with `sk-lf-...`)
- Click **"OK"**

**5. Add LANGFUSE_HOST:**

- Click **"New..."** one more time
- **Variable name:** Type exactly: `LANGFUSE_HOST`
- **Variable value:** Type exactly: `http://localhost:3000`
  - **IMPORTANT:** Use `http` NOT `https`
  - **IMPORTANT:** No trailing slash at the end
- Click **"OK"**

**6. Close All Windows:**

- Click **"OK"** on the Environment Variables window
- Click **"OK"** on the System Properties window

**7. Restart LangFlow:**

- **IMPORTANT:** Close LangFlow completely if it's running
- Close any terminals/command prompts where LangFlow was started
- Open a NEW terminal/command prompt
- Start LangFlow fresh

**Why restart?** Environment variables are only read when a program starts. Existing running programs won't see the new variables.

### Verify Your Environment Variables Are Set:

Open a NEW Command Prompt and type:

```bash
echo %LANGFUSE_PUBLIC_KEY%
echo %LANGFUSE_SECRET_KEY%
echo %LANGFUSE_HOST%
```

You should see your keys and host printed. If you see `%LANGFUSE_PUBLIC_KEY%` (the variable name itself), it's not set correctly.

---

## METHOD 2: Set Variables When Starting LangFlow

If you don't want system-wide variables, you can set them each time you start LangFlow.

### Option A: Using Command Prompt

Before starting LangFlow, run these commands:

```bash
set LANGFUSE_PUBLIC_KEY=pk-lf-YOUR-ACTUAL-PUBLIC-KEY-HERE
set LANGFUSE_SECRET_KEY=sk-lf-YOUR-ACTUAL-SECRET-KEY-HERE
set LANGFUSE_HOST=http://localhost:3000
```

Then start LangFlow in the same command prompt window.

**Note:** These only work in that specific terminal window and disappear when you close it.

### Option B: Using PowerShell

Before starting LangFlow, run these commands:

```powershell
$env:LANGFUSE_PUBLIC_KEY="pk-lf-YOUR-ACTUAL-PUBLIC-KEY-HERE"
$env:LANGFUSE_SECRET_KEY="sk-lf-YOUR-ACTUAL-SECRET-KEY-HERE"
$env:LANGFUSE_HOST="http://localhost:3000"
```

Then start LangFlow in the same PowerShell window.

### Option C: Create a Startup Script

Create a file called `start-langflow-with-langfuse.bat` with:

```batch
@echo off
set LANGFUSE_PUBLIC_KEY=pk-lf-YOUR-ACTUAL-PUBLIC-KEY-HERE
set LANGFUSE_SECRET_KEY=sk-lf-YOUR-ACTUAL-SECRET-KEY-HERE
set LANGFUSE_HOST=http://localhost:3000

echo LangFuse environment variables set!
echo Starting LangFlow...

REM Add your LangFlow start command here
REM For example:
REM langflow run
REM or
REM python -m langflow run

cmd /k
```

Double-click this file to start a command prompt with the variables already set.

---

## METHOD 3: LangFlow .env File (If Supported)

Some LangFlow installations support a `.env` file:

1. Navigate to your LangFlow directory
2. Create a file named `.env` (starts with a dot)
3. Add these lines:

```
LANGFUSE_PUBLIC_KEY=pk-lf-YOUR-ACTUAL-PUBLIC-KEY-HERE
LANGFUSE_SECRET_KEY=sk-lf-YOUR-ACTUAL-SECRET-KEY-HERE
LANGFUSE_HOST=http://localhost:3000
```

4. Save and restart LangFlow

---

## Quick Troubleshooting for Environment Variables:

### Problem: Variables not working

**Checklist:**
- [ ] Did you restart LangFlow after setting variables?
- [ ] Did you close ALL terminal windows and open a NEW one?
- [ ] Did you spell the variable names EXACTLY right? (case-sensitive)
- [ ] Is LANGFUSE_HOST set to `http://` (not `https://`)?
- [ ] Did you paste the FULL keys including `pk-lf-` and `sk-lf-` prefixes?

### How to Check Variables Are Set:

**In Command Prompt:**
```bash
echo %LANGFUSE_PUBLIC_KEY%
```

**In PowerShell:**
```powershell
echo $env:LANGFUSE_PUBLIC_KEY
```

If you see the actual key value, it's set correctly!
If you see the variable name itself or nothing, it's not set.

---

## Step 5: View Your Traces

### Run a LangFlow Flow

1. Execute any flow in LangFlow (with LangFuse configured)
2. Wait for it to complete

### Check LangFuse UI

1. Go back to **http://localhost:3000**
2. Click **"Traces"** in the sidebar
3. You'll see your flow runs listed!

### Dive Into Details

Click on any trace to see:
- All LLM calls made
- Tool calls and their results
- Token usage and costs
- Timing information
- Error messages (if any)

### Debug Agent Loops

Look for:
- Repeated tool calls (shows loops)
- Failed tool executions
- Malformed responses from tools
- Timing issues (slow calls)

---

## Daily Use: Quick Commands

### Start LangFuse (When Your PC Restarts)

```bash
cd c:\d\langfuse-setup
docker-compose up -d
```

### Stop LangFuse (Save Resources)

```bash
cd c:\d\langfuse-setup
docker-compose down
```

### Restart LangFuse (If Something Goes Wrong)

```bash
cd c:\d\langfuse-setup
docker-compose restart
```

### Check If It's Running

```bash
docker-compose ps
```

### View Logs (If Something's Not Working)

```bash
docker-compose logs -f langfuse-server
```

Press `Ctrl + C` to stop viewing logs.

---

## Troubleshooting

### Problem: "Cannot connect" or page won't load

**Solution:**
1. Check Docker Desktop is running
2. Run: `docker-compose ps` to see if containers are up
3. If not running: `docker-compose up -d`
4. Wait 30 seconds and try again

### Problem: "Port 3000 already in use"

**Solution:**
1. Another app is using port 3000
2. Edit [docker-compose.yml](docker-compose.yml) in this folder
3. Change `"3000:3000"` to `"3001:3000"` (or any other port)
4. Access at `http://localhost:3001` instead

### Problem: LangFlow traces not appearing

**Solution:**
1. Double-check your API keys are correct
2. Make sure `LANGFUSE_HOST=http://localhost:3000` (not https)
3. Restart LangFlow after setting environment variables
4. Check LangFlow logs for connection errors

### Problem: Forgot your LangFuse password

**Solution:**
1. Stop containers: `docker-compose down`
2. Delete the database: `docker volume rm langfuse-setup_langfuse-db-data`
3. Start again: `docker-compose up -d`
4. Create a new account (you'll lose old traces)

### Problem: Database errors or corruption

**Solution:**
1. Stop containers: `docker-compose down`
2. Remove the database volume:
   ```bash
   docker volume rm langfuse-setup_langfuse-db-data
   ```
3. Start fresh: `docker-compose up -d`

---

## Advanced: Update LangFuse

To get the latest version:

```bash
cd c:\d\langfuse-setup
docker-compose pull
docker-compose up -d
```

---

## Data Storage

Your traces are stored in a Docker volume:
- Volume name: `langfuse-setup_langfuse-db-data`
- Persists even when containers stop
- Survives PC restarts

To completely remove all data:
```bash
docker-compose down
docker volume rm langfuse-setup_langfuse-db-data
```

---

## Summary Cheat Sheet

| Action | Command |
|--------|---------|
| Start | `cd c:\d\langfuse-setup && docker-compose up -d` |
| Stop | `docker-compose down` |
| Restart | `docker-compose restart` |
| Check Status | `docker-compose ps` |
| View Logs | `docker-compose logs -f` |
| Access UI | Open **http://localhost:3000** |

---

## Need Help?

- LangFuse Docs: https://langfuse.com/docs
- LangFlow + LangFuse: https://docs.langflow.org/
- Docker Issues: Make sure Docker Desktop is running

---

**Last Updated:** 2025-11-04
