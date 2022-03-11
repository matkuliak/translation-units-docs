# Show router ospf type, ID, interfaces

## URL

```
frinx-openconfig-network-instance:network-instances/network-instance/<ni-name>/protocols/protocol/frinx-openconfig-policy-types:OSPF/<process-name>
```

## OPENCONFIG YANG

[YANG models](https://github.com/FRINXio/openconfig/tree/master/ospf/src/main/yang)

```javascript
{
    "protocol": [
        {
            "name": <process-name>,
            "identifier": "frinx-openconfig-policy-types:OSPF",
            "config": {
                "name": <process-name>,
                "identifier": "frinx-openconfig-policy-types:OSPF"
            },
            "state": {
                "name": <process-name>,
                "identifier": "frinx-openconfig-policy-types:OSPF"
            },
            "ospfv2": {
                "global": {
                    "config": {
                        "router-id": <router-id>
                    },
                    "state": {
                        "router-id": <router-id>
                    }
                },
                "areas": {
                    "area": [
                        {
                            "identifier": <area-id>,
                            "config": {
                                "identifier": <area-id>
                            },
                            "interfaces": {
                                "interface": [
                                    {
                                        "id": <intf-id>
                                        "config": {
                                            "id": <intf-id>
                                        },
                                        "state": {
                                            "id": <intf-id>
                                        }
                                    }
                                ]
                            },
                            "state": {
                                "identifier": <area-id>
                            }
                        }
                    ]
                }
            }
        }
    ]
}
```


## OS Commands

### Cisco IOS Classic (15.2(4)S5) / XE (15.3(3)S2)

#### CLI

---
<pre>
R121#sh ip ospf
 Routing Process "ospf &lt;process-name&gt;" with ID &lt;router-id&gt;
 Start time: 01:59:55.128, Time elapsed: 00:01:26.652
 Supports only single TOS(TOS0) routes
 Supports opaque LSA
 Supports Link-local Signaling (LLS)
 Supports area transit capability
 Supports NSSA (compatible with RFC 3101)
 Event-log enabled, Maximum number of events: 1000, Mode: cyclic
 Router is not originating router-LSAs with maximum metric
 Initial SPF schedule delay 5000 msecs
 Minimum hold time between two consecutive SPFs 10000 msecs
 Maximum wait time between two consecutive SPFs 10000 msecs
 Incremental-SPF disabled
 Minimum LSA interval 5 secs
 Minimum LSA arrival 1000 msecs
 LSA group pacing timer 240 secs
 Interface flood pacing timer 33 msecs
 Retransmission pacing timer 66 msecs
 Number of external LSA 0. Checksum Sum 0x000000
 Number of opaque AS LSA 0. Checksum Sum 0x000000
 Number of DCbitless external and opaque AS LSA 0
 Number of DoNotAge external and opaque AS LSA 0
 Number of areas in this router is 1. 1 normal 0 stub 0 nssa
 Number of areas transit capable is 0
 External flood list length 0
 IETF NSF helper support enabled
 Cisco NSF helper support enabled
 Reference bandwidth unit is 100 mbps
    Area &lt;area-id&gt;
        Number of interfaces in this area is 1 (1 loopback)
	Area has no authentication
	SPF algorithm last executed 00:00:50.840 ago
	SPF algorithm executed 1 times
	Area ranges are
	Number of LSA 1. Checksum Sum 0x007F46
	Number of opaque link LSA 0. Checksum Sum 0x000000
	Number of DCbitless LSA 0
	Number of indication LSA 0
	Number of DoNotAge LSA 0
	Flood list length 0
</pre>

Supporting command to determine OPSF - VRF relationships:
<pre>
XE2#sh run | include ospf
router ospf &lt;process-name&gt; vrf &lt;ni-name&gt;
router ospf &lt;process-name&gt;
</pre>

Supporting command to show interfaces
<pre>
R121#sh ip ospf interface brief
Interface     PID              Area            IP Address/Mask    Cost  State Nbrs F/C
&lt;intf-id&gt;     &lt;process-name&gt;   &lt;area-id&gt;       7.7.7.7/32         1     LOOP  0/0
R121#
</pre>
---

##### Unit

Unit version range: 3.1.1.rc1-frinx

Link to github : [ios-unit](https://github.com/FRINXio/cli-units/tree/master/ios/ospf)

### Cisco XR 6.1.2

#### Netconf

---
<pre>
RP/0/0/CPU0:XR1#show run router ospf
Thu Jun  4 17:40:46.790 UTC
router ospf &lt;process-name&gt;
 router-id &lt;router-id&gt;
 address-family ipv4 unicast
 area &lt;area-id&gt;
  interface &lt;intf-id&gt;
  !
 !
!
</pre>
---

#### Device YANG
Link to github : [xml-sample]()

##### Unit

Unit version range: 3.1.1.rc1-frinx

Link to github : [xr-unit](https://github.com/FRINXio/unitopo-units/tree/master/xr-6-ospf-unit)
