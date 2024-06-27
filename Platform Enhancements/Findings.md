## CI/CD
- No pipelines to deploy terraform
- Main branch is way behind production, not quite sure how it all should be managed.

## Snowflake
- What is in the repo is not always whats in Snowflake. Snowflake tasks and procedures have been deployed, and then added to the repo after, and been wrong. Nearly pointed prod data into a staging environment. 
- Some procs in staging have been called by `ROL_UKGI_AZ_SNOWFLAKE_DATA_ENGINEERING_C3` role, which has access to prod data, so no safeguards over misconfiguration. 
- Tasks don't have any alerting, so the team need to manually check if they've failed. 
- EDF are moving to multi-account
- PII retention is a worry
	- Remove PII at AWS end? scanning
- Should only have PII quote data for 45 days?

## Data Modelling
- Orphaned satellites with to FK to a hub
- Intention was the export data 

## Product
- We know what the basic needs are, exports to external systems, finance etc.
- What comes beyond that? How do we align the platform with the business priorities, deliver an actual product rather than ad-hoc requests.
- Who owns reporting etc? Where does the boundary sit?
- 




