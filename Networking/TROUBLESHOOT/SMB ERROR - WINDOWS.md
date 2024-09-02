
### Enable Unauthenticated Guest Access in Windows


````
- Press `Win + R`, type `gpedit.msc`, and press Enter to open the Local Group Policy Editor.
- Navigate to `Computer Configuration` > `Administrative Templates` > `Network` > `Lanman Workstation`.
- Find the policy `Enable insecure guest logons` and set it to `Enabled`.
- Click `OK` and close the Group Policy Editor.

`````

### Additional Steps and Tips

1. **Verify Network Configuration**:
    
    - Before enabling guest access, ensure that the network configuration allows for guest connections. Go to `Control Panel` > `Network and Sharing Center` > `Advanced sharing settings` and make sure that "Turn on network discovery" and "Turn on file and printer sharing" are enabled.
2. **Restart the Computer**:
    
    - After enabling the policy, it's recommended to restart the computer to ensure that the changes take effect.
3. **Check for Updates**:
    
    - Ensure that your Windows installation is up-to-date by going to `Settings` > `Update & Security` > `Windows Update`. Installing the latest updates may prevent potential issues with policy changes.
4. **Test the Connection**:
    
    - After applying the policy and restarting, test the guest access by connecting from another device. Ensure that you can access shared resources without requiring authentication.
5. **Security Considerations**:
    
    - **Warning**: Enabling unauthenticated guest access can expose your system to security risks. Consider whether this is necessary for your environment and limit the scope of guest access to minimize potential vulnerabilities.
    - Use this setting in trusted environments only, such as internal networks that are isolated from external threats.
6. **Troubleshoot Common Issues**:
    
    - If guest access still does not work, check for the following common issues:
        - **Firewall Settings**: Ensure that the firewall is not blocking guest connections. Adjust the firewall settings to allow file sharing for public and private networks.
        - **Incorrect Policy Settings**: Double-check that the `Enable insecure guest logons` policy is set to `Enabled` and was applied correctly.
        - **Network Issues**: Verify that the network connection is stable and that the guest device is on the same network.
7. **Undoing the Changes**:
    
    - If you decide to disable unauthenticated guest access later, simply set the `Enable insecure guest logons` policy to `Disabled` or `Not Configured` and restart the computer.

