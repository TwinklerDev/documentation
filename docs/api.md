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
     --data '{"access_token":"a6905525-3dc9-4e6a-abc5-b23faf5cea77", \
              "dummyval":42}'
```


# Project

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

All parameters are optional.

* "project_name" -- a descriptive name for the project
* "project_notes" -- text notes for the project
* "organisation_uid" -- UID of the organisation of the project; can only be used if the access token allows it 

**Response**

The response is a JSON object with a "result" object.

If the result is "success" then the UID of the newly created project is returned as "project_uid". "proj_cov_ver" is also returned with a value of 1.

**Example**

```
curl --request POST 'https://twinkler.io/api/v1/addproject' \
     --header 'Content-Type: application/json' \
     --data '{"access_token":"a6905525-3dc9-4e6a-abc5-b23faf5cea77", \
              "project_name":"My Project 1", \
              "project_notes": "Testing a new Twinkler project" \
             }'
```

## Update Project

Command: **updateproject**

Updates an existing project. Existing values are overwritten.

**POST parameters**

* "project_uid" -- UID of the project
* "project_name" -- (optional) a descriptive name for the project
* "project_notes" -- (optional) text notes for the project

**Response**

The response is a JSON object with a "result" object - 'success' or 'fail'.

**Example**

```
curl --request POST 'https://twinkler.io/api/v1/updateproject' \
     --header 'Content-Type: application/json' \
     --data '{"access_token":"a6905525-3dc9-4e6a-abc5-b23faf5cea77", \
              "project_uid":"550757de-952d-4f76-996e-ba90cb80b0c8", \
              "project_name":"Updated Project Name", \
              "project_notes": "Testing an updated note" \
             }'
```

## Delete Project

Command: **deleteproject**

Delete an existing project. All data, including sites and coverage of the project is permanently deleted.

**POST parameters**

* "project_uid" -- UID of the project to delete

**Response**

The response is a JSON object with a "result" object - 'success' or 'fail'.

**Example**

```
curl --request POST 'https://twinkler.io/api/v1/deleteproject' \
     --header 'Content-Type: application/json' \
     --data '{"access_token":"a6905525-3dc9-4e6a-abc5-b23faf5cea77", \
              "project_uid":"550757de-952d-4f76-996e-ba90cb80b0c8", \
             }'
```


# Site

See [Site Parameters](/parameters?id=site-parameters) for more information.

## Get Sites

Command: **getprojects**

Returns details for all sites in a project.

**POST parameters**

* "project_uid" -- UID of the project

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
     --data '{"access_token":"a6905525-3dc9-4e6a-abc5-b23faf5cea77" \
              "project_uid":"bd0daf4b-e820-45d6-8d8b-6e91748f5a14", \
             }'
```

## Add Site

Command: **addsite**

Creates a new site in a project.

**POST parameters**

* "project_uid" -- UID of the project to which the site will be added
* "lng" -- longitude of site (WGS84)
* "lat" -- latitude of site (WGS84)
* "site_name" -- (optional) a descriptive name for the site
* "site_notes" -- (optional) text notes for the site
* "site_externalid" -- (optional) a name or reference for the site used by external systems
* "site_tags" -- (optional) list of tags associated with the site

**Response**

The response is a JSON object with a "result" object.

If the result is "success" then the UID of the newly created site is returned as "site_uid".

**Example**

```
curl --request POST 'https://twinkler.io/api/v1/addsite' \
     --header 'Content-Type: application/json' \
     --data '{"access_token":"a6905525-3dc9-4e6a-abc5-b23faf5cea77", \
              "project_uid":"550757de-952d-4f76-996e-ba90cb80b0c8", \
              "longitude": 131.06227, \
              "latitude":, -25.35368, \
              "site_name":"My Site 1", \
              "site_notes": "Testing a new Twinkler site" \
             }'
```

## Update Site

Command: **updatesite**

