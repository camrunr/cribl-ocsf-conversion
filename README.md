# OCSF Conversion Pack
----

Use this Pack to convert specific log types to OCSF schema. At this time the following are supported:

* AWS WAF logs (OCSF 4002)
* Okta System Authentication (OCSF 3002)
* Proofpoint TAP (OCSF 4009)

**This is a work in progress!** Use with Caution.


## Requirements Section

#### AWS WAF logs
Most often they would be collected from an S3 bucket. They should be in JSON format. [Example](https://docs.aws.amazon.com/waf/latest/developerguide/logging-examples.html). There is an example included with the Pack.

#### Okta System Authentication logs
These are commonly collected from the Okta API. They should be in JSON format.

#### Proofpoint TAP logs
Currently the pack supports those logs collected via API in JSON format. Syslog style may come at a later date.

## Using The Pack

The Pack is largely based on Global Variable definitions under the Pack's Knowledge tab. There will be a conversion dictionary defined there for each type of log conversion we support. 
   * Each key in the dictionary is a field name as it appears in the original log. 
   * Each value is the corresponding field name as it appears in the OCSF version of the log.

The dictionary is (optionally) created from a CSV lookup file using the `convert_lookup_noop` pipeline's code function. Copy-paste the resulting object from there into the config.

However, the simple translations of names are never enough for the complexity of OCSF. The pipeline will derive and add more fields as the schema, and your use case, requires.

#### For each data source:

1. Adjust the optional features of the appropriate OCSF pipeline as you desire.
2. Enable a route to point your event data to this Pack and the destination of choice.
   a. You may need to adjust the in-Pack routes to match events to the correct pipeline
3. You can define Schema and use the C.Schema() validation method to check your logs. However, this is a heavy function. Use with caution. 


# Release Notes

### Version 0.5.0 - 2025-01-30
- Added Proofpoint
- Optimized the Code function that translates original -> ocsf names

### Version 0.2.0 - 2024-12-19
- Added Okta System Authentication capabilities

### Version 0.1.0 - 2024-12-13
- Initial release with AWS WAF capabilities

# Contributing to the Pack
To contribute to the Pack fork the repo and submit a PR

# License
This Pack uses the Apache license. Do whatchalike.
