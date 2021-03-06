# CoAP-Based Connection

Developers can report the real-time data collected from a device to EnOS by using the CoAP/UDP protocol. This feature provides secure connection and data management for massive devices. The process for connecting NB-IoT devices to EnOS is as follows:

 .. image:: ../media/coap_messageflow.png

1. Cofigure authentication keyes on a device, including `ProductKey`, `DeviceKey` and `DeviceSecret`;
2. The device connects to EnOS via the NB-IoT network provided by a carrier. The carrier is responsible for billing and the traffic data generated by devices and does not store any service data.
3. Developers can use the EnOS open APIs to obtain data, modify measure points, call device services and export data into applications.

## CoAP Protocol Specifications

The protocol supported by EnOS is RFC 7252 Constrained Application Protocol. For details, see [RFC 7252](https://tools.ietf.org/html/rfc7252?spm=a2c4g.11186623.2.12.2e2e3cb88Cjj8L).

## EnOS-specific Definitions

EnOS supports confirmable (CON) messages. The response to a request carried in a confirmable message is carried, or piggybacked, in the resulting acknowledgement (ACK) message.

EnOS supports cacheability of CoAP prescribed in RFC7252. Therefore, every new request uses a unique CoAP message ID and token.

EnOS supports the block-wise transfers in CoAP protocol. For more information, see [RFC 7959](https://tools.ietf.org/html/rfc7959).

## DTLS Secure Channel

The device requests to connect to the specified CoAP server and then builds a secure channel. The procedure is as follows:

1. The device sends the DTLS handshake request to EnOS.

2. The device and EnOS negotiate PSK parameters as per the pre-defined algorithm.

3. The device sends the `pskid` and `len` parameters to EnOS for verification, and then builds a secure channel after a successful verification.

After a secure channel is established, the device initiates an authentication request. If encryption is adopted, this step can be combined with the DTLS handshake; otherwise, keys are required for authentication. Encrypted authentication methods include unique-certificate-per-device and unique-certificate-per-product authentication. Unique-certificate-per-product authentication requires that the device queries the device secret from EnOS before authentication.

EnoS uses DTLS v1.2 to ensure the channel security. For more information, see [RFC 6347](https://tools.ietf.org/html/rfc6347?spm=a2c4g.11186623.2.13.2e2e3cb88Cjj8L).


## Notes

Device connection based on CoAP reuses the topic specifications of MQTT.

EnOS doesn't support resource discovery or the Observe option [OBSERVE].

The size of a data packet that can be transmitted via CoAP depends on the size of MTU, which should be limited within 1KB.

## Next step

Refer to [CoAP-based Connection and Communication](../reference/coap/index) to connect the device to EnOS and reuse the MQTT topic for data transmission with EnOS Cloud.
