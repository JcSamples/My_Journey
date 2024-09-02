### Installing ZAP (OWASP ZAP)

1. **Download the ZAP installer**:
    
    - Visit the official ZAP download page: ZAP Downloads
    - Download the appropriate installer for your operating system (Windows, macOS, or Linux).
2. **Make the Script Executable (Linux/MacOS)**:
    
    - If you downloaded the `.sh` installer for Linux or macOS, make sure the script is executable by running:
- 

````shell
chmod +x zap.sh
`````

**Run the Installer**:

- After making the script executable, run the installer:

````shell
./zap.sh
`````

**Dependencies (Linux)**:

- Ensure you have Java installed, as ZAP requires it to run. You can install OpenJDK with the following command:

````shell
sudo apt-get install openjdk-11-jdk
`````

##### You can verify the installation by checking the Java version

````
java -version
`````

**Start ZAP**:

- Once installed, you can start ZAP by navigating to the installation directory and running

````
zap.sh
`````