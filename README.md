# Sample NSO package

## NSO config

```
admin@ncs(config)# show config
bgpmgr test
 dev1    xr-1
 dev2    xr-2
 dev1-as 100
 dev2-as 100
```


## IOS-XR configuration to be applied

```
admin@ncs(config)# commit dry-run outformat native
native {
    device {
        name xr-1
        data route-policy PASS
               pass
              end-policy
             !
             router bgp 100
              bgp router-id 10.2.1.2
              bgp update-delay 0
              address-family ipv4 unicast
               redistribute connected
              exit
              neighbor 10.2.1.3
               remote-as 100
               address-family ipv4 unicast
                route-policy PASS in
                route-policy PASS out
               exit
              exit
             exit
    }
    device {
        name xr-2
        data route-policy PASS
               pass
              end-policy
             !
             router bgp 100
              bgp router-id 10.2.1.3
              bgp update-delay 0
              address-family ipv4 unicast
               redistribute connected
              exit
              neighbor 10.2.1.2
               remote-as 100
               address-family ipv4 unicast
                route-policy PASS in
                route-policy PASS out
               exit
              exit
             exit
    }
}
admin@ncs(config)#
```
