Base Environment: CentOS 7

The guide assumes that you're running oVirt Engine with PostgreSQL as per the oVirt Engine with PostgreSQL in 
a container guide or the standard oVirt Engine installation that requires you to have PostgreSQL installed and
appropriately configured. 

### Steps
1. Make sure that the Docker service is running:

   `$ sudo service docker start`

or

   `$ sudo systemctl start docker.service`

2. Clone the repo to build the image. 
   
   `$ git clone https://github.com/freeipa/freeipa-container.git`
   
3. Build the Docker image.
   
   i. Change directory into where you've cloned the above repo:
      
      `$ cd freeipa-container/`
   
   FreeIPA provides the option of building images based on the following distributions:
   - CentOS
   - Fedora 
   - Red Hat Enterprise Linux
   
   By default, it will build for Fedora. To avoid this, copy the Dockerfile named `Dockerfile.centos-7` to `Dockerfile`
   as follows:
   
      `$ cp Dockerfile.centos-7 Dockerfile`
   
   This should make the build use CentOS 7. Do the same for RHEL if that's what you'd like. [1]
   
   ii. Build the image as follows:
   
      `docker build -t freeipa-server`.

4. Run the container image [2]

   `docker run --privileged --name ovirt-freeipa-server-container -p 180:80 -p 1443:443 -ti -h ipa.ovirt.test -e PASSWORD=password freeipa/freeipa-server`

