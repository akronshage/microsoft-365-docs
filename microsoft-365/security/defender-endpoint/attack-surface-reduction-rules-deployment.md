---
title: Deploy attack surface reduction rules
description: Provides guidance to deploy attack surface reduction rules.
keywords: Attack surface reduction rules deployment, ASR deployment, enable asr rules, configure ASR, host intrusion prevention system, protection rules, anti-exploit rules, anti-exploit, exploit rules, infection prevention rules, Microsoft Defender for Endpoint, configure ASR rules
search.product: eADQiWindows 10XVcnh
ms.prod: m365-security
ms.mktglfcycl: manage
ms.sitesec: library
ms.pagetype: security
ms.localizationpriority: medium
audience: ITPro
author: jweston-1
ms.author: v-jweston
ms.reviewer: oogunrinde, sugamar, jcedola
manager: dansimp
ms.custom: asr
ms.technology: mde
ms.topic: article
ms.collection: M365-security-compliance
---

# Attack surface reduction rules deployment guide

## Before you begin

Attack surfaces are all the places where your organization is vulnerable to cyberthreats and attacks. Your organization's attack surfaces includes all the places where an attacker could compromise your organization's devices or networks. Reducing your attack surface means protecting your organization's devices and network, which leaves attackers with fewer ways to attack. Configuring attack surface reduction (ASR) rules—one of many security features found in Microsoft Defender for Endpoint—can help.

ASR rules target certain software behaviors, such as:

- Launching executable files and scripts that attempt to download or run files
- Running obfuscated or otherwise suspicious scripts
- Behaviors that apps don't usually occur during normal day-to-day work

By reducing the different attack surfaces, you can help prevent attacks from happening in the first place.

During your initial preparation, it's vital that you understand the capabilities of the systems that you'll put in place. Understanding the capabilities will help you determine which ASR rules are most important for protecting your organization.

>[!IMPORTANT]
>This guide provides images and examples to help you decide how to configure ASR rules; these images and examples might not reflect the best configuration options for your environment.

