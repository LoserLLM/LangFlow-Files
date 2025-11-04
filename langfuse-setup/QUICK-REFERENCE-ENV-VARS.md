# Quick Reference: Setting Environment Variables for LangFuse

## Part 1: Get Your API Keys from LangFuse

### Where to Click:

1. Open **http://localhost:3000** in browser
2. Click **"Settings"** in left sidebar (has ⚙️ icon)
3. Click **"API Keys"** tab
4. Click **"Create new API key"** button
5. Give it a name like "LangFlow"
6. **COPY BOTH KEYS NOW** (secret key only shown once!)

### What You'll Copy:

```
Public Key:  pk-lf-[long string of letters and numbers]
Secret Key:  sk-lf-[long string of letters and numbers]
```

---

## Part 2: Set Windows Environment Variables

### The Fastest Way:

1. Press `Windows Key + R`
2. Type: `sysdm.cpl` and press Enter
3. Click **"Advanced"** tab
4. Click **"Environment Variables..."** button at bottom
5. In the **top section** (User variables), click **"New..."**
6. Add these THREE variables one at a time:

#### Variable 1:
- Name: `LANGFUSE_PUBLIC_KEY`
- Value: `pk-lf-YOUR-ACTUAL-KEY-HERE`
- Click OK

#### Variable 2:
- Name: `LANGFUSE_SECRET_KEY`
- Value: `sk-lf-YOUR-ACTUAL-KEY-HERE`
- Click OK

#### Variable 3:
- Name: `LANGFUSE_HOST`
- Value: `http://localhost:3000`
- Click OK

7. Click OK on all windows to close them

---

## Part 3: Restart LangFlow

**CRITICAL:** You MUST restart LangFlow for it to see the new variables!

1. Close LangFlow completely
2. Close any terminal/command prompt windows
3. Open a NEW terminal/command prompt
4. Start LangFlow again

---

## Verify It Worked

### Test 1: Check Variables Are Set

Open a NEW Command Prompt and type:

```cmd
echo %LANGFUSE_PUBLIC_KEY%
```

**Expected:** Should show your `pk-lf-...` key
**Problem:** If you see `%LANGFUSE_PUBLIC_KEY%`, it's not set correctly

### Test 2: Run a LangFlow Flow

1. Run any flow in LangFlow
2. Go to **http://localhost:3000**
3. Click **"Traces"** in the left sidebar
4. You should see your flow run listed!

---

## Common Mistakes

❌ **Mistake 1:** Not restarting LangFlow
✅ **Fix:** Close everything and start fresh

❌ **Mistake 2:** Using `https://` instead of `http://`
✅ **Fix:** Make sure LANGFUSE_HOST is `http://localhost:3000`

❌ **Mistake 3:** Typo in variable names
✅ **Fix:** Copy-paste the exact names from this guide

❌ **Mistake 4:** Forgetting to copy the `pk-lf-` or `sk-lf-` prefix
✅ **Fix:** Include the full key including the prefix

❌ **Mistake 5:** Adding variables to "System variables" instead of "User variables"
✅ **Fix:** Use the TOP section (User variables)

---

## Alternative: Set Variables Per-Session

If you don't want permanent variables, run these BEFORE starting LangFlow:

### In Command Prompt:
```cmd
set LANGFUSE_PUBLIC_KEY=pk-lf-YOUR-KEY-HERE
set LANGFUSE_SECRET_KEY=sk-lf-YOUR-KEY-HERE
set LANGFUSE_HOST=http://localhost:3000
```

### In PowerShell:
```powershell
$env:LANGFUSE_PUBLIC_KEY="pk-lf-YOUR-KEY-HERE"
$env:LANGFUSE_SECRET_KEY="sk-lf-YOUR-KEY-HERE"
$env:LANGFUSE_HOST="http://localhost:3000"
```

Then start LangFlow in the SAME window.

---

## Still Not Working?

1. Double-check spelling of variable names (case matters!)
2. Make sure you restarted LangFlow
3. Check LangFuse is running: `docker-compose ps`
4. Check LangFlow logs for connection errors
5. Verify keys are correct in LangFuse Settings → API Keys

---

**For full detailed guide, see [GUIDE.md](GUIDE.md)**
