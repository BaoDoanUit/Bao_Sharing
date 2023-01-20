Link:  https://ces-ltd.atlassian.net/browse/RBC-21854

As a CES BLUE client who has fixed block reallocations <mark style="background: #BBFABBA6;">configured</mark>, there should be a flag available to designate the use of allocation factor 0 instead of null for cases where the reallocate process is unable to find any historical data.

As a CES BLUE client who has fixed block reallocations configured, the reallocation process should use 0’s instead of null for cases where client has this flag turned on.

As a CES BLUE client, the re-allocation process should have logic to determine allocations for cases where there are no active accounts as of the block start date or no active accounts as of the block end date (fix for RETOPS-23759)

![[RBC-21854]]