# 
# API V1

The Twinkler Application Programming Interface provides a means for non-browser applications to access the data and functionality of Twinkler.

Requests are sent as HTTP POSTS to `https://twinkler.io/api/v1/<command>`. The POST contents, in addition to the parameters specific to the command, also includes an `access_token` that is retrieved from the user's account in Twinkler. 

# Echo

Command: **echo**

Returns the parameters that were posted to it. It can be used to check connectivity and access. 

**POST parameters**

Any parameters can be sent. Or none at all.

**Response**

JSON with the parameters of the POST.

**Example**

```
curl --request POST 'https://twinkler.io/api/v1/echo' \
     --header 'Content-Type: application/json' \
     --data '{"access_token":"a6905525-3dc9-4e6a-abc5-b23faf5cea77",
              "dummyval":42}'
```


# Project Commands

## Get Projects

Command: **getprojects**

Returns the details of all projects the user has access to.

**POST parameters**

None.

**Response**

The response is a JSON object with a "result" object.

If the result is "success" then a "project_groups" object is also returned that contains the projects, which are grouped by ownership, using the "group_name" key. The group_name may be "own", "organisation" or "other".

The "projects" object is a list of project objects, where each project object has the keys:

* "access" -- the access rights for the API access token
* "name" -- the name of the project
* "notes" -- any notes associated with the project
* "owner" -- email address of the project owner
* "uid" -- unique ID of the project, used in API calls

**Example**

```
curl --request POST 'https://twinkler.io/api/v1/getprojects' \
     --header 'Content-Type: application/json' \
     --data '{"access_token":"a6905525-3dc9-4e6a-abc5-b23faf5cea77"}'
```

## Add Project

Command: **addproject**

Creates a new project.

**POST parameters**

| Parameter | Mandatory | Type | Description |
| - | - | - | - |
|project_name|N|String|a descriptive name for the project|
|project_notes|N|String|text notes for the project|
|organisation_uid|N|String|UID of the organisation of the project; can only be used if the access token allows it|

**Response**

The response is a JSON object with a "result" object.

If the result is "success" then the UID of the newly created project is returned as "project_uid". "proj_cov_ver" is also returned with a value of 1.

**Example**

```
curl --request POST 'https://twinkler.io/api/v1/addproject' \
     --header 'Content-Type: application/json' \
     --data '{"access_token":"a6905525-3dc9-4e6a-abc5-b23faf5cea77",
              "project_name":"My Project 1",
              "project_notes": "Testing a new Twinkler project"
             }'
```

## Update Project

Command: **updateproject**

Updates an existing project. Existing values are overwritten.

**POST parameters**

| Parameter | Mandatory | Type | Description |
| - | - | - | - |
|project_uid|Y|String|UID of the project|
|project_name|N|String|a descriptive name for the project|
|project_notes|N|String|text notes for the project|

**Response**

The response is a JSON object with a "result" object - 'success' or 'fail'.

**Example**

```
curl --request POST 'https://twinkler.io/api/v1/updateproject' \
     --header 'Content-Type: application/json' \
     --data '{"access_token":"a6905525-3dc9-4e6a-abc5-b23faf5cea77",
              "project_uid":"550757de-952d-4f76-996e-ba90cb80b0c8",
              "project_name":"Updated Project Name",
              "project_notes": "Testing an updated note"
             }'
```

## Delete Project

Command: **deleteproject**

Delete an existing project. All data, including sites and coverage of the project is permanently deleted.

**POST parameters**

| Parameter | Mandatory | Type | Description |
| - | - | - | - |
|project_uid|Y|String|UID of the project to delete|

**Response**

The response is a JSON object with a "result" object - 'success' or 'fail'.

**Example**

```
curl --request POST 'https://twinkler.io/api/v1/deleteproject' \
     --header 'Content-Type: application/json' \
     --data '{"access_token":"a6905525-3dc9-4e6a-abc5-b23faf5cea77",
              "project_uid":"550757de-952d-4f76-996e-ba90cb80b0c8"
             }'
```


