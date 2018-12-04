# Disable Sub-devices

This topic notifies the edge that the specific sub-devices belong to
this edge have been disabled from the EnOS Cloud. EnOS Cloud publishes
the disable devices message to the edge topic asynchronously.

Downstream
- Request Topic: /ext/session/{productKey}/{deviceKey}/combine/disable

- Reply topic: /ext/session/{productKey}/{deviceKey}/combine/disable_reply

**Note:** The *productKey* and *deviceKey* in the TOPIC are the parameters of the edge.

## Example Request Message

```
{
	"id": "123",
	"version": "1.0",
	"params": [
            {
		"productKey": "xxx",
		"deviceKey": "xxx"
	}
	],
	"method": "combine.disable"
}

```

## Example Response Message

```
{
	"id": "123",
	"code": 200,
	"data": {}
}
```

## Parameter Description​

<table>
  <tr>
    <td>Parameters</td>
    <td>Type​</td>
    <td>Occurrence </td>
    <td>Description</td>
  </tr>
  <tr>
    <td>id</td>
    <td>Long</td>
    <td>Optional</td>
    <td>Message ID. Reserved parameter for future use.</td>
  </tr>
  <tr>
    <td>version</td>
    <td>String</td>
    <td>Mandatory</td>
    <td>Version of the protocol. Current version is 1.0.</td>
  </tr>
  <tr>
    <td>params</td>
    <td>Object</td>
    <td>Mandatory</td>
    <td>Request parameters. </td>
  </tr>
  <tr>
    <td>productKey</td>
    <td>String</td>
    <td>Mandatory</td>
    <td>Product key of the sub-device.</td>
  </tr>
  <tr>
    <td>deviceKey</td>
    <td>String</td>
    <td>Mandatory</td>
    <td>Device key of the sub-device.</td>
  </tr>
  <tr>
    <td>method</td>
    <td>String</td>
    <td>Mandatory</td>
    <td>The method of the request.</td>
  </tr>
  <tr>
    <td>code</td>
    <td>Integer</td>
    <td>Mandatory</td>
    <td>Response code &ldquo;200&rdquo; or the error code defined on device end. &ldquo;200&rdquo; indicates the request is executed successfully. </td>
  </tr>
  <tr>
    <td>data</td>
    <td>String</td>
    <td>Optional </td>
    <td>Detailed information, in JSON format. </td>
  </tr>
</table>