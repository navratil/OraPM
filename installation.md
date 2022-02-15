# Troubleshooting

## ORA-29024: Certificate validation failure

OraPM is using Oracle Application Express API (APEX_WEB_SERVICE) for REST web services. The communication is excrypted (HTTPS) by default.
APEX must be configured to use the Oracle Wallet with the certification authority certificate (CA root). 

The [OraPM repository](https://app.orapm.com) is using https://letsencrypt.org as CA.

### 1) Create the wallet

See this detail article https://oracle-base.com/articles/misc/utl_http-and-ssl


### 2) Configure APEX to use the wallet either by

1) SQLcl/SQLPlus as SYS or SYSTEM user
``` sql
sql> ALTER SESSION SET CURRENT_SCHEMA = APEX_210200;    # must match your Oracle APEX version

sql> exec APEX_INSTANCE_ADMIN.SET_PARAMETER('WALLET_PATH', 'file:/home/oracle/mywallet');  # directory where the Oracle wallet is 
```

2) APEX GUI
- Login to the APEX / Administration services (no Workspace)
- Manage Instance / Instance Settings / Wallet tab
- Wallet Path
 
 Note: You can leave the password empty assuming the Wallet SSO file exists in that path (it does by default)
