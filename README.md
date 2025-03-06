# ipsec-between-cisco-and-versa

# Cisco CSR to Versa FlexVNF IPsec VPN Configuration

This repository contains configuration examples and implementation details for establishing an IPsec VPN tunnel between a Cisco CSR router and a Versa Networks FlexVNF device.

## Overview

This implementation demonstrates a site-to-site IPsec VPN tunnel setup between:
- **Cisco CSR Router** (10.10.10.2)
- **Versa FlexVNF** (10.10.10.1)

The tunnel creates a secure connection between two network segments, allowing private network communication over the public internet.

## Network Topology

```
                                IPsec Tunnel
+----------------+                                +----------------+
|                |         10.10.10.1             |                |
| Versa FlexVNF  |<------------------------------>| Cisco CSR      |
| (10.10.10.1)   |         10.10.10.2            | (10.10.10.2)   |
+----------------+                                +----------------+
        |                                                  |
        | 10.0.0.1/24                                      | 
        |                                                  |
+----------------+                                +----------------+
|   LAN Segment  |                                |   LAN Segment  |
|                |                                |                |
+----------------+                                +----------------+
```

## Features

- IKEv2 for key exchange
- AES-CBC 256-bit encryption
- SHA256 authentication
- DH Group 14 for key exchange
- Site-to-site VPN configuration
- Tunnel interface assignment (10.0.0.1/24)

## Configuration Details

### Cisco CSR Configuration

The Cisco CSR is configured with:
- Tunnel interface (Tunnel1)
- IPsec profile with AES-CBC and SHA256 authentication
- IKEv2 setup with PSK (Pre-Shared Key) authentication
- External interface IP: 10.10.10.2

### Versa FlexVNF Configuration

The Versa device is set up with:
- IPsec VPN profile named "Cisco-CSR"
- External interface IP: 10.10.10.1
- IKE responder role
- Compatible crypto settings with the Cisco router

## Verification Commands

### Cisco Verification Commands
```
show crypto ipsec sa
show crypto ikev2 sa
show interface tunnel1
```

### Versa Verification Commands
```
show orgs org-services SAFE ipsec vpn-profile Cisco-CSR ike history
```

## Implementation Notes

- The tunnel is using a standard IPsec configuration with strong encryption (AES-256)
- Both devices show successful establishment of the IPsec tunnel
- Traffic statistics show successful bidirectional communication
- Packet encryption and decryption are working properly

## Troubleshooting

Common issues that may arise:
- Phase 1 (IKE) negotiation failures due to mismatched crypto parameters
- Phase 2 (IPsec) negotiation failures due to mismatched policies
- Firewall rules blocking IPsec traffic (UDP 500, UDP 4500, ESP protocol)
- Routing issues preventing traffic from being sent through the tunnel

## Requirements

- Cisco IOS XE version supporting IKEv2
- Versa FlexVNF compatible software version
- Network connectivity between external interfaces
- Correct routing configuration on both ends

## License

[Your license information here]

## Contributing

Contributions, issues, and feature requests are welcome. Feel free to submit pull requests.
