A simple example of using iptables with an empty chain to count traffic passing through a virtual network interface on linux.

You will need to edit the vagrantfile so that it points at a box you have access to. Anything debian flavoured will do.

The provision script adds an virtual ip on eth0:0 bound to 192.168.1.6, and sets up a user iptables chain that accepts all traffic, and jump rules for source and destination packets to this interface to pass through it.

`vagrant up && vagrant ssh` to shell in

you can throw some traffic at the interface by telnetting to it. Something like this will do it.

open a new shell and run `nc -l 192.168.1.6 -p 12345`

from another shell `telnet 192.168.1.6 12345`

type some jank into the first shell

from a third shell `iptables -L -v` should show a packet count on the user chaing
