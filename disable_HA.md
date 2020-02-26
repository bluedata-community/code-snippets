
We can put together something for internal use as there are a series of commands that you can run through to understand the state of the platform.

To suspend HA, you can run the following command on the current active primary controller:
```
/opt/bluedata/bundles/bluedata*/startscript --action suspendha
```

Once you resolve any issues, then you can resume HA with the following command:
```
/opt/bluedata/bundles/bluedata*/startscript --action resumeha
```

Here is the basic process:
1. From the primary controller, run
```bdconfig --getw```
and see if the hosts you expect to be primary and shadow are still designated as such or if they have switched (which would indicate a failover).

2. Run this on primary, shadow and arbiter and send the output.
```
/opt/bluedata/common-install/bd_mgmt/bin/bd_mgmt ha query_state
```

3. Run this on the primary controller and send the output:
```
/opt/bluedata/common-install/bd_mgmt/bin/bd_mgmt ha read_record bd_ha_record
```

4a. Run this on current primary and send the output:
```
pcs status
```
4b. If this shows an error like "Failed", run the following on primary and send the output:
crm_resource -P5. Check if ha engine is running on primary and shadow
ps auxf | grep ha_engine
11:46
There are a myriad of other questions that would also need to be collected. Things like: is the UI up and accessible? etc, etc.
