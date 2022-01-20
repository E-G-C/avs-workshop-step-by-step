# Task 10: Run Recovery Plan

In this task, you will move the test VM back to the original protected site.
This task can be performed either from the protected site’s or the recovery
site’s SRM console. The steps are identical in both cases.

In the recovery site’s SRM console, provide credentials for the protected site,
by clicking on the **LOGIN** button.

![](media/bbc48c93c42a5d7ca108d5467488a473.png)

Select your recovery plan and select **RUN**.

![](media/45faf1d7335366a3f88250dcfbb5f936.png)

Follow the steps in the wizard. As you are now performing a planned failback to
the original protected site, select **Planned Migration** as the recovery type.

![](media/6d625f59d1fe1c74ce6b8785247570fb.png)

Monitor progress. When the recovery plan run completes, go to the primary site’s
vCenter and confirm that the test VM is back online and attached to the
**SRM-LAB** network segment.

![](media/5aa9178ac0d1b963948f0c202463cc1b.png)

Confirm that the test VM is fully operational by pinging it from your jump-box
(please note that the VM’s IP address might not be the same as shown in the
screenshots).

Now that the test VM is running in the protected site, you need to also restore
replication towards the recovery site. This is done by reprotecting the VM
again. In the protected site’s SRM console, select your recovery plan, click on
the **…** item in the actions bar and select **Reprotect**.

![](media/fd102a3e30838c8cf75dcaf0a6566351.png)

Follow the steps in the wizard, which are exactly the same as those described in
Task 9. This completes the lab for SRM Disaster Recovery scenario.

## Next Steps

[Module 4](module-4-index)

[Module 3 Index](module-3-index)

[Main Index](index)