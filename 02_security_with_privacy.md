# Security With Privacy - Solving the Encrypted Traffic Problem

**BRKSEC-2726**

Presenter: Jatin Sachdeva

# Summary and Key Takeaways

* TLS 1.3 will make it very difficult to decrypt TLS traffic in flight.
* Other approaches are needed:
    * Using metadata about the connection, including information in the initial packet, and sequence information (packet lengths versus time).
    * Using DNS requests / responses as a control point (Cisco pitch OpenDNS for this).
    * Continuing to use endpoint protection to control the point before data is encrypted.

# Presentation Notes

## Encrypted Threats

Around 85% of the internet traffic is encrypted.

The challenges:
* Application may break (cert pinning, HKPK)
* New protocols (TLS 1.3, SPDY, HTTP3, QUIC)
* Vendors pushing TLS
* Privacy and compliance
* Decryption computationally intensive

## TLS 1.3

* The certificate is now encrypted between the server and client. This means that the outgoing [SNI](https://en.wikipedia.org/wiki/Server_Name_Indication) is now the main indicator of the destination as the returned certificate can't be seen.
* As the SNI is under control of the client, it can be spoofed. This can lead to incorrect app detection in TLS 1.3.
* SNI encryption is now in draft as well now. See [this CloudFlare blog post](https://blog.cloudflare.com/encrypted-sni/) for more information.


## HTTP/2 Challenges

* Encrypted by default with TLS
* Binary format and header compressions.
* Sinlge TCP reuse.

## QUIC Challenges

* Always encrypted and authenticated - more information [here](https://blog.cloudflare.com/the-road-to-quic/).

## Approaches

### Encrypted Traffic Analytics

Looking for heuristics and patterns in the encrypted data - 'network as a sensor'.

The initial data packet tells us a lot. The ciphersuites of a browser are generally heavy, mobile applications prefer ciphersuites that computationally easier to save battery.

Sequence of packet lenths and times tells us information on the type of application.

### DNS Protection

* OpenDNS/Umbrella pitch - the [intelligent proxy redirection](https://umbrella.cisco.com/products/features/intelligent-proxy) looks interesting.

## CASB

Pitch for CloudLock

## Endpoint

Pitch for Anyconnect

## References

* [TLS 1.3 Impact on Network-Based Security](https://tools.ietf.org/html/draft-camwinget-tls-use-cases-00)



