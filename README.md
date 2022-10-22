### hq.akdev.xyz internal network configuration

1. Bootstrapping a host
2. Router configuration

#### Bootstraping

1. Add inventory to ansible inventory - `inventory.yml`
2. Execute `bootstrap-host.yml` with an available USB drive for flashing
3. Run `virtualization-platform.yml` to set up the new host as a hypervisor

##### Router configuration

We are running on a virtualized pfSense instance using Linux bridge networking for
connectivity.

1. enp1s0 - corresponds to the uplink from the ISP
2. enp2s0 - corresponds to the trunk port for the local network
3. enp4s0 - corresponds to the PI network [wip]

The pfSense guest claims exclusive ownership of `enp1s0` and nothing else should be bound to that network.
The local traffic goes in through `enp2s0` with the proper VLAN tags. `enp4s0` has a PVID=11 which isolates
the PI network from any other traffic.
