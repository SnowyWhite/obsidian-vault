# Installing Metasploit on Linux / macOS

The following script invocation will import the Rapid7 signing key and setup the package for supported Linux and macOS systems:

```bash
curl https://raw.githubusercontent.com/rapid7/metasploit-omnibus/master/config/templates/metasploit-framework-wrappers/msfupdate.erb > msfinstall && \
 chmod 755 msfinstall && \
 ./msfinstall
```

Once installed, you can launch msfconsole as /opt/metasploit-framework/bin/msfconsole from a terminal window, or depending on your environment, it may already be in your path and you can just run it directly. On first run, a series of prompts will help you setup a database and add Metasploit to your local PATH if it is not already.

These packages integrate into your package manager and can be updated with the msfupdate command, or with your package manager. On first start, these packages will automatically setup the database or use your existing database.

```bash
Creating MSF web service user user

    ############################################################
    ##              MSF Web Service Credentials               ##
    ##                                                        ##
    ##        Please store these credentials securely.        ##
    ##    You will need them to connect to the webservice.    ##
    ############################################################

MSF web service username: admin
MSF web service password: admin123
MSF web service user API token: <3


MSF web service configuration complete
The web service has been configured as your default data service in msfconsole with the name "local-https-data-service"

If needed, manually reconnect to the data service in msfconsole using the command:
db_connect --name local-https-data-service --token <3 --cert /home/user/.msf4/msf-ws-cert.pem --skip-verify https://localhost:5443

The username and password are credentials for the API account:
https://localhost:5443/api/v1/auth/account

Persisting http web data service credentials in msfconsole
====================================================================

```