```
systemd 231 running in system mode. (+PAM +AUDIT +SELINUX +IMA -APPARMOR +SMACK +SYSVINIT +UTMP +LIBCRYPTSETUP +GCRYPT +GNUTLS +ACL +XZ +LZ4 +SECCOMP +BLKID +ELFUTILS +KMOD +IDN)
Detected virtualization docker.
Detected architecture x86-64.
Set hostname to <ipa.ovirt.test>.
Failed to install release agent, ignoring: No such file or directory
Thu Aug 31 10:04:31 UTC 2017 /usr/sbin/ipa-server-configure-first 

The log file for this installation can be found in /var/log/ipaserver-install.log
==============================================================================
This program will set up the FreeIPA Server.

This includes:
  * Configure a stand-alone CA (dogtag) for certificate management
  * Configure the Network Time Daemon (ntpd)
  * Create and configure an instance of Directory Server
  * Create and configure a Kerberos Key Distribution Center (KDC)
  * Configure Apache (httpd)

To accept the default shown in brackets, press the Enter key.

Do you want to configure integrated DNS (BIND)? [no]: 

Enter the fully qualified domain name of the computer
on which you're setting up server software. Using the form
<hostname>.<domainname>
Example: master.example.com.


Server host name [ipa.ovirt.test]: 

The domain name has been determined based on the host name.

Please confirm the domain name [ovirt.test]: 

The kerberos protocol requires a Realm name to be defined.
This is typically the domain name converted to uppercase.

Please provide a realm name [OVIRT.TEST]: 

The IPA Master Server will be configured with:
Hostname:       ipa.ovirt.test
IP address(es): 172.17.0.4
Domain name:    ovirt.test
Realm name:     OVIRT.TEST

Continue to configure the system with these values? [no]: 

The following operations may take some minutes to complete.
Please wait until the prompt is returned.

Configuring NTP daemon (ntpd)
  [1/4]: stopping ntpd
  [2/4]: writing configuration
  [3/4]: configuring ntpd to start on boot
  [4/4]: starting ntpd
Done configuring NTP daemon (ntpd).
Configuring directory server (dirsrv). Estimated time: 1 minute
  [1/47]: creating directory server user
  [2/47]: creating directory server instance
  [3/47]: updating configuration in dse.ldif
  [4/47]: restarting directory server
  [5/47]: adding default schema
  [6/47]: enabling memberof plugin
  [7/47]: enabling winsync plugin
  [8/47]: configuring replication version plugin
  [9/47]: enabling IPA enrollment plugin
  [10/47]: enabling ldapi
  [11/47]: configuring uniqueness plugin
  [12/47]: configuring uuid plugin
  [13/47]: configuring modrdn plugin
  [14/47]: configuring DNS plugin
  [15/47]: enabling entryUSN plugin
  [16/47]: configuring lockout plugin
  [17/47]: configuring topology plugin
  [18/47]: creating indices
  [19/47]: enabling referential integrity plugin
  [20/47]: configuring certmap.conf
  [21/47]: configure autobind for root
  [22/47]: configure new location for managed entries
  [23/47]: configure dirsrv ccache
  [24/47]: enabling SASL mapping fallback
  [25/47]: restarting directory server
  [26/47]: adding sasl mappings to the directory
  [27/47]: adding default layout
  [28/47]: adding delegation layout
  [29/47]: creating container for managed entries
  [30/47]: configuring user private groups
  [31/47]: configuring netgroups from hostgroups
  [32/47]: creating default Sudo bind user
  [33/47]: creating default Auto Member layout
  [34/47]: adding range check plugin
  [35/47]: creating default HBAC rule allow_all
  [36/47]: adding sasl mappings to the directory
  [37/47]: adding entries for topology management
  [38/47]: initializing group membership
  [39/47]: adding master entry
  [40/47]: initializing domain level
  [41/47]: configuring Posix uid/gid generation
  [42/47]: adding replication acis
  [43/47]: enabling compatibility plugin
  [44/47]: activating sidgen plugin
  [45/47]: activating extdom plugin
  [46/47]: tuning directory server
  [47/47]: configuring directory to start on boot
Done configuring directory server (dirsrv).
Configuring certificate server (pki-tomcatd). Estimated time: 3 minutes 30 seconds
  [1/31]: creating certificate server user
  [2/31]: configuring certificate server instance
  [3/31]: stopping certificate server instance to update CS.cfg
  [4/31]: backing up CS.cfg
  [5/31]: disabling nonces
  [6/31]: set up CRL publishing
  [7/31]: enable PKIX certificate path discovery and validation
  [8/31]: starting certificate server instance
  [9/31]: creating RA agent certificate database
  [10/31]: importing CA chain to RA certificate database
  [11/31]: fixing RA database permissions
  [12/31]: setting up signing cert profile
  [13/31]: setting audit signing renewal to 2 years
  [14/31]: restarting certificate server
  [16/31]: issuing RA agent certificate
  [17/31]: adding RA agent as a trusted user
  [18/31]: authorizing RA to modify profiles
  [19/31]: authorizing RA to manage lightweight CAs
  [20/31]: Ensure lightweight CAs container exists
  [21/31]: configure certmonger for renewals
  [22/31]: configure certificate renewals
  [23/31]: configure RA certificate renewal
  [24/31]: configure Server-Cert certificate renewal
  [25/31]: Configure HTTP to proxy connections
  [26/31]: restarting certificate server
  [26/31]: restarting certificate server
  [27/31]: migrating certificate profiles to LDAP
  [28/31]: importing IPA certificate profiles
  [29/31]: adding default CA ACL
  [30/31]: adding 'ipa' CA entry
  [31/31]: updating IPA configuration
Done configuring certificate server (pki-tomcatd).
Configuring directory server (dirsrv). Estimated time: 10 seconds
  [1/3]: configuring ssl for ds instance
  [2/3]: restarting directory server
  [3/3]: adding CA certificate entry
Done configuring directory server (dirsrv).
Configuring Kerberos KDC (krb5kdc). Estimated time: 30 seconds
  [1/9]: adding kerberos container to the directory
  [2/9]: configuring KDC
  [3/9]: initialize kerberos container
WARNING: Your system is running out of entropy, you may experience long delays
  [4/9]: adding default ACIs
  [5/9]: creating a keytab for the directory
  [6/9]: creating a keytab for the machine
  [7/9]: adding the password extension to the directory
  [8/9]: starting the KDC
  [9/9]: configuring KDC to start on boot
Done configuring Kerberos KDC (krb5kdc).
Configuring kadmin
  [1/2]: starting kadmin 
  [2/2]: configuring kadmin to start on boot
Done configuring kadmin.
  [1/2]: starting kadmin 
  [2/2]: configuring kadmin to start on boot
Done configuring kadmin.
Configuring ipa_memcached
  [1/2]: starting ipa_memcached 
  [2/2]: configuring ipa_memcached to start on boot
Done configuring ipa_memcached.
Configuring ipa-otpd
  [1/2]: starting ipa-otpd 
  [2/2]: configuring ipa-otpd to start on boot
Done configuring ipa-otpd.
Configuring ipa-custodia
  [1/5]: Generating ipa-custodia config file
  [2/5]: Making sure custodia container exists
  [3/5]: Generating ipa-custodia keys
  [4/5]: starting ipa-custodia 
  [5/5]: configuring ipa-custodia to start on boot
Done configuring ipa-custodia.
Configuring the web interface (httpd). Estimated time: 1 minute
  [1/21]: setting mod_nss port to 443
  [2/21]: setting mod_nss cipher suite
  [3/21]: setting mod_nss protocol list to TLSv1.0 - TLSv1.2
  [4/21]: setting mod_nss password file
  [5/21]: enabling mod_nss renegotiate
  [6/21]: adding URL rewriting rules
  [7/21]: configuring httpd
  [8/21]: configure certmonger for renewals
  [9/21]: setting up httpd keytab
  [10/21]: setting up ssl
  [11/21]: importing CA certificates from LDAP
  [12/21]: setting up browser autoconfig
  [13/21]: publish CA cert
  [14/21]: clean up any existing httpd ccache
  [15/21]: configuring SELinux for httpd
  [16/21]: create KDC proxy user
  [17/21]: create KDC proxy config
  [18/21]: enable KDC proxy
  [19/21]: restarting httpd
  [20/21]: configuring httpd to start on boot
  [21/21]: enabling oddjobd
Done configuring the web interface (httpd).
Applying LDAP updates
Upgrading IPA:
  [1/9]: stopping directory server
  [2/9]: saving configuration
  [3/9]: disabling listeners
  [4/9]: enabling DS global lock
  [5/9]: starting directory server
  [6/9]: upgrading server
  [7/9]: stopping directory server
  [8/9]: restoring configuration
  [9/9]: starting directory server
Done.
Restarting the directory server
Restarting the KDC
ipa         : ERROR    unable to resolve host name ipa.ovirt.test. to IP address, ipa-ca DNS record will be incomplete
Please add records in this file to your DNS system: /tmp/ipa.system.records.TpnpmT.db
Restarting the web server
Configuring client side components
Using existing certificate '/etc/ipa/ca.crt'.
Client hostname: ipa.ovirt.test
Realm: OVIRT.TEST
DNS Domain: ovirt.test
IPA Server: ipa.ovirt.test
BaseDN: dc=ovirt,dc=test

Skipping synchronizing time with NTP server.
New SSSD config will be created
Configured sudoers in /etc/nsswitch.conf
Configured /etc/sssd/sssd.conf
trying https://ipa.ovirt.test/ipa/json
Forwarding 'schema' to json server 'https://ipa.ovirt.test/ipa/json'
trying https://ipa.ovirt.test/ipa/session/json
Forwarding 'ping' to json server 'https://ipa.ovirt.test/ipa/session/json'
Forwarding 'ca_is_enabled' to json server 'https://ipa.ovirt.test/ipa/session/json'
Systemwide CA database updated.
SSSD enabled
Configured /etc/openldap/ldap.conf
/etc/ssh/ssh_config not found, skipping configuration
/etc/ssh/sshd_config not found, skipping configuration
Configuring ovirt.test as NIS domain.
Client configuration complete.

==============================================================================
Setup complete

Next steps:
	1. You must make sure these network ports are open:
		TCP Ports:
		  * 80, 443: HTTP/HTTPS
		  * 389, 636: LDAP/LDAPS
		  * 88, 464: kerberos
		UDP Ports:
		  * 88, 464: kerberos
		  * 123: ntp

	2. You can now obtain a kerberos ticket using the command: 'kinit admin'
	   This ticket will allow you to use the IPA tools (e.g., ipa user-add)
	   and the web user interface.

Be sure to back up the CA certificates stored in /root/cacert.p12
These files are required to create replicas. The password for these
files is the Directory Manager password
FreeIPA server does not run DNS server, skipping update-self-ip-address.
Created symlink /etc/systemd/system/container-ipa.target.wants/ipa-server-update-self-ip-address.service -> /usr/lib/systemd/system/ipa-server-update-self-ip-address.service.
Created symlink /etc/systemd/system/container-ipa.target.wants/ipa-server-upgrade.service -> /usr/lib/systemd/system/ipa-server-upgrade.service.
Failed to disable unit: Too many levels of symbolic links
FreeIPA server configured.

```

