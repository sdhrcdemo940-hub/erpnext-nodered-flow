## Node-RED ERPNext Sync - Daily Log

### 2026-09-15

**Issue:** Node-RED unable to reach ERPNext API
- Initial error: "no response from server" → "getaddrinfo ENOTFOUND"
- Root cause: Node-RED on default bridge network, ERPNext on `frappe_docker_default` network

**Actions Taken:**
1. ✅ Fixed flows.json → enabled `insecureHTTPParser`, added 10s timeouts, set `senderr: true`
2. ✅ Updated base URL from `localhost:8080` → `frappe_docker-frontend-1:8080`
3. ⏳ Restarted Node-RED on correct Docker network (`frappe_docker_default`)
   - Hit permission error on `/data` volume mount
   - In progress: Resolve EACCES and restart container

**Next Steps:**
- Fix Docker permissions on `/data` directory
- Verify Node-RED can reach `frappe_docker-frontend-1:8080` 
- Test flow with sample CSV at `/data/test.csv`
- Confirm Stock Entry sync workflow completes without errors

**Test CSV:**
```
item_code,qty,warehouse
ITEM-001,100,Stores - SD
ITEM-002,50,Stores - SD
```

**Credentials Config (in "Config + Map CSV Row" function):**
- `ERP_BASE_URL`: http://frappe_docker-frontend-1:8080
- `ERP_API_KEY` / `ERP_API_SECRET`: Update with real ERPNext credentials
- `DEFAULT_WAREHOUSE`: Stores - SD