# Site Commands

See [Site Parameters](/parameters?id=site-parameters) for more information.

## Get Sites

Command: **getprojects**

Returns details for all sites in a project.

**POST parameters**

| Parameter | Mandatory | Type | Description |
| - | - | - | - |
|project_uid|Y|String|UID of the project|

**Response**

The response is a JSON object with a "result" object.

If the result is "success" then a "data" object is returned that contains an array of site objects. Each site object has the following information:

* "site_uid" -- UID of the site
* "lng" -- longitude of site (WGS84)
* "lat" -- latitude of site (WGS84)
* "site_name" -- a descriptive name for the site
* "site_notes" -- text notes for the site
* "site_externalid" -- a name or reference for the site used by external systems
* "site_tags" -- list of tags associated with the site
* "address" -- text address of the site
* "change_locked" -- whehther changes are permitted in the web interface
* "clusterable" -- whether the site will form clusters in the web interface
* "color" -- color of the site in the web interface
* "image" -- representative image in the web interface

**Example**

```
curl --request POST 'https://twinkler.io/api/v1/getsites' \
     --header 'Content-Type: application/json' \
     --data '{"access_token":"a6905525-3dc9-4e6a-abc5-b23faf5cea77",
              "project_uid":"bd0daf4b-e820-45d6-8d8b-6e91748f5a14"
             }'
```

## Add Site

Command: **addsite**

Creates a new site in a project.

**POST parameters**

| Parameter | Mandatory | Type | Description |
| - | - | - | - |
|project_uid|Y|String|UID of the project that has the site to be updated|
|lng|Y|Number|longitude of site (WGS84)|
|lat|Y|Number|latitude of site (WGS84)|
|site_name|N|String|a descriptive name for the site|
|site_notes|N|String|text notes for the site|
|site_externalid|N|String|a name or reference for the site used by external systems|
|site_tags|N|Array of strings|list of tags associated with the site|
|address|N|String|text address of the site|

The following POST parameters that manipulate the site on the web interface may also be supplied.

| Parameter | Mandatory | Type | Description |
| - | - | - | - |
|change_locked|N|Boolean|whehther changes are permitted in the web interface|
|clusterable|N|Boolean|whether the site will form clusters in the web interface|
|color|N|String|color of the site in the web interface|
|image|N|String|representative image in the web interface|

**Response**

The response is a JSON object with a "result" object.

If the result is "success" then the UID of the newly created site is returned as "site_uid".

**Example**

```
curl --request POST 'https://twinkler.io/api/v1/addsite' \
     --header 'Content-Type: application/json' \
     --data '{"access_token":"a6905525-3dc9-4e6a-abc5-b23faf5cea77",
              "project_uid":"550757de-952d-4f76-996e-ba90cb80b0c8",
              "longitude": 131.06227,
              "latitude": -25.35368,
              "site_name":"My Site 1",
              "site_notes": "Testing a new Twinkler site"
             }'
```

## Update Site

Command: **updatesite**

Updates a site in a project. Existing values are overwritten and coverage are re-predicted if the site is moved.

**POST parameters**

| Parameter | Mandatory | Type | Description |
| - | - | - | - |
|project_uid|Y|String|UID of the project that has the site to be updated|
|site_uid|Y|String|UID of the site to be updated|
|lng|N|Number|longitude of site (WGS84)|
|lat|N|Number|latitude of site (WGS84)|
|site_name|N|String|a descriptive name for the site|
|site_notes|N|String|text notes for the site|
|site_externalid|N|String|a name or reference for the site used by external systems|
|site_tags|N|Array of strings|list of tags associated with the site|
|address|N|String|text address of the site|
|change_locked|N|Boolean|whehther changes are permitted in the web interface|
|clusterable|N|Boolean|whether the site will form clusters in the web interface|
|color|N|String|color of the site in the web interface|
|image|N|String|representative image in the web interface|

