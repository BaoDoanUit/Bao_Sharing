### Business Requirement
- Add new column to the right-most column of the batch template "Bill867ID"
- New data validation for batch process
- 


Purpose of Manual Interval Usage
- Duquense .001 issue where the profile code can't currently profile because usage is so small
- Cases where we have an interval profile assigned but the usage comes in as summary
- Cases where we need to manually profile data for any reason
- One day usages where the utility doesn't follow the inclusive/exclusive rules so the profiling procedure can't load
- Any other cases or exceptions where we currently need to rely on IT ops to load data to retail_billing.bil.tbl_interval_usage_acnt.