# Versioning, life cycle management and cross region replication

## S3 versioning

- Once enabled, _versioning cannot be disabled_, only suspended. Bucket needs to be re-created to not have versioning.
- Can integrate with life cycle rules, i.e. only save last 3 versions, …
- A new uploaded version will not be publicly accessible (if public access is enabled), but the old ones will still be
- Old versions can be accessed with the object URL that includes `?versionId=`
- Deleting a file simply places a _delete marker_ as a new version on the file. The file can be restored by deleting the delete marker.
- Versioning MFA delete capability requires MFA for deletion as an additional layer of security.

## S3 life cycle rules

- Automates moving objects between different storage tiers
- Can be used in conjunction with versioning (only apply to current/previous version)

## Cross region replication

- Versioning must be enabled on both source and destination bucket.
- Replicate between buckets in different regions.
- Only new objects are replicated when a replication rule is set up.
- Delete markers or deletes of individual versions are not replicated.
