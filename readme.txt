#################################################################################################

																	ASSIGNMENT -3 

#################################################################################################

This system listens for SNMP traps to port UDP:50162. It listens to all the traps and logs them to a file. The message is sent containing the FQDN. Device status could be OK, PROBLEM,DANGER or FAIL. If status is reported as FAIL a trap is sent to the IP,COMMUNITY,PORT specified by the Manager.

****When the first trap is sent the previous status will be shown "MISSING".*****

## Required changes in the configuration files need to be done
   * In /etc/snmp/snmptrapd.conf add the following lines:
        ** disableAuthorization yes
           snmpTrapdAddr UDP:50162
           traphandle 1.3.6.1.4.1.41717.10.* /usr/bin/perl <path to script>/trapdeamon.pl
   *  In /etc/default/snmpd set the following line
        ** TRAPDRUN=yes 
## After making changes in the configuration file restart snmpd from terminal
        ** sudo service snmpd restart  
## To send the trap use the following command:
sudo snmptrap -v 1 -c public 127.0.0.1:50162 .1.3.6.1.4.1.41717.10 10.0.2.2 6 247 ' ' .1.3.6.1.4.1.41717.10.1 s "FQDN" .1.3.6.1.4.1.41717.10.2 i "num"           

Working of the tool:

1) Set all write permissions to the folder which contains assignment3.
2) When a trap is recieved from 1.3.6.1.4.1.41717.10.* to the UDP port 50162 the trapdaemon.pl gets triggered automatically and log file is created in the folder or in to the specified path.
4) Open web browser and type "localhost/path/index.php" to view the home page of the tool.  
5) The main page displays a table showing the status and FQDN.
6) For sending traps on FAIL message IP,COMMUNITY and PORT need to be specified in the front end.
  
