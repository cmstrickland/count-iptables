A simple example of using iptables with an empty chain to count traffic passing through a virtual network interface on linux.

You will need to edit the vagrantfile so that it points at a box you have access to. Anything debian flavoured will do.

The provision script adds an virtual ip on eth0:0 bound to 192.168.1.6, and sets up a user iptables chain that accepts all traffic, and jump rules for source and destination packets to this interface to pass through it.

`vagrant up && vagrant ssh` to shell in

You can throw some traffic at the interface by telnetting to it. Something like this will do it.

Open a new shell and run `nc -l 192.168.1.6 -p 12345` to listen on that interface

From another shell `telnet 192.168.1.6 12345`

Type some jank into the second shell, you should see it coming in on the first one 

From a third shell `iptables -L -v` should show a packet count on the user chain
