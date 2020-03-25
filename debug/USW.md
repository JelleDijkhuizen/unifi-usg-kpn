# Uinify Managed Switch (USW)

## Introduction
This document describes how to validate the switch' IGMP configuration

## Validate Switch Provisioning

1. Login 

    Login into the switch using the debug terminal from the management interface or use `ssh`.

2. Verify provisionming configuration file

    The end of the `/etc/system.cfg` contains the custom provisioned data from the `config.properties` file on the controller. At the end of the file in the `#misc` section you will see the provisioned entries

    ```
    # misc
    switch.igmp.header_checking=false
    switch.vlan.1.igmp_fastleave=true
    ```

# Validate the Switch Configuration

1. Login

    Login into the switch using the debug terminal from the management interface or use `ssh`.

2. Change to switch managment mode

    `telnet localhost`

3. Enable switch management mode

    `enable`

4. Enter VLAN mode

    `vlan database`

5. Show IGMP configuration

    `show igmpsnooping`

    The output of the command shows that IGMP header validation is disabled:
    ```
    Admin Mode..................................... Enable
    Multicast Control Frame Count.................. 584799
    IGMP header validation......................... Disabled
    Interfaces Enabled for IGMP Snooping........... None
    VLANs enabled for IGMP snooping................ 1
    ```
    
    `show igmpsnooping 1`

    The output of the command shows that Fast Leave Mode is enabled for VLAN 1:
    ```
    VLAN ID........................................ 1
    IGMP Snooping Admin Mode....................... Enabled
    Fast Leave Mode................................ Enabled
    Group Membership Interval (secs)............... 260
    Max Response Time (secs)....................... 10
    Multicast Router Expiry Time (secs)............ 0
    Report Suppression Mode........................ Disabled
    ```