# tap-trustpilot

This is a [Singer](https://singer.io) tap that produces JSON-formatted data
following the [Singer
spec](https://github.com/singer-io/getting-started/blob/master/SPEC.md).

This tap:

- Pulls raw data from [TrustPilot](https://developers.trustpilot.com/)
- Extracts the following resources:
  - [Business Unit Reviews](https://developers.trustpilot.com/business-units-api#get-a-business-unit's-reviews)
  - [Consumers](https://developers.trustpilot.com/consumer-api#get-the-profile-of-the-consumer(with-#reviews-and-weblinks))
- Outputs the schema for each resource

This tap does _not_ support incremental replication!


### Configuration

Create a `config.json` file that looks like this:

```
{
    "access_key": "...",
    "client_secret": "...",
    "username": "user@email.com",
    "password": "hunter2",
    "business_unit_id": "123abc"
}
```

You can get the access key and client secret by logging into Trustpilot for Business and going to Integrations > APIs. You can get the business unit ID by using the Trustpilot API.

Create a catalog.json file by running the following command:

`tap-trustpilot -c config.json --discover > catalog.json` 

Then, in `catalog.json` under the `schema` for each type of stream (business units, reviews, consumers), add `"selected": true` to enable that type of stream in the export. 

---

Copyright &copy; 2018 Fishtown Analytics
