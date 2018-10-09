# Direct device connection overview

Smart devices can establish a safe bi-directional connection with the IoT Hub through the mainstream IoT protocol, MQTT, to allow IoT engineers to start building IoT projects rapidly.

 ![](media/Basic_concepts_mqtt_protocols.png)

## Key concepts

The following concepts are involved in the MQTT connection:

**License**

To connect to the MQTT broker in the EnOS™ cloud, an MQTT client must have a license issued by the EnOS™. The license defines the maximum connections allowed and the expiration date of the authorized connections.

**Connection**

The connection channels that are created under a license. A connection channel can be used by one or multiple devices. For example, you can create a connection `connection_01` to receive data from only the device `inverter_01`. You can also create the connection to receive data from device `inverter_01` and `inverter_02`.

**Policy**

A policy defines transceiving permissions on specific topics. Each permission defines the rights on a single topic. A policy is a collection of permissions.

**Topic**

A topic is the theme of messages. A topic is transmitted through a connection channel, and users can publish or subscribe to the messages of the corresponding topic in the queue. Before you can use the IoT Hub service, you need to create a topic name for our upcoming subscription and publication activities with the MQTT client.

## Data formats

In a direct device connection, the data that the devices send to the IoT Hub must be UTF-8 encoded. Each message is a JSON object or JSON array. The JSON object contains the following nodes:

<table border="1" cellspacing="0" cellpadding="0">
  <tr>
    <th>Node name</td>
    <th>Description</td>
    <th>Required or not</td>
  </tr>
  <tr>
    <td>object</td>
    <td>ID of device instance, string type</td>
    <td>Required</td>
  </tr>
  <tr>
    <td>timestamp</td>
    <td>The time at which data is generated, in milliseconds for UNIX timestamps, long integer.</td>
    <td>Required</td>
  </tr>
  <tr>
    <td>Name of device data point (English string)</td>
    <td>Data point value, follow the definitions in the device model.</td>
    <td>Optional, one message can carry multiple pairs of point values.</td>
  </tr>
  <tr>
    <td>attributes</td>
    <td>Supplemental information about the data points</td>
    <td>Optional</td>
  </tr>
  <tr>
    <td>DEVICE_CONN</td>
    <td>State of device communication. Send string 0 when device is disconnected; send string 1 when device connection resumes.</td>
    <td>Optional</td>
  </tr>
</table>

**Note**: Each message is used to describe the data for a device instance. In each message, the value of device data point and communication state must carry at least one.

Here is an example JSON message

```
{
   “object” : “e61fe67eda1d447a9d11fad686754dd8”,
   “timestamp” : “1505700704000”,
   “INV.GenActivePW” : 16.8256,
   “INV.CurDCIn” : [ 17.3, 17.3 ],
   “INV.PVPowIn” : 17.2601
}
```

In this message，a device instance with ID `e61fe67eda1d447a9d11fad686754dd8` sends two **Floating-point** type of value from data points `INV.GenActivePW` and `INV.PVPowIn` and one **Floating-array** type of value from data point `INV.CurDCIn`。

## Applicable scenarios of MQTT direct connection

The devices to be connected should support MQTT protocol. New intelligent devices of Internet of Things are usually the targets.