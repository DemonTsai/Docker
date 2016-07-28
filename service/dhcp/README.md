# ISC-DHCP-SERVER

## Run:
* Command

    ```
    docker run -d --name=dhcp --privileged --net=host dhcp-server
    ```

## Help:
* dhcp_cfg -h

    ```
    Usage: dhcp_cfg [Option] [Value]
    [Options]:
            -D                      :Dump debug message.
            -U                      :Update host|subnet config
            -R                      :Remove host|subnet config
            -T host|subnet|global   :Type (mandatory)
        
            In host type:
            -u name                 :Host name (mandatory)
            -m macaddress           :MAC address (mandatory)
            -f ip                   :Host IP address (mandatory)
        
            In subnet type:
            -s subnet               :Subnet network (mandatory)
            -n netmask              :Subnet netmask (mandatory)
            -r start_ip/end_ip      :Dynamic IP range (mandtory)
            -i interface            :Specify interface.
            -g ip                   :Router IP address
            -b broadcast            :Broadcast address
            -d ip                   :DNS IP address for specific subnet
            -o name                 :Domain name for specific subnet
            -e time                 :Default lease time for specific subnet
            -x time                 :Max lease time for specific subnet
        
            In global type:
            -d ip                   :DNS IP address for global
            -o name                 :Domain name for global
            -e time                 :Default lease time for global
            -x time                 :Max lease time for global
        
            -p                      :Dump DHCP config
            -h                      :Help
    ```

## Sample:
### Host Type:
* Add a fixed host ip
    * -T, -u, -m, -f is necessary, -g, -d, -o, -e, -x is optional.

        ```
        dhcp_cfg -T host -u host_name -m aa:bb:cc:dd -f 192.168.10.1
        ```
    * Result

        ```
        host host_name {
            hardware ethernet aa:bb:cc:dd;
            fixed-address 192.168.10.1;
        }
        ```
* Update host data
    * -U, -T, -u is necessary, -m, -f, -g, -d, -o, -e, -x is optional.

        ```
        dhcp_cfg -U -T host -u host_name -m 11:22:33:44:55:66
        ```
        ```
        dhcp_cfg -U -T host -u host_name -m ww:xx:yy:zz -f 192.168.111.1
        ```
    * Result

        ```
        host host_name {
            hardware ethernet 11:22:33:44:55:66;
            fixed-address 192.168.10.1;
        }
        ```
        ```
        host host_name {
            hardware ethernet ww:xx:yy:zz;
            fixed-address 192.168.111.1;
        }
        ```
* Remove a fixed ip host
    * -R, -T, -u is necessary

        ```
        dhcp_cfg -R -T host -u host_name
        ```

### Subnet Type:
* Add a subnet
    * -T, -s, -n, -r is necessary, -b, -i, -g, -d, -o, -e, -x is optional

        ```
        dhcp_cfg -T subnet -s 192.168.10.0 -n 255.255.255.0 -r 192.168.10.1/192.168.10.254
        ```
    * Result

        ```
        subnet 192.168.10.0 netmask 255.255.255.0 {
            range 192.168.10.1 192.168.10.254;
        }
        ```
* Update a subnet
    * -U, -T, -s, -n is necessary, -r, -b, -i, -g, -d, -o, -e, -x is optional

        ```
        dhcp_cfg -U -T subnet -s 192.168.10.0 -n 255.255.255.0 -r 192.168.10.100/192.168.10.200 -i eth1.100
        ```
        ```
        dhcp_cfg -U -T subnet -s 192.168.10.0 -n 255.255.255.0 -g 192.168.10.254
        ```
    * Result

        ```
        subnet 192.168.10.0 netmask 255.255.255.0 {
            range 192.168.10.100 192.168.10.200;
            interface eth1.100;
        }
        ```
        ```
        subnet 192.168.10.0 netmask 255.255.255.0 {
            range 192.168.10.100 192.168.10.200;
            interface eth1.100;
            option routers 192.168.10.254;
        }
        ```
* Remove a subnet
    * -R, -T, -s, -n is necessary

        ```
        dhcp_cfg -R -T subnet -s 192.168.10.0 -n 255.255.255.0
        ```

### Global Type:
* Update global config
    * -T is necessary, -d, -o, -e, -x only.

        ```
        dhcp_cfg -T global -o my_domain_name
        ```
    * Result

        ```
        option domain-name "my_domain_name";
        option domain-name-servers ns1.example.org, ns2.example.org;
        default-lease-time 600;
        max-lease-time 7200;
        ```

### NOTE:
* Router and DNS is multiple
    * Example:

        ```
        dhcp_cfg -T subnet -s 192.168.10.0 -n 255.255.255.0 -r 192.168.10.1/192.168.10.200 -d 168.95.1.1 -d 8.8.8.8 -g 192.168.10.254 -g 192.168.10.253
        ```
