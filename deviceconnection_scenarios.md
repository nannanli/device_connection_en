# Use case scenarios

## Scenario 1: Photovoltaic monitoring application

The devices are typically connected to the EnOS™ cloud through local Edge.

### Business background

An application developer plans to build a cloud-based distributed photovoltaic
monitoring application to achieve centralized real-time monitoring of the operational
state of photovoltaic devices across different sites from the cloud. The application also provides event alarming and data analysis services to achieve effective management and optimization of photovoltaic power generation assets.

The application developer, as a third party operator, cannot change the
inverters to be connected, and therefore needs to adapt to various inverters in the market.

### Business analysis

#### Assumptions

- Two types of devices need to be connected: inverter and smart meter. But
the brand and model of inverters and meters vary in different projects.

- No third-party systems are involved, the device data needs to be collected and sent directly to the EnOS™ cloud.

- The total number of devices to be connected to a site does not exceed 20, and
each device collects data from 20 points on average, with an average sampling
cycle of 1 minute.

- The inverters and smart meters support standard Modbus-RTU protocols.

- Wired network is available in the site for connection to the public network.

#### Analysis

Because of the presence of multiple types of third-party devices, and the fact that the communication system can’t be altered, data acquisition needs to be completed with Edge.

### Business construction

1. Device modeling (in EnOS™ cloud).  
   Device modelling is application-facing, which indicates that all projects will reuse the models. The major procedure is as follows:
   <ol style="list-style-type: lower-alpha;">
    <li>Create the photovoltaic domain</li>
    <li>Create the photovoltaic site model</li>
    <li>Create the inverter model and electric meter model</li>
   </ol>

2. Select an appropriate local Edge and install the software.  

   The configuration varies baesd on project conditions. In this case, take the following facts into consideration for determining the edge product to choose:
   - Because each site has limited number of sampling points and limited sampling frequency, Edge hardware with a low configuration is sufficient.
   - As the inverters and smart meters are connected via RS485 bus, a serial port server is required to achieve conversion from serial port to Ethernet port.  

   Purchase an Edge based on the recommended list and install the Edge software.

3. Create device templates (in EnOS™ cloud):

   Assume that there are 20 inverters of the same brand and the same model in a site, and there is one smart meter, you'll need to create a device template for the inverter and a device template for the smart meter.

4. Connect devices to the cloud (in EnOS™ cloud)

   The major procedure is as follows:
    <ol style="list-style-type: lower-alpha;">
      <li>Create devices as cloud assets on EnOS™ (model instantiation)</li>
      <li>Create edge</li>
      <li>Configure connection from the edge to the cloud and add devices into the connection</li>
    </ol>

5. On-site wiring
  The major procedure is as follows:
    <ol style="list-style-type: lower-alpha;">
      <li>Use a 485 bus to connect all inverters and smart meters serially in a daisy chain, and then connect the bus to a serial port server.</li>
      <li>Connect the serial port server to the edge device via wired network, and complete relevant configurations.</li>
      <li>Connect the edge device to the wired network in the site, and ensure that the edge device can connect to the public network.</li>
      </ol>


6. Test communication

   Publish the cloud configuration to Edge and check communication, ensure that all device data is correctly collected to the cloud.

By now, the device data has been collected and sent to the cloud. The next steps will be data acquisition, processing, and analysis via EnOS™ APIs with the photovoltaic applications.

## Scenario 2: Household energy storage battery monitoring application

The devices are typically connected directly to the cloud via MQTT protocol

### Business background

A household energy storage battery vendor plans to build a cloud-based
battery monitoring application to achieve centralized real-time monitoring of operational state of different household energy storage batteries from the cloud. The application will also provide alarm and data analysis services.

The vendor has its own energy storage battery products, and is able to develop and reinvent batteries.

### Business analysis

#### Assumptions

- The battery has its own communication system, and the vendor has the R&D
capability to modify the external communication system of the batteries;

- There is no third party system involved, and the battery devices are
connected directly to EnOS™ cloud platform;

- There is a local wired network with access to public network connected to the battery communication system

#### Analysis

As the vendor has the capability and previledge to modify the device, the vendor can develop the self-registration service for the devices, to enable devices to achieve data interchange with the EnOS™ IoT Hub through the MQTT protocol.

As the devices are standard, all devices share the same template. Therefore, the mapping can be defined natively in the device configuration file. There is no need to create a device template in the EnOS™ cloud.

### Business construction

1. Device modeling (in EnOS™ cloud):
   <ol style="list-style-type: lower-alpha;">
      <li>Create a home energy storage domain</li>
      <li>Create a home site model</li>
      <li>Create a battery model</li>
   </ol>

2. Modify the device, develop self-registration services and integrate MQTT
Client:
   <ol style="list-style-type: lower-alpha;">
      <li>Modify the battery device, develop the device self-registration service in PLC (by calling the EnOS™ API via Web Service protocol), and integrate the MQTT Client.</li>
      <li>Determine MQTT parameters and relevant message structure based on platform MQTT
   access standards. </li>
      <li>Download the license, device id, and key that the platform issues to the device as firmware. This will allow automatic connection of the device to EnOS™ cloud platform upon power-on.</li>
   </ol>

3. After the battery is powered on and connected to the grid, it will automatically connect to the EnOS™ cloud for device registration and asset
creation, and transmit the data, which is already mapped to the model points, to the cloud.

By now, you've completed automatic connection and registration of the battery device. The next steps will be data acquisition, processing, and analysis via EnOS™ API through the energy storage application.