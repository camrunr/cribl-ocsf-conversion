# OCSF Conversion Pack
----

Use this Pack to convert specific log types to OCSF schema. At this time the following are supported:

* AWS WAF logs (OCSF 4002)
* Okta System Authentication (OCSF 3002)
* Proofpoint TAP (OCSF 4009)

**This is a work in progress!** Use with Caution.

## Installation

See "Contributing to the Pack" below for using github integrations to install, upgrade, and contribute to the Pack

#### Requirements Section

## AWS WAF logs
Most often they would be collected from an S3 bucket. They should be in JSON format. [Example](https://docs.aws.amazon.com/waf/latest/developerguide/logging-examples.html). There is an example included with the Pack.

## Okta System Authentication logs
These are commonly collected from the Okta API. They should be in JSON format.

## Proofpoint TAP logs
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

# Contributing to the Pack

As of Cribl 4.13 you can install, upgrade and contribute to a pack directly through git. Below are instructions for doing this with Github. I recommend usually forking into your repo and pushing changes there to encourage collaboration and better change management.

* Fork this Pack from the [main repo](https://github.com/camrunr/cribl-ocsf-conversion) into your own repo
* Create a [fine-grained access token per GitHub's instructions](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens#creating-a-fine-grained-personal-access-token)
* In Cribl go to Packs -> Add Pack -> Import from Git
   * Enter the repo URL as `https://username:token@uri`
      * Example: `https://myuser:somecrazytoken@github.com/myuser/my-forked-pack-repo`
   * Click Import 
* You can sync your fork with the main release in github's interface
   * ie, any new changes in the main release will be pulled down into your repo
* You can sync your installation in Cribl with your fork by using the Upgrade option in the Packs inteface or API
   * ie, any changes present in your repo will be pulled into Cribl
* You can sync changes in your installed Pack to your fork by using the Publish to Git option in the Packs interface or API
   * ie, any changes made locally in Cribl will be pushed up to your fork repo
   * If you think your changes will benefit others in the community, you can issue a PR to the original repo

## Release Notes

### Version 0.5.1 - 2025-08-25
- No functional changes made!
- Updated this readme (only) to include github integration instructions

### Version 0.5.0 - 2025-01-30
- Added Proofpoint
- Optimized the Code function that translates original -> ocsf names

### Version 0.2.0 - 2024-12-19
- Added Okta System Authentication capabilities

### Version 0.1.0 - 2024-12-13
- Initial release with AWS WAF capabilities

# License
This Pack uses the Apache license. Do whatchalike.
