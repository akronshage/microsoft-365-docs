---
title: Set up Microsoft Defender for Endpoint deployment
description: Learn how to set up the deployment for Microsoft Defender for Endpoint
keywords: deploy, setup, licensing validation, tenant configuration, network configuration
ms.prod: m365-security
ms.mktglfcycl: deploy
ms.sitesec: library
ms.pagetype: security
ms.author: macapara
author: mjcaparas
ms.localizationpriority: medium
manager: dansimp
audience: ITPro
ms.collection:
  - M365-security-compliance
  - m365solution-endpointprotect
  - m365solution-scenario
ms.custom: admindeeplinkDEFENDER
ms.topic: article
ms.technology: mde
---

# Set up Microsoft Defender for Endpoint deployment

[!INCLUDE [Microsoft 365 Defender rebranding](../../includes/microsoft-defender.md)]


**Applies to:**
- [Microsoft Defender for Endpoint](https://go.microsoft.com/fwlink/p/?linkid=2154037)
- [Microsoft 365 Defender](https://go.microsoft.com/fwlink/?linkid=2118804)

> Want to experience Microsoft Defender for Endpoint? [Sign up for a free trial.](https://signup.microsoft.com/create-account/signup?products=7f379fee-c4f9-4278-b0a1-e4c8c2fcdf7e&ru=https://aka.ms/MDEp2OpenTrial?ocid=docs-wdatp-exposedapis-abovefoldlink)

Deploying Defender for Endpoint is a three-phase process:

|[![deployment phase - prepare.](images/phase-diagrams/prepare.png)](prepare-deployment.md)<br>[Phase 1: Prepare](prepare-deployment.md) | ![deployment phase - setup](images/phase-diagrams/setup.png)<br>Phase 2: Setup | [![deployment phase - onboard](images/phase-diagrams/onboard.png)](onboarding.md)<br>[Phase 3: Onboard](onboarding.md)|
|---|---|---|
||*You are here!*||

You are currently in the set-up phase.

In this deployment scenario, you'll be guided through the steps on:

- Licensing validation
- Tenant configuration
- Network configuration

> [!NOTE]
> For the purpose of guiding you through a typical deployment, this scenario will only cover the use of Microsoft Endpoint Configuration Manager. Defender for Endpoint supports the use of other onboarding tools but won't cover those scenarios in the deployment guide. For more information, see [Onboard devices to Microsoft Defender for Endpoint](onboard-configure.md).

## Check license state

Checking for the license state and whether it got properly provisioned, can be done through the admin center or through the **Microsoft Azure portal**.

1. To view your licenses, go to the **Microsoft Azure portal** and navigate to the [Microsoft Azure portal license section](https://portal.azure.com/#blade/Microsoft_AAD_IAM/LicensesMenuBlade/Products).

   ![Image of Azure Licensing page.](images/atp-licensing-azure-portal.png)

1. Alternately, in the admin center, navigate to **Billing** \> **Subscriptions**.

    On the screen, you'll see all the provisioned licenses and their current **Status**.

    ![Image of billing licenses.](images/atp-billing-subscriptions.png)

## Cloud Service Provider validation

To gain access into which licenses are provisioned to your company, and to check the state of the licenses, go to the admin center.

1. From the **Partner portal**, select **Administer services > Office 365**.

2. Clicking on the **Partner portal** link will open the **Admin on behalf** option and will give you access to the customer admin center.

   ![Image of O365 admin portal.](images/atp-O365-admin-portal-customer.png)

## Tenant Configuration

Onboarding to Microsoft Defender for Endpoint is easy. From the navigation menu, select any item under the Endpoints section, or any Microsoft 365 Defender feature such as Incidents, Hunting, Action center, or Threat analytics to initiate the onboarding process.

From a web browser, navigate to the <a href="https://go.microsoft.com/fwlink/p/?linkid=2077139" target="_blank">Microsoft 365 Defender portal</a>.

## Network configuration

If the organization doesn't require the endpoints to use a Proxy to access the Internet, skip this section.

The Microsoft Defender for Endpoint sensor requires Microsoft Windows HTTP (WinHTTP) to report sensor data and communicate with the Microsoft Defender for Endpoint service. The embedded Microsoft Defender for Endpoint sensor runs in the system context using the LocalSystem account. The sensor uses Microsoft Windows HTTP Services (WinHTTP) to enable communication with the Microsoft Defender for Endpoint cloud service. The WinHTTP configuration setting is independent of the Windows Internet (WinINet) internet browsing proxy settings and can only discover a proxy server by using the following discovery methods:

- **Autodiscovery methods**:
  - Transparent proxy
  - Web Proxy Autodiscovery Protocol (WPAD)

  If a Transparent proxy or WPAD has been implemented in the network topology, there is no need for special configuration settings. For more information on Microsoft Defender for Endpoint URL exclusions in the proxy, see the [Proxy Service URLs](production-deployment.md#proxy-service-urls) section in this document for the URLs allow list or on [Configure device proxy and Internet connectivity settings](configure-proxy-internet.md#enable-access-to-microsoft-defender-for-endpoint-service-urls-in-the-proxy-server).

- **Manual static proxy configuration**:
  - Registry-based configuration
  - WinHTTP configured using netsh command

    Suitable only for desktops in a stable topology (for example: a desktop in a corporate network behind the same proxy).

### Configure the proxy server manually using a registry-based static proxy

Configure a registry-based static proxy to allow only Microsoft Defender for Endpoint sensor to report diagnostic data and communicate with Microsoft Defender for Endpoint services if a computer isn't permitted to connect to the Internet. The static proxy is configurable through Group Policy (GP). The group policy can be found under:

- Administrative Templates \> Windows Components \> Data Collection and Preview Builds \> Configure Authenticated Proxy usage for the Connected User Experience and Telemetry Service
- Set it to **Enabled** and select **Disable Authenticated Proxy usage**

1. Open the Group Policy Management Console.
2. Create a policy or edit an existing policy based off the organizational practices.
3. Edit the Group Policy and navigate to **Administrative Templates \> Windows Components \> Data Collection and Preview Builds \> Configure Authenticated Proxy usage for the Connected User Experience and Telemetry Service**.

   ![Image of Group Policy configuration.](images/atp-gpo-proxy1.png)

4. Select **Enabled**.
5. Select **Disable Authenticated Proxy usage**.
6. Navigate to **Administrative Templates \> Windows Components \> Data Collection and Preview Builds \> Configure connected user experiences and telemetry**.

    ![Image of Group Policy configuration setting.](images/atp-gpo-proxy2.png)

7. Select **Enabled**.
8. Enter the **Proxy Server Name**.

The policy sets two registry values `TelemetryProxyServer` as REG_SZ and `DisableEnterpriseAuthProxy` as REG_DWORD under the registry key `HKLM\Software\Policies\Microsoft\Windows\DataCollection`.

The registry value `TelemetryProxyServer` takes the following string format:

```text
<server name or ip>:<port>
```

For example: 10.0.0.6:8080

The registry value `DisableEnterpriseAuthProxy` should be set to 1.

### Configure the proxy server manually using netsh command

Use netsh to configure a system-wide static proxy.

> [!NOTE]
>
> - This will affect all applications including Windows services which use WinHTTP with default proxy.
> - Laptops that are changing topology (for example: from office to home) will malfunction with netsh. Use the registry-based static proxy configuration.

1. Open an elevated command line:
    1. Go to **Start** and type **cmd**.
    1. Right-click **Command prompt** and select **Run as administrator**.

2. Enter the following command and press **Enter**:

   ```PowerShell
   netsh winhttp set proxy <proxy>:<port>
   ```

   For example: netsh winhttp set proxy 10.0.0.6:8080

### Proxy Configuration for down-level devices

Down-Level devices include Windows 7 SP1 and Windows 8.1 workstations as well as Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, and versions of Windows Server 2016 prior to Windows Server CB 1803. These operating systems will have the proxy configured as part of the Microsoft Management Agent to handle communication from the endpoint to Azure. Refer to the Microsoft Management Agent Fast Deployment Guide for information on how a proxy is configured on these devices.

### Proxy Service URLs

URLs that include v20 in them are only needed if you have Windows 10, version 1803 or Windows 11 devices. For example, `us-v20.events.data.microsoft.com` is only needed if the device is on Windows 10, version 1803 or Windows 11.

If a proxy or firewall is blocking anonymous traffic, as Microsoft Defender for Endpoint sensor is connecting from system context, make sure anonymous traffic is permitted in the listed URLs.

The following downloadable spreadsheet lists the services and their associated URLs that your network must be able to connect to. Ensure there are no firewall or network filtering rules that would deny access to these URLs, or you may need to create an *allow* rule specifically for them.

<br>

****

|Spreadsheet of domains list|Description|
|---|---|
|![Thumb image for Microsoft Defender for Endpoint URLs spreadsheet.](images/mdatp-urls.png)|Spreadsheet of specific DNS records for service locations, geographic locations, and OS. <p> [Download the spreadsheet here.](https://download.microsoft.com/download/8/a/5/8a51eee5-cd02-431c-9d78-a58b7f77c070/mde-urls.xlsx)|
|

## Next step

![**Phase 3: Onboard**.](images/onboard.png) <br> [Phase 3: Onboard](onboarding.md): Onboard devices to the service so that the Microsoft Defender for Endpoint service can get sensor data from them.
