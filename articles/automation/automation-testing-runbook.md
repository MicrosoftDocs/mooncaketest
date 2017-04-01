---
title: Testing a runbook in Azure Automation | Azure
description: Before you publish a runbook in Azure Automation, you can test it to ensure that works as expected.  This article describes how to test a runbook and view its output.
services: automation
documentationcenter: ''
author: mgoedtel
manager: jwhit
editor: tysonn

ms.assetid: 7f7db785-52c0-4613-aa12-b02fd32a5182
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/12/2016
wacn.date: ''
ms.author: magoedte;bwren

---
# Testing a runbook in Azure Automation
When you test a runbook, the [Draft version](automation-creating-importing-runbook.md#publishing-a-runbook) is executed and any actions that it performs are completed. No job history is created, but the [Output](automation-runbook-output-and-messages.md#output-stream) and [Warning and Error](automation-runbook-output-and-messages.md#message-streams) streams are displayed in the Test output Pane. Messages to the [Verbose Stream](automation-runbook-output-and-messages.md#message-streams) are displayed in the Output Pane only if the [$VerbosePreference variable](automation-runbook-output-and-messages.md#preference-variables) is set to Continue.

Even though the draft version is being run, the runbook still executes the workflow normally and performs any actions against resources in the environment. For this reason, you should only test runbooks at non-production resources.

## To test a runbook in the Azure Classic Management Portal
1. [Open the Draft version of the runbook](automation-edit-textual-runbook.md#to-edit-a-runbook-with-the-azure-portal).
2. Click the **Test** button to start the test.  If the runbook has parameters, you will receive a dialog box to provide values to be used for the test.
3. You can stop or suspend the runbook while it is being tested with the buttons underneath the Output Pane. When you suspend the runbook, it completes the current activity before being suspended. Once the runbook is suspended, you can stop it or restart it.
7. Inspect the output from the runbook in the output pane.

## Next Steps
* To learn how to create or import a runbook, see [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md)
* To get started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)
* To learn more about configuring runboks to return status messages and errors, including recommended practices, see [Runbook output and messages in Azure Automation](automation-runbook-output-and-messages.md)