Updates a site in a project. Existing values are overwritten and coverage are re-predicted if the site is moved.

**POST parameters**

* "project_uid" -- UID of the project that has the site to be updated
* "site_uid" -- UID of the the site to be updated
* "lng" -- (optional) longitude of site (WGS84)
* "lat" -- (optional) latitude of site (WGS84)
* "site_name" -- (optional) a descriptive name for the site
* "site_notes" -- (optional) text notes for the site
* "site_externalid" -- (optional) a name or reference for the site used by external systems
* "site_tags" -- (optional) list of tags associated with the site
* "address" -- (optional) text address of the site
* "change_locked" -- (optional boolean) whehther changes are permitted in the web interface
* "clusterable" -- (optional boolean) whether the site will form clusters in the web interface
* "color" -- (optional) color of the site in the web interface
* "image" -- (optional) representative image in the web interface

**Response**

The response is a JSON object with a "result" object - 'success' or 'fail'.

**Example**

```
curl --request POST 'https://twinkler.io/api/v1/updatesite' \
     --header 'Content-Type: application/json' \
     --data '{"access_token":"a6905525-3dc9-4e6a-abc5-b23faf5cea77", \
              "project_uid":"550757de-952d-4f76-996e-ba90cb80b0c8", \
              "site_uid":"bd0daf4b-e820-45d6-8d8b-6e91748f5a14", \
              "longitude": 131.06227, \
              "latitude":, -25.35368, \
              "site_name":"My Site 1", \
              "site_notes": "Testing a new Twinkler site" \
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
     --data '{"access_token":"a6905525-3dc9-4e6a-abc5-b23faf5cea77", \
              "project_uid":"550757de-952d-4f76-996e-ba90cb80b0c8", \
              "site_uid":"bd0daf4b-e820-45d6-8d8b-6e91748f5a14" \
             }'
```


# Coverage

## Get Coverages

Command: **getcoverages**

Returns details for all coverage predictions in a site.

**POST parameters**

* "project_uid" -- UID of the project
* "site_uid" -- UID of the site

**Response**

The response is a JSON object with a "result" object.

If the result is "success" then a "data" object is returned that contains an array of coverage objects. Each coverage object has the parameters listed below, which are described [here](https://twinkler-docs.s3.amazonaws.com/index.html#/parameters?id=coverage-parameters):

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
     --data '{"access_token":"a6905525-3dc9-4e6a-abc5-b23faf5cea77" \
              "project_uid":"550757de-952d-4f76-996e-ba90cb80b0c8", \
              "site_uid":"bd0daf4b-e820-45d6-8d8b-6e91748f5a14" \
             }'
```

## Add Coverage

Command: **addcoverage**

Creates a new coverage prediction in a site. The values of the coverage prediction parameters are determined in the following order:

1. Default parameter values (every parameter has a default value)
2. Values of the reference coverage, if `reference_coverage_uid` is supplied
3. Meta-Parameters (`radio_tech`, `scenario`, `band`), if they are supplied 
4. Any individual parameter, if supplied

The parameter ordering gives a lot of flexbility. As a mimimum 

**POST parameters**

* "project_uid" -- UID of the project
* "site_uid" -- UID of the site
* XXX

**Response**

XXX

**Example**

XXX

Prediction Parameter Precedence
1. Supplied parameter (one)
2. Supplied Radio System Meta-Parameter (some) - Technology / Scenario / Band
3. Reference coverage (UID) (all)
4. Default parameter (all)

## Update Coverage

Command: **updatecoverage**

XXX

**POST parameters**

* "project_uid" -- UID of the project
* "coverage_uid" -- UID of the site
* XXX

**Response**

XXX

**Example**

XXX

## Delete Coverage

Command: **deletecoverage**

XXX

**POST parameters**

* "project_uid" -- UID of the project
* "coverage_uid" -- UID of the site

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
* "site_uid" -- UID of the site
* XXX

**Response**

XXX

**Example**

XXX

