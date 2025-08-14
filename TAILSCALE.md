# SALT Tailscale Setup Guide

## Overview
With Tailscale, you can play from an LGS, tournament, or over Spelltable.

## Part 1: Account Setup and Configuration

### Step 1: Create Tailscale Account and Enable HTTPS
**Important**: Do this BEFORE installing Tailscale on any devices. Once installed on your server, changing this setting may require a restart to pick up.

1. Go to https://tailscale.com/start
2. Create a free account using Google/GitHub/Microsoft.
3. After account creation, go to https://login.tailscale.com/admin/dns
4. In the **"HTTPS Certificates"** section, **enable the "HTTPS certificates" toggle**

## Part 2: Server Setup

1. Install Tailscale from https://tailscale.com/download
2. After installation, Tailscale should appear in your menu bar
3. Sign into Tailscale from your server machine.
4. After authentication, you'll see "Connected" in the menu bar and your "This Device" IP address

Your machine now has a Tailscale IP address and is part of your private network!

### Step 3: Set a Hostname (Optional but Recommended)
1. Go to https://login.tailscale.com/admin/machines
2. Find your serving machine in the device list
3. Click the "..." menu next to your device and select "Edit device name"
4. Change it to "salt" and click "Save"

Now your server will be available as `https://salt.tailxxxxxx.ts.net` instead of just an IP address!

### Step 4: Run the Server
1. Run the binary you downloaded.
You should see something like
```
SALT Server

Remote Access (via Tailscale):
  https://salt.tailxxxxxx.ts.net:8443

Remote Access QR Code:
Scan with mobile device (Remote Access):

<QR Code>

Local Network:
  http://192.xxx.xx.xxx:8080

Local Network QR Code:
Scan with mobile device (Local Network):

<QR Code>
```
If tailscale is unavailable, the server will only generate the local network link.
If the server is unable to generate HTTPS certificates, it will still connect to Tailscale, but serve HTTP. Things will still work, your devices will show a security warning.

## Part 3: Mobile Setup

### Step 1: Setup Tailscale
1. Open the App Store (iPhone) or Android equivalent
2. Search for "Tailscale"
3. Install the official Tailscale app (by Tailscale Inc.)

### Step 2: Sign In and Connect
1. Open the Tailscale app and tap "Sign In"
2. After signing in, you'll see a toggle switch. turn it **ON**
3. You should see your server listed as "salt" or an IP address if you didn't set a hostname

### Step 3: Test the Connection
1. Open a browser on your device
2. Go to: `https://salt.tailxxxxxx.ts.net:8443` by copying the server address or scanning the QR code.
3. You should see the SALT lobby!

### Sharing with Friends
To let friends connect to your server use one of the below options. You need to do this setup once per person.

**Option 1: Device Sharing (Recommended)**
1. Have your friends do Part 3: Mobile Setup up until connecting to the server
2. Go to https://login.tailscale.com/admin/machines
3. Click "Share" on your SALT server (via the "..." menu)
4. They use the shared link to add your server to their tailnet
5. Share the QR code for your server from your own SALT page. They should now be able to connect

**Option 2: Account Sharing**
1. Have your friends do `Part 3: Mobile Setup` up until connecting to the server
2. Log them in with your own account credentials
3. Share the QR code for your server
4. Tailscale free tier supports up to 100 devices. You can remove their device from your admin panel

**Option 3: Invite to Your Tailnet (Not recommended)**
1. Go to https://login.tailscale.com/admin/users
2. Click "Invite users"
3. Enter your friend's email. They'll get setup instructions. Approve their join request
4. Share the QR code for your server from your own SALT client
5. Tailscale free tier supports up to 3 accounts in a network so someone in a pod of 4 will have use another method

## Troubleshooting

### Can't Connect from Mobile
1. **Check both devices are connected**:
   - Server: `tailscale status` should show your connection status
   - Mobile: Tailscale app should show "Connected" with green indicator

2. **Try the IP address instead of hostname**:
   - Use `https://100.x.x.x:8443` instead of `https://salt.tailxxxxxx.ts.net`

3. **Restart Tailscale on both devices**:
   - Mac/Linux: `sudo tailscale down && sudo tailscale up`
   - Windows: Exit and reopen the menu tray icon
   - Mobile: Toggle Tailscale off and on in the app

### "Tailscale not connected" on Server Start

Restart tailscale as described above

### Performance Issues
- Tailscale adds 5-50ms latency
- First connection might be slower as it establishes direct connection and downloads uncached resources
- Check `tailscale status` - if you see "relay" connections, devices might be behind restrictive firewalls

## Security Notes
- ✅ All traffic is encrypted end-to-end
- ✅ Only devices in your Tailnet can access your server
- ⚠️ Anyone with access to your Tailnet can access your server

## Getting Help
- **Tailscale Documentation**: https://tailscale.com/kb/
