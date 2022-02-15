# abstrac types

~ means optional
1 numbers mean if one is set, others with the same number need to be set as well.
1? means at least one of the numbers has to be fulfilled completely.
1! means either all of 1 or all of 2 have to be set, but never a mix.


## compute
Properties:
- <os>
- <base>

### os
- name
- version
- ~ codename
- ~ filepath (download url, iso?)

### base (mainboard)
- []<cpu>
- []<memory>
- ~ []<storage>
- ~ []<nic>
- ~ <case>
- ~ <psu>
- ~ [] ordered list bootorder
- ~ manufacturer
- ~ model no
- ~ serial no -> random id if unkown -> primary key

### cpu
cores, speed, arch could be retrieved from some only dictionary if manufacturer, model and serial no are known
- cores count
- ~ speed ghz
- ~ arch (x64, arm, ...)
- ~ manufacturer
- ~ model no
- ~ serial no -> random id if unkown -> primary key

### memory
- size gb
- ~ speed mhz
- ~ manufacturer
- ~ model no
- ~ serial no -> random id if unkown -> primary key

### case
- ~ manufacturer
- ~ model no
- ~ serial no -> random id if unkown -> primary key

### PSU
- ~ [] power inlet -> //TODO defined in `## power`, default is 'plugged in correctly'
- ~ manufacturer
- ~ model no
- ~ serial no -> random id if unkown -> primary key


## storage
- size GB
- type (HDD, SSD, Thumbdrive) -> not optional, but needs mapping per provider? or just set optional and have sane default in place? SSD?
- ~ manufacturer
- ~ model no
- ~ serial no -> random id if unkown -> primary key


## network
- <subnet> mask -> only private ones are allowed
- []<ni>: attached network interfaces (one per jack)
- ~ []<dhcp server>: multiple allowed, since they could be responsible for different areas
- ~ []<dns server>: multiple allowed, they could each be referred to by different clients

### nic
- []<ni>
- ~ manufacturer
- ~ model no
- ~ serial no -> random id if unkown -> primary key

### ni
- id (mac) -> random id if unkown -> primary key
- enum: type (rj45, ...)
- []MAC: supported speeds
- ~ MAC: opposite MAC
- ~ []MAC: reachable MACs
- []<ip>: allowed ips
- <ip>: gateway

### cable
- type (rj45, ...)
- []<ni> (#2)

### ip // abstract
#### ipv4
- address
#### ipv6
- address

### dns
#### dns server
- <compute>
- upstreamDNS {primary: <ip>, secondary <ip>}
- []<dns entry>

#### dns entry
- type
- affected (sub)domain / host
- value
- TTL, recommended 300 ?

### dhcp server
- []<subnet>
- ~<ip>: gateway
- ~<ip>: dns-server

##
