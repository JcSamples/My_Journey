Here's an improved guide for installing and running XSS-Proxy:

---

### Installing and Running XSS-Proxy

1. **Download XSS-Proxy**:
    
    - Visit the official XSS-Proxy download page on SourceForge: [XSS-Proxy Downloads](https://sourceforge.net/projects/xss-proxy/).
    - Download the latest version of XSS-Proxy, which typically comes as a `.pl` Perl script.
2. **Install Perl (if not already installed)**:
    
    - XSS-Proxy requires Perl to run. Most Linux and macOS systems come with Perl pre-installed, but if not, you can install it using the following command:

````shell
sudo apt-get install perl  # On Ubuntu/Debian
sudo yum install perl      # On CentOS/RHEL
brew install perl          # On macOS using Homebrew
`````

Verify Perl installation by checking the version

````
perl -v
`````

**Set Up Dependencies**:

- XSS-Proxy may require additional Perl modules. You can install common dependencies using CPAN (Comprehensive Perl Archive Network):

````shell
sudo cpan install LWP::UserAgent HTTP::Request
`````

**Make the Script Executable (Optional)**:

- If you prefer, you can make the script executable

````shell
chmod +x XSS-Proxy_0_0_12-book.pl
`````

**Run the Script**:

- After setting up Perl and any necessary modules, you can run the XSS-Proxy script

````
perl XSS-Proxy_0_0_12-book.pl
`````