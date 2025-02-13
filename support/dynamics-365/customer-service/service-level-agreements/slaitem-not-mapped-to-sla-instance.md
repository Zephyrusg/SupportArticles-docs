---
title: SLA instances associated with a case don't have mapped SLA item
description: Provides a resolution for the Object reference not set to an instance of an object error that occurs when updating old cases and entities.
ms.reviewer: sdas
ms.author: ravimanne
ms.date: 07/18/2023
---
# Can't fill an SLA item for the SLA instances associated with the entity or case

This article provides a resolution for an issue where the service-level agreement (SLA) instances associated with the entity or case records don't have an SLA item ID filled.

## Symptoms

You can't update old cases and entities with an old SLA in a Unified Interface SLA, and you receive the following error message:

> System.NullReferenceException: Object reference not set to an instance of an object.  
> at Microsoft.Dynamics.SLAManagement.Plugins.SLAInstanceService.GetSLAInstance(String regardingId, Guid slaItemId).

## Cause

This issue occurs because the legacy SLA instances are still attached to the case but not in the **Cancelled** status.

## Resolution

To solve this issue, take the following steps:

1. Verify in test CRM instance that the record updates that get the error have SLA instances with no SLA item filled.

    Users can search for `slakpiinstances` records in **Advanced Find** by applying the filter for *SLA item is null* and the SLA with the ID mentioned in the telemetry error.

2. If the SLA items are no longer present on `slakpiinstances`, the current mitigation would be either to update the status of `slakpiinstances` to **Cancelled** or to delete `slakpiinstances`. You can also update the SLA item ID.

3. Follow the mitigation steps on test or lower environments where the issue is reproduced, and after confirmation, try on the affected environment.

> [!NOTE]
> This resolution applies only to old records that are getting errors. If newly created records also get this error, contact [Microsoft support](https://dynamics.microsoft.com/support/) for further assistance.

