================================================================================
                    LANGFUSE QUICK START GUIDE
================================================================================

PURPOSE: Debug LangFlow flows with LM Studio using LangFuse traces
LOCATION: C:\d\langfuse-setup\
ACCESS: http://localhost:3000

================================================================================
                        QUICK COMMANDS
================================================================================

START LANGFUSE:
    cd c:\d\langfuse-setup
    docker-compose up -d

STOP LANGFUSE:
    docker-compose down

RESTART:
    docker-compose restart

CHECK STATUS:
    docker-compose ps

VIEW LOGS:
    docker-compose logs -f langfuse-server

================================================================================
                        FIRST TIME SETUP
================================================================================

1. Open Command Prompt
2. Run:
   cd c:\d\langfuse-setup
   docker-compose up -d

3. Wait 30-60 seconds

4. Open browser to: http://localhost:3000

5. Create account (use any email, even fake ones work)

6. Get API keys from Settings:
   - Public Key (pk-lf-...)
   - Secret Key (sk-lf-...)
   - Host: http://localhost:3000

7. Add to Windows Environment Variables:
   LANGFUSE_PUBLIC_KEY=pk-lf-YOUR-KEY
   LANGFUSE_SECRET_KEY=sk-lf-YOUR-KEY
   LANGFUSE_HOST=http://localhost:3000

8. Restart LangFlow

9. Run flows and view traces at http://localhost:3000

================================================================================
                        TROUBLESHOOTING
================================================================================

PROBLEM: Page won't load
FIX: Make sure Docker Desktop is running, then run:
     docker-compose up -d

PROBLEM: Port 3000 in use
FIX: Edit docker-compose.yml, change "3000:3000" to "3001:3000"
     Access at http://localhost:3001

PROBLEM: No traces appearing
FIX: Check API keys are correct and LANGFUSE_HOST is http (not https)
     Restart LangFlow after setting environment variables

PROBLEM: Database errors
FIX: Stop and reset:
     docker-compose down
     docker volume rm langfuse-setup_langfuse-db-data
     docker-compose up -d

================================================================================
                        FILES IN THIS FOLDER
================================================================================

PREREQUISITES.txt               - What you need before starting (Docker, etc.)
docker-compose.yml              - Docker container configuration
.env                            - Environment variables and secrets
GUIDE.md                        - Full detailed guide (open in browser/editor)
QUICK-REFERENCE-ENV-VARS.md     - Quick guide for API keys & env vars setup
README.txt                      - This file (quick reference)

================================================================================
                        HELPFUL INFO
================================================================================

- LangFuse runs in the background even after closing the terminal
- Data persists between restarts (stored in Docker volume)
- To completely remove all data: docker-compose down && docker volume rm langfuse-setup_langfuse-db-data
- Read GUIDE.md for detailed step-by-step instructions with screenshots context

================================================================================
STRUGGLING WITH ENV VARS OR API KEYS? → Open QUICK-REFERENCE-ENV-VARS.md

For full instructions, open GUIDE.md in a markdown viewer or text editor
================================================================================