**Response**

The response is a JSON object with a "result" object - 'success' or 'fail'.

**Example**

```
curl --request POST 'https://twinkler.io/api/v1/updatesite' \
     --header 'Content-Type: application/json' \
     --data '{"access_token":"a6905525-3dc9-4e6a-abc5-b23faf5cea77",
              "project_uid":"550757de-952d-4f76-996e-ba90cb80b0c8",
              "site_uid":"bd0daf4b-e820-45d6-8d8b-6e91748f5a14",
              "longitude": 131.06227,
              "latitude": -25.35368,
              "site_name":"My Site 1",
              "site_notes": "Testing a new Twinkler site"
             }'
```

## Delete Site

Command: **deletesite**

Delete an existing site. All data, including coverage of the site is permanently deleted.

**POST parameters**

* "project_uid" -- UID of the project that contains the site to delete
* "site_uid" -- UID of the site to delete

**Response**

The response is a JSON object with a "result" object - 'success' or 'fail'.

**Example**

```
curl --request POST 'https://twinkler.io/api/v1/deletesite' \
     --header 'Content-Type: application/json' \
     --data '{"access_token":"a6905525-3dc9-4e6a-abc5-b23faf5cea77",
              "project_uid":"550757de-952d-4f76-996e-ba90cb80b0c8",
              "site_uid":"bd0daf4b-e820-45d6-8d8b-6e91748f5a14"
             }'
```


# Coverage Commands

## Get Coverages

Command: **getcoverages**

Returns the details in JSON for all coverage predictions of a site or sites.

**POST parameters**

| Parameter | Mandatory | Type | Description |
| - | - | - | - |
|project_uid|Y|String|UID of the project|
|site_uids|Y|String or Array of Strings|UID of the site or sites|

**Response**

The response is a JSON object with a "result" object.

If the result is "success" then a "data" object is returned that contains an array of coverage objects. Each coverage object has the parameters listed below, which are described **[here](parameters?id=coverage-parameters)**:

General Parameters
* site_uid
* coverage_uid
* coverage_tags
* coverage_external_id
* coverage_notes
* name

Meta-Parameters
* radio_tech
* scenario
* band

Prediction Parameters
* measurement_system
* pixel_size
* max_dist
* min_sigstr
* smoothing
* skip_water
* freq
* tx_antenna_uid
* tx_azimuth
* tx_height
* tx_elevation
* tx_power
* tx_system_loss
* radio_ch_loss
* rx_ant_gain
* rx_height
* rx_system_loss
* indoor_loss
* use_indoor_loss
* prop_model
* morphology
* itm_ModVar
* itm_RSiteCriteria
* itm_TSiteCriteria
* itm_deltaH
* itm_eno_ns_surfref
* itm_eps_dielect
* itm_pctConf
* itm_pctLoc
* itm_pctTime
* itm_pol
* itm_radio_climate
* itm_sgm_conductivity
* spm_K1
* spm_K2
* spm_K3
* spm_K4
* spm_K5
* spm_K6
* spm_K7
* spm_Kclutter
* spm_Khill
* spm_fclutter

**Example**

```
curl --request POST 'https://twinkler.io/api/v1/getcoverages' \
     --header 'Content-Type: application/json' \
     --data '{"access_token":"a6905525-3dc9-4e6a-abc5-b23faf5cea77",
              "project_uid":"550757de-952d-4f76-996e-ba90cb80b0c8",
              "site_uid":"bd0daf4b-e820-45d6-8d8b-6e91748f5a14"
             }'
```

## Add Coverage

Command: **addcoverage**

Creates a new coverage prediction in a site. The values of the coverage prediction parameters are selected in the 
following order:

