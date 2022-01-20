# Task 7: Test Recovery Plan

In this task you will test the recovery plan created in the previous one.

In the protected site’s SRM console, select the **Recovery Plans** tab, click on
the recovery plan you created and select the **TEST** action.

![](media/a054d39d7062275307af98d7baf77143.png)

Follow the steps in the wizard to launch the recovery plan test.

![](media/98c7cb7e3203d03971963ce584afc5fa.png)

Monitor progress in the SRM console and wait until the test completes
successfully.

![](media/c5d6a0bc5e94f1a8c20fe600112b5b4e.png)

Now log into the recovery site’s vCenter and confirm that the test VM has been
successfully powered on in the recovery site.

![](media/2c0dcb7c63919e37dc6f7a67dffef9cb.png)

As this was a recovery plan **test**:

-   The VM in the protected site has NOT been shut down;

-   The VM in the recovery site has been attached to an isolated network
    segment, as per the configuration you created in Task 5 (click on the
    **Networks** tab to double check).

You can now complete your recovery plan testing process by cleaning up the
recovery site. In the SRM console, select your recovery plan and click on the
**CLEANUP** button.

![](media/150c8d916f2ac294768954a472f24c7f.png)

Follow the steps in the wizard to launch the clean-up process.

## Next Steps

[Module 3](module-3-task-8)

[Module 3 Index](module-3-index)

[Main Index](index)