5. Make directory.

`mkdir /var/lib/ipa-data`

6. Enter the container and edit the `/etc/dirsrv/slapd-EXAMPLE-TEST/dse.ldif` or equivalent file based on what you named your FreeIPA server domain. Change the line `nsslapd-minssf: 0` to `nsslapd-minssf: 1` before stopping and restarting the container. [3]
You may use the command below:

`docker exec -ti ovirt-freeipa-server-container bash`

7. Create a new user to use with the oVirt Engine:
- Enter the container:
  `docker exec -ti ovirt-freeipa-server-container bash`
- Run `kinit admin` at the prompt to authenticate as the FreeIPA admin, using the password set when you first ran the container. 
  ```
  [root@ovirt /]# kinit admin`
  Password for admin@OVIRT.TEST:
  
  ```
- Add a user account for oVirt Engine to use with FreeIPA
  ```
  [root@ovirt /]# ipa user-add
  First name: ovirt
  Last name: user
  User login [ouser]: ovirt-user
  -----------------------
  Added user "ovirt-user"
  -----------------------
    User login: ovirt-user
    First name: ovirt
    Last name: user
    Full name: ovirt user
    Display name: ovirt user
    Initials: ou
    Home directory: /home/ovirt-user
    GECOS: ovirt user
    Login shell: /bin/sh
    Principal name: ovirt-user@OVIRT.TEST
    Principal alias: ovirt-user@OVIRT.TEST
    Email address: ovirt-user@ovirt.test
    UID: 142400001
    GID: 142400001
    Password: False
    Member of groups: ipausers
    Kerberos keys available: False

  ```
- Add a password for the new user created:
  ```
  [root@ovirt /]# ipa passwd ovirt-user
  New Password: 
  Enter New Password again to verify: 
  --------------------------------------------
  Changed password for "ovirt-user@OVIRT.TEST"
  --------------------------------------------
  
  ```
- Log in as `ovirt-user` and change the above password as required by FreeIPA
  ```
  [root@ovirt /]# kinit ovirt-user
  Password for ovirt-user@OVIRT.TEST: 
  Password expired.  You must change it now.
  Enter new password: 
  Enter it again: 

  ```
8. Add the container's IP address to the `/etc/resolv.conf` file to use the FreeIPA container for DNS i.e. `nameserver CONTAINER-IP`

[1]: Here the README for FreeIPA containers says that the option to build an image based on something other that what is offered by the default target can be specified using the -f option. Didn't work for me. Reference [here.](https://github.com/freeipa/freeipa-container)
[2]: You may use the default ports for the FreeIPA container for easier debugging. I have done the port mapping to prevent conflicts with other containers on the host. 
[3]: This refers to the issue detailed [here](http://www.ovirt.org/documentation/how-to/troubleshooting/troubleshooting/#adding-an-ipa-domain-to-ovirt-engine).