1. Default prediction parameter values (every parameter has a default value).
2. Values of the reference coverage, if `reference_coverage_uid` is supplied.
3. Meta-Parameters (`radio_tech`, `scenario`, `band`), if they are supplied.
4. Individual parameter values, if they are supplied.

The parameter ordering gives a lot of flexbility. `project_uid` and `site_uid` must be supplied but all 
other prediction values are optional.

It can be good practice to at least supply a unique `name` to each coverage.

If the same radio configuration is being used repeatedly, a good approach is to 
create an initial coverage instance, note it's UID then supply the UID as `reference_coverage_uid` on every `addcoverage`
call after that.

**POST parameters**

| Parameter | Mandatory | Type | Description |
| - | - | - | - |
|project_uid|Y|String|UID of the project|
|site_uid|Y|String|UID of the site|
|reference_coverage_uid|N|String|UID of another coverage from which to copy all |
|All other|N|Various|See **[here](parameters?id=coverage-parameters)** for all other possible coverage parameters|


**Response**

The response is a JSON object with a “result” object - ‘success’ or ‘fail’.

If it's a failure then a "message" object will give the reason.

If it's successful then a "coverage_uid" object will give the UID of the newly created coverage.

**Example**

```
curl --request POST 'https://twinkler.io/api/v1/addcoverage' \
     --header 'Content-Type: application/json' \
     --data '{"access_token": "a6905525-3dc9-4e6a-abc5-b23faf5cea77",
              "project_uid": "550757de-952d-4f76-996e-ba90cb80b0c8",
              "site_uid": "bd0daf4b-e820-45d6-8d8b-6e91748f5a14",
              "reference_coverage_uid": "6e9c4ecd-3d81-4550-9d14-f19104e1114c",
              "tx_height": 30,
              "tx_azimuth": 180
             }'
```

## Update Coverage

Command: **updatecoverage**

Updates an existing coverage prediction with one or more new values. A new prediction is generated if required by the changed values.

**POST parameters**

| Parameter | Mandatory | Type | Description |
| - | - | - | - |
|project_uid|Y|String|UID of the project|
|coverage_uid|Y|String|UID of the coverage prediction|
|One or more coverage parameters|N|Various|See **[here](parameters?id=coverage-parameters)** for all possible coverage parameters|

**Response**

The response is a JSON object with a “result” object - ‘success’ or ‘fail’.

If it's a failure then a "message" object will give the reason.

If it's successful then a "coverage_uid" object will give the UID of the updated coverage prediction.

**Example**

```
curl --request POST 'https://twinkler.io/api/v1/updatecoverage' \
     --header 'Content-Type: application/json' \
     --data '{"access_token": "550757de-952d-4f76-996e-ba90cb80b0c8",
              "project_uid": "c8eb94a2-a834-4298-8019-2b122fae7b73",
              "site_uid": "0c55770c-12f3-492a-ae23-faf2135ab472",
              "coverage_uid": "b9cbcfe0-a5b6-4fdc-a0e3-ffc008c2370e",
              "tx_height": 35,
              "tx_azimuth": 200
             }'
```

## Delete Coverage

Command: **deletecoverage**

Deletes a coverage prediction.

**POST parameters**

* "project_uid" -- UID of the project
* "coverage_uid" -- UID of the site

**Response**

XXX

**Example**

XXX

## Get Coverage Vector

Command: **getcoveragevector**

GET (not POST)  getcoveragevector - png, tiff, jpeg?

XXX

**GET parameters**

* "project_uid" -- UID of the project
* file_type []
* coverage selectors ???

**Response**

XXX

**Example**

XXX

## Get Coverage Image

Command: **getcoverageimage**

GET (not POST)  getcoverageimage - png, tiff, jpeg?

XXX

**GET parameters**

* "project_uid" -- UID of the project
* "coverage_uid" -- UID of the coverage
* file_type
* color_scheme
* ???

**Response**

XXX

**Example**

XXX