Before you start, review [Overview of attack surface reduction](overview-attack-surface-reduction.md), and [Demystifying attack surface reduction rules - Part 1](https://techcommunity.microsoft.com/t5/microsoft-defender-for-endpoint/demystifying-attack-surface-reduction-rules-part-1/ba-p/1306420) for foundational information. To understand the areas of coverage and potential impact, familiarize yourself with the current set of ASR rules; see [Attack surface reduction rules](attack-surface-reduction-rules.md).

ASR rules are only one capability of the attack surface reduction capabilities within Microsoft Defender for Endpoint. This document will go into more detail on deploying ASR rules effectively to stop advanced threats like human-operated ransomware and other threats.  

### Rules by category

As outlined in [Use attack surface reduction rules to prevent malware infection](attack-surface-reduction.md), there are multiple attack surface reduction rules within MDE that you can enable to protect your organization. Following are the rules broken out by category:

<br/>

| Polymorphic threats | Lateral movement & credential theft | Productivity apps rules |  Email rules | Script rules | Misc rules |
|:---|:---|:---|:---|:---|:---|
| Block executable files from running unless they meet a prevalence (1000 machines), age (24 hrs), or trusted list criteria | Block process creations originating from PSExec and WMI commands | Block Office apps from creating executable content | Block executable content from email client and webmail | Block obfuscated JS/VBS/PS/macro code | Block abuse of exploited vulnerable signed drivers <sup>[[1](#fn1)]<sup></sup>  |
| Block untrusted and unsigned processes that run from USB | Block credential stealing from the Windows local security authority subsystem (lsass.exe)<sup>[[2](#fn1)]<sup></sup>   | Block Office apps from creating child processes |  Block only Office communication applications from creating child processes | Block JS/VBS from launching downloaded executable content | |
| Use advanced protection against ransomware | Block persistence through WMI event subscription | Block Office apps from injecting code into other processes | Block Office communication apps from creating child processes | | |
| | | Block Adobe Reader from creating child processes | | | |

(<a id="fn1">1</a>) _Block abuse of exploited vulnerable signed drivers_ isn't currently available in MEM Endpoint security. You can configure this rule using [MEM OMA-URI](enable-attack-surface-reduction.md#mem).

(<a id="fn1">2</a>) Some ASR rules generate considerable noise, but won't block functionality. For example, if you're updating Chrome; Chrome will access lsass.exe; passwords are stored in lsass on the device. However, Chrome should not be accessing local device lsass.exe. If you enable the rule to block access to lsass, it will generate a lot of events. Those events are good events because the software update process should not access lsass.exe. Enabling this rule will block Chrome updates from accessing lsass, but will not block Chrome from updating; this is also true of other applications that make unnecessary calls to lsass.exe. The _block access to lsass_ rule will block unnecessary calls to lsass, but won't block the application from running.

### Infrastructure requirements

Although multiple methods of implementing ASR rules are possible, this guide is based on an infrastructure consisting of:

- Azure Active Directory
- Microsoft Endpoint Management (MEM)
- Windows 10 and Windows 11 devices
- Microsoft Defender for Endpoint E5 or Windows E5 licenses

To take full advantage of ASR rules and reporting, we recommend using a Microsoft 365 Defender E5 or Windows E5 license, and A5. Learn more: [Minimum requirements for Microsoft Defender for Endpoint](minimum-requirements.md).

>[!Note]
>There are multiple methods to configure ASR rules. ASR rules can be configured using: Microsoft Endpoint Manager (MEM), PowerShell, Group Policy, Microsoft System Center Configuration Manager (SCCM), MEM OMA-URI.
>If you are using a different infrastructure configuration than what is listed for _Infrastructure requirements_ (above), you can learn more about deploying attack surface reduction rules using other configurations here: [Enable attack surface reduction rules](enable-attack-surface-reduction.md).  

### ASR rules dependencies

Microsoft Defender Antivirus must be enabled and configured as primary anti-virus solution, and must be in the following mode:

- Primary antivirus/antimalware solution  
- State: Active mode

Microsoft Defender Antivirus must not be in any of the following modes:

- Passive
- Passive Mode with Endpoint detection and response (EDR) in Block Mode
- Limited periodic scanning (LPS)
- Off

See: [Cloud-delivered protection and Microsoft Defender Antivirus](cloud-protection-microsoft-defender-antivirus.md).

### Cloud Protection (MAPS) must be enabled

Microsoft Defender Antivirus works seamlessly with Microsoft cloud services. These cloud protection services, also referred to as Microsoft Advanced Protection Service (MAPS), enhances standard real-time protection, arguably providing the best antivirus defense. Cloud protection is critical to preventing breaches from malware and a critical component of ASR rules.
[Turn on cloud-delivered protection in Microsoft Defender Antivirus](enable-cloud-protection-microsoft-defender-antivirus.md).

### Microsoft Defender Antivirus components must be current versions

The following Microsoft Defender Antivirus component versions must be no more than two versions older than the most-currently-available version:

- **Microsoft Defender Antivirus Platform update version**  - Microsoft Defender Antivirus platform is updated monthly.
- **Microsoft Defender Antivirus engine version** - Microsoft Defender Antivirus engine is updated monthly.
- **Microsoft Defender Antivirus security intelligence** - Microsoft continually updates Microsoft Defender security intelligence (also known as, definition and signature) to address the latest threats, and to refine detection logic.

Keeping Microsoft Defender Antivirus versions current helps reduce ASR rules false positive results and improves Microsoft Defender Antivirus detection capabilities. For more details on the current versions and how to update the different Microsoft Defender Antivirus components visit [Microsoft Defender Antivirus platform support](manage-updates-baselines-microsoft-defender-antivirus.md).

## ASR rules deployment phases

As with any new, wide-scale implementation which could potentially impact your line-of-business operations, it is important to be methodical in your planning and implementation. Because of the powerful capabilities of ASR rules in preventing malware, careful planning and deployment of these rules is necessary to ensure they work best for your unique customer workflows. To work in your environment, you need to plan, test, implement, and operationalize ASR rules carefully.  

> [!div class="mx-imgBorder"]
> ![ASR rules deployment phases](images/asr-rules-deployment-phases.png)

>[!Note]
>For Customers who are using a non-Microsoft HIPS and are transitioning to Microsoft Defender for Endpoint attack surface reduction rules:
>Microsoft advises customers to run their HIPS solution side-by-side with their ASR rules deployment until the moment you shift from Audit to Block mode. Keep in mind that you must reach out to your 3rd-party antivirus vendor for exclusion recommendations.  

## Phase 1: Plan

Starting to test ASR rules involves starting with the right business unit. You’ll want to start with a small group of people in a specific business unit. You can identify some ASR champions within a particular business unit who can provide real-world impact to the ASR rules and help you tune your implementation.

> [!div class="mx-imgBorder"]
> ![ASR rules planning steps](images/asr-rules-planning-steps.png)

### Start with the right business unit

How you select the business unit to roll out your ASR rules  deployment will depend on factors such as:

- Size of business unit
- Availability of ASR rules champions  
- Distribution and usage of:
  - Software
  - Shared folders
  - Use of scripts
  - Office macros
  - Other entities affected by ASR rules

Depending on your business needs, you might decide to include multiple business units to get a broad sampling of software, shared folders, scripts, macros, etc. Conversely, you might decide to limit the scope of your first ASR rules rollout to a single business unit, then repeat the entire ASR rules rollout process to your other business units, one-at-a-time.

### Identify ASR  rules champions

ASR  rules champions are members in your organization that will help with your initial ASR  rules rollout during the preliminary testing and implementation phases. Your champions are typically employees who are more technically adept, and who are not derailed by intermittent work-flow outages. The champions' involvement will continue throughout the broader expansion of ASR rules deployment to your organization. Your ASR rules champions will be first to experience each level of the ASR  rules rollout.

It is important to provide a feedback and response channel for your ASR rules champions to alert you to ASR rules-related work disruptions and receive ASR  rules-rollout related communications.

### Get inventory of line-of-business apps and understand the business unit processes

Having a full understanding of the applications and per-business-unit processes that are used across your organization is critical to a successful ASR rules deployment. Additionally, it is imperative that you understand how those apps are used within the various business units in your organization.
To start, you should get an inventory of the apps that are approved for use across the breadth of the organization. You can use tools such as the Microsoft 365 Apps admin center to help you inventory software applications. See: [Overview of inventory in the Microsoft 365 Apps admin center](/deployoffice/admincenter/inventory).

### Define reporting and response team  roles and responsibilities

Clearly articulating roles and responsibilities of persons responsible for monitoring and communicating ASR  rules status and activity is a core activity of ASR  maintenance. Therefore, it is important to determine:

- The person or team responsible for gathering reports
- How and with whom reports are shared
- How escalation is addressed for newly identified threats or unwanted blockages caused by ASR rules

Typical roles and responsibilities include:

- IT admins: Implement ASR rules, manage exclusions. Work with different business units on apps and processes. Assembling and sharing reports to stakeholders
- Certified security operations center (CSOC) analyst: Responsible for investing high-priority, blocked processes, to determine wither the threat is valid or not
- Chief information security officer (CISO): Responsible for the overall security posture and health of the organization

### Ring deployment

For large enterprises, Microsoft recommends deploying ASR  rules in “rings.” Rings are groups of devices that are visually represented as concentric circles that radiate outward like non-overlapping tree rings. When the innermost ring is successfully deployed, you can transition the next ring into the testing phase. Thorough assessment of your business units, ASR  rules champions, apps, and processes is imperative to defining your rings.
In most cases, your organization will have designed deployment rings for phased rollouts of Windows updates. You can use your existing ring design to implement ASR  rules.
See: [Create a deployment plan for Windows](/windows/deployment/update/create-deployment-plan)

## Phase 2: Test

Begin your ASR  rules deployment with ring 1.

> [!div class="mx-imgBorder"]
> ![ASR rules testing steps](images/asr-rules-testing-steps.png)

### Step 1: Test ASR rules using Audit

Begin the testing phase by turning on the ASR rules with the rules set to Audit, starting with your champion users or devices in ring 1. Typically, the recommendation is that you enable all the rules (in Audit) so that you can determine which rules are triggered during the testing phase. Note that rules that are set to Audit do not generally impact functionality of the entity or entities to which the rule is applied but do generate logged events for the evaluation; there is no effect on end users.

#### Configure ASR Rules using MEM

You can use Microsoft Endpoint Manager (MEM) Endpoint Security to configure custom ASR rules.

1. Open [Microsoft Endpoint Manager admin center](https://endpoint.microsoft.com/#home)
2. Go to **Endpoint Security** > **Attack surface reduction**.
3. Select **Create Policy**.
4. In **Platform**, select **Windows 10 and later**, and in **Profile**, select **Attack surface reduction rules**.
  
    > [!div class="mx-imgBorder"]
    > ![Configure ASR rules profile](images/asr-mem-create-profile.png)

5. Click **Create**.
6. In the **Basics** tab of the **Create profile** pane, in **Name** add a name for your policy. In **Description** add a description for your ASR rules policy.
7. In the **Configuration settings** tab, under **Attack Surface Reduction Rules**, set all rules to **Audit mode**.

    > [!div class="mx-imgBorder"]
    > ![Set ASR rules to Audit mode](images/asr-mem-configuration-settings.png)

    >[!Note]
    >There are variations in some ASR rules mode listings; _Blocked_ and _Enabled_ provide the same functionality.

8. [Optional] In the **Scope tags** pane, you can add tag information to specific devices. You can also use role-based access control and scope tags to make sure that the right admins have the right access and visibility to the right Intune objects. Learn more: [Use role-based access control (RBAC) and scope tags for distributed IT in Intune](/mem/intune/fundamentals/scope-tags).
9. In the **Assignments** pane, you can deploy or "assign" the profile to your user or device groups. Learn more: [Assign device profiles in Microsoft Intune](/mem/intune/configuration/device-profile-assign#exclude-groups-from-a-profile-assignment)
10. Review your settings in the **Review + create** pane. Click **Create** to apply the rules.

   > [!div class="mx-imgBorder"]
   > ![Activate ASR rules policy](images/asr-mem-review-create.png)

Your new attack surface reduction policy for ASR rules is listed in **Endpoint security | Attack surface reduction**.

   > [!div class="mx-imgBorder"]
   > ![Listed ASR rule policy](images/asr-mem-my-asr-rules.png)

### Step 2: Understand the Attack surface reduction rules reporting page in the Microsoft 365 Defender portal

The ASR  rules reporting page is found in **Microsoft 365 Defender portal** > **Reports** > **Attack surface reduction rules**. This page has three tabs:

- Detections
- Configuration
- Add exclusions

#### Detections tab

Provides a 30-day timeline of detected audit and blocked events.

> [!div class="mx-imgBorder"]
> ![Attack surface reduction rules detections tab](images/asr-defender365-01.png)

The Attack Surface reduction rules pane provides an overview of detected events on a per-rule basis.

>[!Note]
>There are some variations in ASR rules reports. Microsoft is in the process of updating the behavior of the ASR rules reports to provide a consistent experience.

> [!div class="mx-imgBorder"]
> ![Attack surface reduction rules rule detections](images/asr-defender365-01b.png)

Click **View detections** to open the **Detections** tab.

> [!div class="mx-imgBorder"]
> [ ![Attack surface reduction rules detections](images/asr-defender365-reports-detections.png) ](images/asr-defender365-reports-detections.png#lightbox)

The **GroupBy** and **Filter** pane provide the following options:

The **GroupBy** returns results set to the following groups:

- No grouping
- Detected file
- Audit or block
- Rule
- Source app
- Device
- User
- Publisher

> [!div class="mx-imgBorder"]
> [ ![Attack surface reduction rules detections GroupBy filter](images/asr-defender365-reports-detections.png) ](images/asr-defender365-reports-detections.png#lightbox)

**Filter** opens the **Filter on rules** page, which enables you to scope the results to only the selected ASR rules:

> [!div class="mx-imgBorder"]
> [ ![Attack surface reduction rules detections filter on rules](images/asr-defender365-filter.png) ](images/asr-defender365-filter.png#lightbox)

>[!Note]
>If you have a Microsoft Microsoft 365 Security E5 or A5, Windows E5 or A5 license, the following link opens the Microsoft Defender 365  Reports > [Attack surface reductions](https://security.microsoft.com/asr?viewid=detections) > Detections tab.

#### Configuration tab

Lists – on a per-computer basis – the aggregate state of ASR rules: Off, Audit, Block.

> [!div class="mx-imgBorder"]
> [ ![Attack surface reduction rules Configuration tab](images/asr-defender365-configurations.png) ](images/asr-defender365-configurations.png#lightbox)

On the Configurations tab, you can check – on a per-device basis – which ASR rules are enabled, and in which mode, by selecting the device for which you want to review ASR rules.

> [!div class="mx-imgBorder"]
> [ ![Attack surface reduction rules enabled and mode](images/asr-defender365-configurations.settings.png) ](images/asr-defender365-configurations.settings.png#lightbox)

The **Get started** link opens the Microsoft Endpoint Manager admin center, where you can create or modify an endpoint protection policy for ASR:

> [!div class="mx-imgBorder"]
> [ ![Attack surface reduction rules in MEM](images/asr-defender365-05b-mem1.png) ](images/asr-defender365-05b-mem1.png#lightbox)

In Endpoint security | Overview, select **Attack surface reduction**:

> [!div class="mx-imgBorder"]
> [ ![Attack surface reduction in MEM](images/asr-defender365-05b-mem2.png) ](images/asr-defender365-05b-mem2.png#lightbox)

The Endpoint Security | Attack surface reduction pane opens:

> [!div class="mx-imgBorder"]
> [ ![Endpoint security Asr pane](images/asr-defender365-05b-mem3.png) ](images/asr-defender365-05b-mem3.png#lightbox)

>[!Note]
>If you have a Microsoft Defender 365 E5 (or Windows E5?) license, this link will open the Microsoft Defender 365  Reports > Attack surface reductions > [Configurations](https://security.microsoft.com/asr?viewid=configuration) tab.

#### Add exclusions

This tab provides a method to select detected entities (for example, false positives) for exclusion. When exclusions are added, the report provides a summary of the expected impact.

>[!Note]
> Microsoft Defender Antivirus AV exclusions are honored by ASR rules.  See [Configure and validate exclusions based on extension, name, or location](configure-extension-file-exclusions-microsoft-defender-antivirus.md).

> [!div class="mx-imgBorder"]
> [ ![Endpoint security Asr tool](Images/asr-defender365-06d.png) ](Images/asr-defender365-06d.png#lightbox)

> [!Note]
>If you have a Microsoft Defender 365 E5 (or Windows E5?) license, this link will open the Microsoft Defender 365  Reports > Attack surface reductions > [Exclusions](https://security.microsoft.com/asr?viewid=exclusions) tab.

### Step 3: Assess impact

#### Review

Use the reporting page in the Microsoft 365 Defender portal to see which – if any – ASR rules have impacted the business unit process. Include feedback from your ASR champions as part of this process. Review the audit report to determine which rules have the most fired/triggered events, and which have the fewest.

Because ASR rules target a broad array of components, and those components will be called at varying intervals, it is difficult to predict how long it will take to obtain a useful sampling of ASR rules-triggered events in your organizations rings; however, Microsoft suggests a minimum of four weeks. For example, some ASR rules for Microsoft Office applications might trigger sooner and more frequently than the ASR rule to “Use advanced protection against ransomware.” Likewise, each ring will likely use applications and other components that are subject to ASR rules differently and with dissimilar frequency. You must make the determination of when testing is complete based on the results in your organization. For a better understanding, see [How long should I test an ASR rule in audit mode before enabling it?](attack-surface-reduction-faq.yml#how-long-should-i-test-an-asr-rule-in-audit-mode-before-enabling-it-).

#### Create exclusions

In many cases, an organization has files, or folders of files, for example that are known to be safe, and which might contain aspects that would trigger an ASR rule; audit mode will reveal such files and folders. For example, your organization might have a collection of Word or Excel documents that have macros enabled for specific purposes; such macros can trigger an ASR rule. In such cases, if audit mode identifies such files, you want to exclude these files or folders to prevent them from being captured by ASR rules. See [Exclude files and folders](enable-attack-surface-reduction.md#exclude-files-and-folders-from-asr-rules)

>[!Note]
>Keep in mind that Microsoft Defender Antivirus AV exclusions are honored by ASR rules. See [Configure and validate exclusions based on extension, name, or location](configure-extension-file-exclusions-microsoft-defender-antivirus.md).

If you determine a rule will broadly impact line-of-business operations in a detrimental way, you can leave the rule in audit so that you can continue to capture, or you can disable the rule entirely. Exclusions are easily enabled in **Microsoft 365 Defender** > **Reports** > **Attack surface reduction rules**. Simply select the entity or entities for which you want to create an exclusion.

Exclusions are easily enabled in **Microsoft 365 Defender** > **Reports** > **Attack surface reduction rules**. Simply select the entity or entities for which you want to create an exclusion.

> [!div class="mx-imgBorder"]
> [ ![ASR Create Exclusions](images/asr-defender365-06d.png) ](images/asr-defender365-06d.png#lightbox)

#### Create exclusions after review

In many cases, an organization has files, or folders of files, for example that are known to be safe, and which might contain aspects that would trigger an ASR rule; audit mode will reveal such files and folders. For example, your organization might have a collection of Word or Excel documents that have macros enabled for specific purposes; such macros can trigger an ASR rule. In such cases, if audit mode identifies such files, you want to exclude these files or folders to prevent them from being captured by ASR rules. See [Exclude files and folders](enable-attack-surface-reduction.md#exclude-files-and-folders-from-asr-rules).

>[!Note]
>Keep in mind that Microsoft Defender Antivirus AV exclusions are honored by ASR rules. See [Configure and validate exclusions based on extension, name, or location](configure-extension-file-exclusions-microsoft-defender-antivirus.md).

## Phase 3: Implement

The implementation phase moves the ring from testing into functional state.

> [!div class="mx-imgBorder"]
> ![ASR rules implementation steps](images/asr-rules-implementation-steps.png)

### Step 1: Transition ASR Rules from Audit to Block

1. After all exclusions are determined while in audit mode, start setting some ASR rules to "block" mode, starting with the rule that has the fewest triggered events. See” [Enable attack surface reduction rules](enable-attack-surface-reduction.md).
2. Review the reporting page in the Microsoft 365 Defender portal; see [Threat protection report in Microsoft Defender for Endpoint](threat-protection-reports.md). Also review feedback from your ASR champions.
3. Refine exclusions or create new exclusions as determined necessary.
4. Switch problematic rules back to Audit.

  >[!Note]
  >For problematic rules (rules creating too much noise), it is better to create exclusions than to turn rules off or switching back to Audit. You will have to determine what is best for your environment.

  >[!Tip]
  >When available, take advantage of the Warn mode setting in rules to limit disruptions. Enabling ASR rules in Warn mode enables you to capture triggered events and view their potential disruptions, without actually blocking end-user access. Learn more: [Warn mode for users](attack-surface-reduction.md#warn-mode-for-users).

#### How does Warn mode work?

Warn mode is effectively a Block instruction, but with the option for the user to “Unblock” subsequent executions of the given flow or app. Warn mode unblocks on a per device, user, file and process combination. The warn mode information is stored locally and has a duration of 24 hours.

### Step 2: Expand deployment to ring n + 1

When you are confident that you have correctly configured the ASR rules for ring 1, you can widen the scope of your deployment to the next ring (ring n + 1).

The deployment process, steps 1 – 3,  is essentially the same for each subsequent ring:

1. Test rules in Audit
2. Review ASR-triggered audit events in the Microsoft 365 Defender portal
3. Create exclusions
4. Review: refine, add, or remove exclusions as necessary
5. Set rules to “block”
6. Review the reporting page in the Microsoft 365 Defender portal.
7. Create exclusions.
8. Disable problematic rules or switch them back to Audit.

## Phase 4: Operationalize

After you have fully deployed the ASR rules to your organization, it is vital that your organization has processes in place to monitor and respond to ASR-related activities.

### Manage false positives

False positives/negatives can occur with any threat protection solution, including Microsoft Defender for Endpoint. In endpoint protection solutions, false positives are cases in which an entity (such as a file or process) is detected and identified as malicious, although the entity isn't actually a threat. In contrast, a false negative is an entity that was not detected as a threat but is actually malicious.
For additional information about attending to false positives and false negatives, see: [Address false positives/negatives in Microsoft Defender for Endpoint](defender-endpoint-false-positives-negatives.md)

### Keeping up with reports

Consistent, regular review of reports is an essential aspect of maintaining your ASR rules deployment and keeping abreast of newly emerging threats. Your organization should have scheduled reviews of ASR  rules events on a cadence that will keep current with ASR  rules-reported events. Depending on the size of your organization, this may be daily, hourly, or continuous monitoring.

### Hunting

One of the most powerful and coolest features of [Microsoft 365 Defender](https://securitycenter.microsoft.com) is advanced hunting. If you are not familiar with advanced hunting, please refer to the documentation: [Proactively hunt for threats with advanced hunting](/windows/security/threat-protection/microsoft-defender-atp/advanced-hunting-overview).

> [!div class="mx-imgBorder"]
> [ ![Microsoft 365 Defender Advanced hunting](images/asr-defender365-advanced-hunting2.png) ](images/asr-defender365-advanced-hunting2.png#lightbox)

Advanced hunting is a query-based (Kusto Query Language) threat-hunting tool that lets you explore up to 30 days of the captured (raw) data, that Microsoft Defender ATP Endpoint Detection and Response (EDR) collects from all your machines. Through advanced hunting you can proactively inspect events in order to locate interesting indicators and entities. The flexible access to data facilitates unconstrained hunting for both known and potential threats.

Through advanced hunting, it is possible to extract ASR rules information, create reports, and get in-depth information on the context of a given ASR rule audit or block event.

You can query ASR rules events from the DeviceEvents table in the advanced hunting section of the Microsoft 365 Defender portal. For example, a simple query such as the one below can report all the events that have ASR rules as data source, for the last 30 days, and will summarize them by the ActionType count, that in this case it will be the actual codename of the ASR rule.

> [!div class="mx-imgBorder"]
> ![Microsoft 365 Defender Advanced hunting query command line](images/asr-defender365-advanced-hunting3.png)

> [!div class="mx-imgBorder"]
> [ ![Microsoft 365 Defender Advanced hunting query results](images/asr-defender365-advanced-hunting4.png) ](images/asr-defender365-advanced-hunting4.png#lightbox)

The above shows that 187 events were registered for AsrLsassCredentialTheft (102 for Blocked and 85 for Audited), 2 events for AsrOfficeChildProcess (1 for Audited and 1 for Block) and 8 events for AsrPsexecWmiChildProcessAudited.

If you want to focus on the AsrOfficeChildProcess rule, and get details on the actual files and processes involved, change the filter for ActionType and replace the summarize line with a projection of the wanted fields (in this case they are DeviceName, FileName, FolderPath, etc.).

> [!div class="mx-imgBorder"]
> ![Microsoft 365 Defender Advanced hunting query focused](images/asr-defender365-advanced-hunting4b.png)

> [!div class="mx-imgBorder"]
> [ ![Microsoft 365 Defender Advanced hunting query focused results](images/asr-defender365-advanced-hunting5b.png) ](images/asr-defender365-advanced-hunting5b.png#lightbox)

The true benefit of advanced hunting is that you can shape the queries to your liking, so that you can see the exact story of what was happening, regardless of whether you want to pinpoint something on an individual machine, or you want to extract insights from your entire environment.

For additional information about additional hunting options, see [Demystifying attack surface reduction rules - Part 3](https://techcommunity.microsoft.com/t5/microsoft-defender-for-endpoint/demystifying-attack-surface-reduction-rules-part-3/ba-p/1360968).

## Reference

### Blogs

[Demystifying attack surface reduction rules - Part 1](https://techcommunity.microsoft.com/t5/microsoft-defender-for-endpoint/demystifying-attack-surface-reduction-rules-part-1/ba-p/1306420)

[Demystifying attack surface reduction rules - Part 2](https://techcommunity.microsoft.com/t5/microsoft-defender-for-endpoint/demystifying-attack-surface-reduction-rules-part-2/ba-p/1326565)

[Demystifying attack surface reduction rules - Part 3](https://techcommunity.microsoft.com/t5/microsoft-defender-for-endpoint/demystifying-attack-surface-reduction-rules-part-3/ba-p/1360968)

[Demystifying attack surface reduction rules - Part 4](https://techcommunity.microsoft.com/t5/microsoft-defender-for-endpoint/demystifying-attack-surface-reduction-rules-part-4/ba-p/1384425)

### ASR collection

[Overview of attack surface reduction](overview-attack-surface-reduction.md)

[Use attack surface reduction rules to prevent malware infection](attack-surface-reduction.md)

[Enable attack surface reduction rules](enable-attack-surface-reduction.md)

[Attack surface reduction rules](attack-surface-reduction-rules.md)

[Attack surface reduction FAQ](attack-surface-reduction-faq.yml)

### Microsoft Defender

[Address false positives/negatives in Microsoft Defender for Endpoint](defender-endpoint-false-positives-negatives.md)

[Cloud-delivered protection and Microsoft Defender Antivirus](cloud-protection-microsoft-defender-antivirus.md)

[Turn on cloud-delivered protection in Microsoft Defender Antivirus](enable-cloud-protection-microsoft-defender-antivirus.md)

[Configure and validate exclusions based on extension, name, or location](configure-extension-file-exclusions-microsoft-defender-antivirus.md)

[Microsoft Defender Antivirus platform support](manage-updates-baselines-microsoft-defender-antivirus.md)

[Overview of inventory in the Microsoft 365 Apps admin center](/deployoffice/admincenter/inventory)

[Create a deployment plan for Windows](/windows/deployment/update/create-deployment-plan)

[Use role-based access control (RBAC) and scope tags for distributed IT in Intune](/mem/intune/fundamentals/scope-tags)

[Assign device profiles in Microsoft Intune](/mem/intune/configuration/device-profile-assign#exclude-groups-from-a-profile-assignment)

### Management sites

[Microsoft Endpoint Manager admin center](https://endpoint.microsoft.com/#home)

[Attack surface reduction](https://security.microsoft.com/asr?viewid=detections)

[ASR rules Configurations](https://security.microsoft.com/asr?viewid=configuration)

[ASR rules Exclusions](https://security.microsoft.com/asr?viewid=exclusions)
