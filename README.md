# check_ibm_pdu
nagios check for IBM / Lenovo intelligent Power Distribution Unit

This check is for IBM / Lenovo Intelligent Power Distribution Units.  
Originally designed and manufactured by IBM, these PDU devices are also re-branded by Lenovo.
If you are not sure if you have the appropriate PDU, the login screen looks similar to:

<img src=images/login.png>

The web-based user interface to this PDU will look similar to:

<img src=images/webgui.png>

# Requirements
perl, enable SNMP on PDU


# Configuration
Enable SNMP on the PDU

<img src=images/snmp.png>

Add a section similar to the following to services.cfg on the nagios server
```
# Define a service to check the IBM/Lenovo PDU
# Parameters are SNMP community name
define service {
        use                             generic-service
        hostgroup_name                  all_ibm_pdu
        service_description             PDU health
        check_command                   check_ibmpdu!public
        }
```


Add a section similar to the following to commands.cfg on the nagios server
```
# 'check_ibm_pdu' command definition
# parameters are -H hostname -C snmp_community
define command{
        command_name    check_ibmpdu
        command_line    $USER1$/check_ibm_pdu -H $HOSTADDRESS$ -C $ARG1$
        }
```



# Output
<img src=images/output.png>

# Optional Graphs

This check provides performance data that can be optionally graphed via NagiosGraph, PNP4Nagios, Prometheus, etc to provide historical utilization details.
<img src=images/temperature.png>
<img src=images/watts.png>
<img src=images/amps.png>
