---
title: App Installer file update settings
description: Learn how to configure app updates by using the App Installer file.
author: mcleanbyron
ms.author: mcleans
ms.date: 12/12/2018
ms.topic: article
keywords: windows 10, uwp, msix
ms.localizationpriority: medium
ms.custom: RS5
---

# Configure update settings in the App Installer file

As mentioned in [App Installer file overview](app-installer-file-overview.md), you can configure the update behavior of the app in the App Installer file. This article explores the update options and their respective trade-offs.

You can configure the update behavior of the app by using the [UpdateSettings](https://docs.microsoft.com/uwp/schemas/appinstallerschema/element-update-settings) element. Here we explore the update options and their respective trade-offs.

In short, you can choose to check for updates two different ways:
1. Independently of the user launching the app.
2. Only when the user launches the app.

Additionally, you can choose to apply updates in two different ways:
1. By informing the user with a prompt.
2. Silently, without informing the user.

Finally, when you inform the user of an update, you can either force them to take the update before allowing them to launch the app, or you can allow them to launch the app and apply the update at an opportune time.

Specifically, the syntax that is available to you is the following:

- The [UpdateSettings](https://docs.microsoft.com/uwp/schemas/appinstallerschema/element-update-settings) element can have the following elements:

    - **OnLaunch**: Checks for updates on launch. This type of update can show UI and has the following attributes:

        - **ShowPrompt**: ABoolean that determines if UI will be shown to the user.

        - **UpdateBlocksActivation**: A Boolean that determines if the UI shown to the user allows the user to launch the app without taking the update, or if the user must take the update before launching the app. This attribute can be set to “true” only if **ShowPrompt** is set to “true”. **UpdateBlocksActivation** =“true” means the UI the user will see allows the user to take the update or close the app. **UpdateBlocksActivation** =“false” means the UI the user will see allows the user to take the update or start the app without updating. In the latter case, the update will be applied silently the next time the app is launched.

        - **HoursBetweenUpdateChecks**: An integer that indicates how often (in how many hours) the system will check for updates to the app. “0” to “255” inclusive. The default value is 24 (if this value is not specified). For example if HoursBetweenUpdateChecks = 3 then when the user launches the app, if the system has not checked for updates within the past 3 hours, it will check for updates now.  

    - **AutomaticBackgroundTask**: Checks for updates in the background every 8 hours independently of whether the user launched the app. This type of update cannot show UI.

    - **ForceUpdateFromAnyVersion**: Allows the app to update from version x to version x++ or to downgrade from version x to version x--. Without this element, the app can only move to a higher version.
