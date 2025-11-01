# NiFi CI/CD Core - Step by Step Guide

## Step 1: Setup
Generate a secure password for NiFi.

```bash
make setup
```

**What happens:**
- Generates a random password
- Saves it to your `.env` file

**Output:**
```
🔑 Generating a password...
✅ Password generated.
🔐 Password updated in .env file.
```

---

## Step 2: Start Services
Start NiFi and NiFi Registry.

```bash
make up
```

**What happens:**
- Runs `make setup` automatically (generates new password)
- Starts Docker containers
- Shows your credentials and URLs

**Output:**
```
🔑 Generating a password...
✅ Password generated.
🔐 Password updated in .env file.
🚀 Starting NiFi and NiFi Registry...
✅ Services started.
```

**⏰ Wait 2-3 minutes** for NiFi to fully start before logging in.

---

## Step 3: Get Your Credentials
Display your username, password, and access URLs.

```bash
make echo
```

**Output:**
```
NIFI_USERNAME: admin
NIFI_PASSWORD: d6050b8543e409de054cc0d43d56ae34
✅ NiFi:          https://localhost:8443/nifi
✅ NiFi Registry: http://localhost:18080/nifi-registry
🔗 Access the services using the above URLs.
```

**Copy these credentials** to log into NiFi.

---

## Step 4: Access NiFi
Open your browser and go to:

**https://localhost:8443/nifi**

Login with:
- **Username:** `admin`
- **Password:** (from `make echo`)

---

## Step 5: Check Logs (Optional)
Monitor NiFi startup progress.

```bash
make logs-nifi
```

**Look for this message:**
```
NiFi has started
```

Press `Ctrl+C` to exit logs.

---

## Step 6: Stop Services
When you're done, stop all services.

```bash
make down
```

**Output:**
```
🛑 Stopping NiFi and NiFi Registry...
✅ Services stopped.
```

---

## Complete Workflow Example

```bash
# 1. Start everything
make up

# 2. Wait 2-3 minutes, then get credentials
make echo

# 3. Open browser: https://localhost:8443/nifi
#    Login with credentials from step 2

# 4. When done, stop services
make down
```

---

## Other Useful Commands

### View all logs
```bash
make logs
```

### View NiFi Registry logs
```bash
make logs-registry
```

### Start and show credentials (shortcut)
```bash
make all
```

---

## Troubleshooting

### Can't login? Reset credentials:
```bash
make down
docker volume rm nifi-ci-cd-core_nifi_conf
make up
# Wait 2-3 minutes
make echo
```

### Check if NiFi is ready:
```bash
make logs-nifi
# Look for "NiFi has started"
```