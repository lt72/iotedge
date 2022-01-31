
# Azure IoT Edge Design and Architecture


These documentation pages describe the design principles, architecture and most important implementation details for [Azure IoT Edge](https://azure.microsoft.com/en-us/services/iot-edge/).

## What is Azure IoT Edge
Azure IoT Edge is an application runtime for Edge devices that are directly or indirectly connected to [Azure IoT Hub](https://azure.microsoft.com/en-us/services/iot-hub/#overview). Azure IoT Edge can operate as an application host and a gateway. Azure IoT Edge can host and manage containerized workloads via any [OCI](https://opencontainers.org/)-compatible container runtime and it is developed and tested using [Moby](https://mobyproject.org/). Azure IoT Edge can behave as a gateway to allow devices to indirectly connect to Azure IoT Hub. 

## When to use Azure IoT Edge
One should use Azure IoT Edge to improve responsiveness and reliability of Edge operations. This need is typically driven by two scenarios: 
  1. Operator wants to limit response latency, by avoiding device-to-cloud rountrips, which may be expensive both in terms of bandwidth and time
  2. Operator wants to achieve continuous operations also in the presence of network instability, e.g., when the device is offline and cannot communicate with any Cloud service, such as Azure IoT Hub. 

### Edge runtime in a nutshell
Edge runtime is build to enable deploying Cloud workloads at the Edge and deal with network instability and low latency requirements. Edge runtime supports deployement of containerized workloads using the Moby OCI-compatible engine. The orchestration of the deployment happens through Azure IoT Edge portal in Azure. Edge runtime manges the wokloads lifetime following the established deployment plan, and monitors and reports status about each workload selected by the operator. Edge runtime allows workloads to communicate with Azure IoT Hub as if all workloads were directly connected to Azure IoT Hub by replicating the functionality of [Azure IoT Hub Device API](https://docs.microsoft.com/en-us/rest/api/iothub/device). Customers can code workloads as containerized apps (a.k.a. _modules_) and can use the [Azure IoT SDKs](https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-devguide-sdks) to connect to Azure IoT Hub indirectly, through Edge runtime, as if there were connecting directly to Azure IoT Hub. Edge runtime will take charge of all telemetry and operations workloads perform with Azure IoT Hub, and will handle lack of connectivity by storing all messages until connectivity is restored. Azure IoT Edge can also behave as a _gateway_ to allow other devices to connect to Azure IoT Hub through Edge.

## How is this documentation organized
This documentation will describe all Azure IoT Edge components (a.k.a. Edge runtime), their interacion with host operating system, the major interaction between components,  the interaction of customer workloads with Edge runtime and Azure IoT Hub, and the role of edge as a gateway. This documentation also describes how to operate Azure IoT Edge and how to develop, deploy and debug a workload and the Edge runtime.

### Conventions
Every Edge runtime component is represented in red. Every optional runtime component is represented in lighter or shaded red. All customer workloads are represented in green. Azure Cloud and its services are represnted in blue. We will use a few UML diagrams to describe components and their interaction:
	
* For all major components, we will provide at least one [deployment diagram](https://en.wikipedia.org/wiki/Deployment_diagram) to describe the physical deployment of that component and at least one [component diagram](https://en.wikipedia.org/wiki/Component_diagram) to describe the interaction of that component with other parts of the deployment, e.g., by documenting which interfaces are exposed and/or consumed. 
* For all major state transitions of runtime components and customer workloads, we will provide [state diagrams](https://en.wikipedia.org/wiki/State_diagram) to document those trnsitions.
* For all interactions between Edge runtime components and other edge runtime components or customer workloads, we will provide at least one [sequence diagram](https://en.wikipedia.org/wiki/Sequence_diagram) to document those interactions, e.g., to illustrate which interfaces are involved in the interaction.

## Index 

1. [Azure IoT Edge Deployment](./md/AzureIoTEdgeRuntime__architecture.md)
   1. Component diagrams for all [Azure IoT Edge runtime components and customer workloads](./md/AzureIoTEdgeRuntime__components_and_workloads.md) 
   2. Runtime [bootstrap sequence](./md/AzureIoTEdgeRuntime__bootstrap.md)
   3. Customer [workloads interaction with Edge runtime](./md/AzureIoTEdgeRuntime__runtime_and_workloads_interactions.md)
   4. Edge as a [gateway](./md/AzureIoTEdgeRuntime__gateway.md)
    
2. Operational Experience
	1. Setup and Configure 
		1. Remote provisioning through [Azure IoT Hub Device Provisioning Service](https://docs.microsoft.com/en-us/azure/iot-dps/) (DPS) 
		2. On-prem provisioning with [EST](https://en.wikipedia.org/wiki/Enrollment_over_Secure_Transport) 
	2. Monitor 
	3. Troubleshoot 

3. Development Experience
	1. Build 
	2. Deploy and Debug 


