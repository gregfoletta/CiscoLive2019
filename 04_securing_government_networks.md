# Securing Government Netwokrs

**BRKSEC-2067**

# Summary and Key Takeaways

# Further Reading

* [Suite B](https://en.wikipedia.org/wiki/NSA_Suite_B_Cryptography)
* [CSfC](https://www.nsa.gov/resources/everyone/csfc/)

# Presentation Notes

## Defense in Depth

"Our common enemies are operating within Our certification, accreditation, acquisition and deployment cycles"

## Next Generation Encryption

CNSA aka Suite B - commercial encryption.

**Protocol Suite**:
* Authenticated encryption: AES-128/256-GCM
* Authentication: HMAC-SHA-256
* Key establishment
* Entropy

Define a 'minimum level of security' or 'MLOS'. When combining all of the security parameters.

Size matters: RSA move to 4096 bits

## Layers of Trust

Government enryption devices are replaced with approved high assurance commercial encryption.

**Suite B** has transitioned to **CSfC**. Defines capability packages or architectural patterns for certain use cases. 

## Cryptographic Domain Isolation

Discusses some of the architecures for dealing with differing cryptographic domains (typically [red/black](https://en.wikipedia.org/wiki/Red/black_concept).

CDS or [cross domain solution](https://en.wikipedia.org/wiki/Cross-domain_solution) to cross cryptographic boundaries. Cisco has UDP director which it got when it acquired LANCope.

## Mobile Access

Outer VPN client (through black), inner VPN client (through grey), application encryption (through red).

## Secure Remote Enclave

Inner tunnel and outer tunnel, differing operating systems running on encrypting devices to ensure one vulnerability cannot bring down both tunnels.

## Tagging and Segmentation
