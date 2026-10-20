# 🚀 s5h-autodelist

## 📌 Automatic IP Delist Guide for all.s5h.net RBL Blacklist
If your emails are unexpectedly quarantined by Outlook, Exchange Online, or other corporate mail servers, the root cause might be your mail server IP address listed on a global blacklist (RBL).

This guide explains how to automatically remove your IP address from the all.s5h.net (s5h.net) blacklist directly via the terminal without dealing with web forms.

### 🔍 1. Problem Detection (Checking if your IP is blacklisted)
You can check your IP status using `dig` or an external RBL checker tool:

```bash
dig +short your_reversed_ip.zen.spamhaus.org
```

If you see a code like `127.0.0.2` under `all.s5h.net` on an RBL checker, your IP is marked on this list.

### ⚡ 2. Automatic Delist Solution
The s5h.net blacklist service automatically removes an IP address if an HTTP request is sent directly from the listed server itself.

Log into your server via SSH and run the following command:
```bash
curl -4 http://www.usenix.org.uk/content/rblremove
```

If you prefer using `telnet`:
```bash
telnet www.usenix.org.uk 80
```
> than copy and paste codes below:
```text
GET /content/rblremove HTTP/1.1
Host: www.usenix.org.uk
```
> than enter twice...

### ✅ 3. Success Message
After running the command, you should receive a response similar to this:

```text
IP address YOUR_IP_ADDRESS removed successfully. Please allow up to one hour for database propagation.
```

### ⏳ 4. Propagation Time
- Once your IP address is successfully removed from the system, it generally takes up to 1 hour for global DNS/RBL databases to propagate.
- After propagation, you can send test emails to verify that quarantine issues with corporate providers like Outlook are resolved.
