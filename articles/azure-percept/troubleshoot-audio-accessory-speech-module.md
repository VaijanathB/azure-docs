---
title: Troubleshoot issues with Azure Percept Audio and speech modules
description: Get troubleshooting tips for some of the more common issues found during the on-boarding experience
author: mimcco
ms.author: mimcco
ms.service: azure-percept
ms.topic: how-to
ms.date: 02/18/2021
ms.custom: template-how-to #Required; leave this attribute/value as-is.
---

# Azure Percept Audio and speech module troubleshooting

Use the guidelines below to troubleshoot voice assistant application issues.

## Collecting speech module logs

To run these commands, [connect to the Azure Percept DK Wi-Fi access point and connect to the dev kit over SSH](./how-to-ssh-into-percept-dk.md) and enter the commands in the SSH terminal.

```console
 iotedge logs azureearspeechclientmodule
```

To redirect any output to a .txt file for further analysis, use the following syntax:

```console
[command] > [file name].txt
```

After redirecting output to a .txt file, copy the file to your host PC via SCP:

```console
scp [remote username]@[IP address]:[remote file path]/[file name].txt [local host file path]
```

[local host file path] refers to the location on your host PC which you would like to copy the .txt file to. [remote username] is the SSH username chosen during the [on-boarding experience](./quickstart-percept-dk-set-up.md). If you did not set up an SSH login during the Azure Percept DK on-boarding experience, your remote username is root.

## Checking runtime status of the speech module

Check if the runtime status of **azureearspeechclientmodule** shows as **running**. To locate the runtime status of your device modules, open the [Azure portal](https://portal.azure.com/) and navigate to **All resources** -> **\<your IoT hub>** -> **IoT Edge** -> **\<your device ID>**. Click the **Modules** tab to see the runtime status of all installed modules.

:::image type="content" source="./media/troubleshoot-audio-accessory-speech-module/over-the-air-iot-edge-device-page.png" alt-text="Edge device page in the Azure portal.":::

If the runtime status of **azureearspeechclientmodule** is not listed as **running**, click **Set modules** -> **azureearspeechclientmodule**. On the **Module Settings** page, set **Desired Status** to **running** and click **Update**.

## Understanding Ear SoM LED indicators

You can use LED indicators to understand which state you device is in. Usually it takes around 2 minutes for the module to fully initialize after *power on*. As it goes through initialization steps you will see:

1. 1 center white LED - the device is powered on. 
2. 1 center white LED blinking - authentication is in progress. 
3. All three LEDs will change to blue once the device is authenticated and ready to use.

|LED|	LED State| 	Ear SoM Status|
|---|------------|----------------| 
|L02|	1x white, static on	|Power on |
|L02|	1x white, 0.5 Hz flashing|	Authentication in progress |
|L01 & L02 & L03|	3x blue, static on| 	Waiting for keyword|
|L01 & L02 & L03|	LED array flashing, 20fps |	Listening or speaking|
|L01 & L02 & L03|	LED array racing, 20fps|	Thinking|
|L01 & L02 & L03|	3x red, static on |	Mute|

## Next steps

See the [general troubleshooting guide](./troubleshoot-dev-kit.md) for more information on troubleshooting your Azure Percept DK.
