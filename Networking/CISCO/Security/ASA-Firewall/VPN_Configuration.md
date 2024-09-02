
# VPN Configuration Commands

## 1. Enable WebVPN
This command enables the WebVPN feature on the outside interface.

```bash
webvpn
enable outside
```

## 2. Configure Group Policy for VPN Users

### Group 1 Configuration
This block configures a group policy named `groupA` for users connecting through VPN. It specifies the use of SSL clientless VPN and associates a URL list with the group.

```bash
group-policy groupA internal
vpn-tunnel-protocol ssl-clientless
webvpn
url-list value Site1
exit
exit
```

### Group 2 Configuration
Similarly, this block configures another group policy named `groupB` for a different set of users, associating them with a different URL list.

```bash
group-policy groupB internal
vpn-tunnel-protocol ssl-clientless
webvpn
url-list value Site2
exit
exit
```

## 3. Configure User Accounts

### User 1 Configuration
This block creates a user named `john` with a password and associates this user with `groupA`.

```bash
username john password SecurePass1
username john attributes
vpn-group-policy groupA
exit
```

### User 2 Configuration
This block creates another user named `doe` with a password and associates this user with `groupB`.

```bash
username doe password SecurePass2
username doe attributes
vpn-group-policy groupB
exit
```

## 4. Configure Tunnel Group

### Tunnel Group Setup
This block configures a tunnel group for remote access VPNs, associating it with `groupA`.

```bash
tunnel-group tunnelA type remote-access
tunnel-group tunnelA general-attributes
default-group-policy groupA
```

## 5. Save Configuration
Finally, this command saves the configuration changes to the device memory.

```bash
wr memory
```
