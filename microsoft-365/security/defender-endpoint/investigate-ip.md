---
title: Investigate an IP address associated with an alert
description: Use the investigation options to examine possible communication between devices and external IP addresses.
keywords: investigate, investigation, IP address, alert, Microsoft Defender for Endpoint, external IP
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
  - m365-security-compliance
  - m365initiative-defender-endpoint
ms.topic: article
ms.date: 04/24/2018
ms.technology: mde
---

# Investigate an IP address associated with a Microsoft Defender for Endpoint alert

[!INCLUDE [Microsoft 365 Defender rebranding](../../includes/microsoft-defender.md)]


**Applies to:**
- [Microsoft Defender for Endpoint](https://go.microsoft.com/fwlink/p/?linkid=2154037)
- [Microsoft 365 Defender](https://go.microsoft.com/fwlink/?linkid=2118804)


> Want to experience Defender for Endpoint? [Sign up for a free trial.](https://signup.microsoft.com/create-account/signup?products=7f379fee-c4f9-4278-b0a1-e4c8c2fcdf7e&ru=https://aka.ms/MDEp2OpenTrial?ocid=docs-wdatp-investigateip-abovefoldlink)

Examine possible communication between your devices and external internet protocol (IP) addresses.

Identifying all devices in the organization that communicated with a suspected or known malicious IP address, such as Command and Control (C2) servers, helps determine the potential scope of breach, associated files, and infected devices.

You can find information from the following sections in the IP address view:

- IP worldwide
- Reverse DNS names
- Alerts related to this IP
- IP in organization
- Prevalence

## IP Worldwide and Reverse DNS names

The IP address details section shows attributes of the IP address such as its ASN and its Reverse DNS names.

## Alerts related to this IP

The **Alerts related to this IP** section provides a list of alerts that are associated with the IP.

## IP in organization

The **IP in organization** section provides details on the prevalence of the IP address in the organization.

## Prevalence

The **Prevalence** section displays how many devices have connected to this IP address, and when the IP was first and last seen. You can filter the results of this section by time period; the default period is 30 days.

## Most recent observed devices with IP

The **Most recent observed devices** with IP section provides a chronological view on the events and associated alerts that were observed on the IP address.

**Investigate an external IP:**

1. Select **IP** from the **Search bar** drop-down menu.
2. Enter the IP address in the **Search** field.
3. Click the search icon or press **Enter**.

Details about the IP address are displayed, including: registration details (if available), reverse IPs (for example, domains), prevalence of devices in the organization that communicated with this IP Address (during selectable time period), and the devices in the organization that were observed communicating with this IP address.

> [!NOTE]
> Search results will only be returned for IP addresses observed in communication with devices in the organization.

Use the search filters to define the search criteria. You can also use the timeline search box to filter the displayed results of all devices in the organization observed communicating with the IP address, the file associated with the communication and the last date observed.

Clicking any of the device names will take you to that device's view, where you can continue investigate reported alerts, behaviors, and events.

## Related topics

- [View and organize the Microsoft Defender for Endpoint Alerts queue](alerts-queue.md)
- [Manage Microsoft Defender for Endpoint alerts](manage-alerts.md)
- [Investigate Microsoft Defender for Endpoint alerts](investigate-alerts.md)
- [Investigate a file associated with a Microsoft Defender for Endpoint alert](investigate-files.md)
- [Investigate devices in the Microsoft Defender for Endpoint Devices list](investigate-machines.md)
- [Investigate a domain associated with a Microsoft Defender for Endpoint alert](investigate-domain.md)
- [Investigate a user account in Microsoft Defender for Endpoint](investigate-user.md)
