# cldemo-netq-l3

This demo repo is to be downloaded onto the oob-mgmt-server of cldemo-vagrant(<https://github.com/CumulusNetworks/cldemo-vagrant>) under 'cumulus' user. It assumes the rest of the network nodes are up and running, but have no configuration on them.

If you had already run a different configuration playbook (for example the vxlan or l2 setup) on this setup, clear out all that using the command:

    ansible-playbook -s reset.yml

To execute the playbook to setup netq, type:

    ansible-playbook -s configure.yml

Once successfully run, you can type 'netq' to see the status of the various nodes. You can also type 'netq' by logging into any of the spine/leaf nodes.
Typing 'netq <TAB>' will show you options to try out. Some useful examples to get you going:

    netq check bgp
    netq check vlan
    netq trace l3 10.1.20.1 from 10.3.20.3
    netq show ip routes 10.1.20.1 origin
    netq show macs leaf01
    netq show changes between 1s and 2m
    ip route | netq resolve | less -R

If you wish to run this with OSPF unnumbered instead of BGP, just edit the properties.yml file and replace 'bgp' with 'ospf' as the value for 'protocol' keyword. Run reset.yml playbook and configure.yml playbook as described above, and you should have a network configured with OSPF. Please note we don't support OSPF analysis yet in netq.
