# USING RASPBERRY PI as a Print Server
playing around pi


** always update first: sudo apt-get update **

1. cheezychinito@cheezychinitopi:~ $ sudo apt-get install hplip
2. cheezychinito@cheezychinitopi:~ $ sudo apt-get install cups

** as a best practice add your user to the linux admin group "lpadmin". You can verify if lpadmin is added by typing
"groups": cheezychinito@cheezychinitopi:~ $ groups. This requires a reboot **

3. cheezychinito@cheezychinitopi:~ $ sudo usermod -a -G lpadmin cheezychinito

** CUPS can be accessed through web, but we need to edit some settings to cups config file first **

4. cheezychinito@cheezychinitopi:~ $ nano /etc/cups/cupsd.conf

#Only listen for connections from the local machine.

Port 631
Listen /var/run/cups/cups.sock

#Show shared printers on the local network.

Browsing On

BrowseLocalProtocols dnssd

BrowseRemoteProtocols CUPS dnssd

BrowseAddress @LOCAL

#Restrict access to the server...

<Location />
  Order allow,deny
  Allow all
</Location>

#Restrict access to the admin pages...

<Location /admin>
#Order allow,deny
</Location>

5. Exit and restart service
cheezychinito@cheezychinitopi:~ $ sudo service cups reload

6. Go the web browser and type the IP address or hostname of your PI print server using port 631
https://cheezychinitopi:631

7. From the admin page, select "add printer".
8. Authenticate using your username and password
9. Follow the procedures and use your Printer device and model

