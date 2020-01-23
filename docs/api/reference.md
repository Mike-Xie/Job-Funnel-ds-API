
# 1. Table of Contents #
<!-- TOC -->

- [Table of Contents #](#table-of-contents-)
- [API Reference #](#api-reference-)
- [Resources #](#resources-)
	- [Searches ##](#searches-)
		- [The search object ###](#the-search-object-)
			- [Attributes ####](#attributes-)
			- [Example ####](#example-)
		- [The result object ###](#the-result-object-)
			- [Attributes ####](#attributes-)
			- [Example ####](#example-)
		- [The /search endpoint ###](#the-search-endpoint-)
			- [Arguments ####](#arguments-)
			- [Example request ####](#example-request-)
			- [Returns ####](#returns-)
	- [Job Details ##](#job-details-)
		- [The details object ###](#the-details-object-)
			- [Attributes ####](#attributes-)
			- [Example ####](#example-)
		- [The /details endpoint ###](#the-details-endpoint-)
			- [Arguments ####](#arguments-)
			- [Example request ####](#example-request-)
			- [Returns ####](#returns-)
- [Errors #](#errors-)

<!-- /TOC -->

# 2. API Reference #

Base URL: TBD

The API accepts `application/json` requests and returns `application/json` responses.


# 3. Resources #


## 3.1. Searches ##

Searches provide a way for users to search the database for jobs.

### 3.1.1. The search object ###

The search object is returned by [the /search endpoint](#313-the-search-endpoint).

#### 3.1.1.1. Attributes ####

`responses` *List*

A list of [result objects](#312-the-result-object). If no results were found, this list may be empty.

`count` *Int*

The count of results returned.

#### 3.1.1.2. Example ####
```json
{
	'count': 2,
	'responses': [
		{
			'title': 'Web Developer, Frontend',
			'job_id': 14631,
			'post_timestamp': 1579804925,
			'relevance': 1.0
		},
		{
			'title': 'Fullstack Engineer',
			'job_id': 14309,
			'post_timestamp': 1579800341,
			'relevance': 1.0
		}
	]
}
```

### 3.1.2. The result object ###

Several result objects are included in each [search object](#311-the-search-object), which is returned by [the /search endpoint](#313-the-search-endpoint).

#### 3.1.2.1. Attributes ####

`title` *String*

The title of the job.

`job_id` *Int*

The id of the job in the database.

`post_timestamp` *Int*

The time and date when the job was posted, in epoch format.

`relevance` *Float*

The relevance score of the job. Not yet implemented, so will always be 1.0.

#### 3.1.2.2. Example ####
```json
{
	'title': 'Technical Writer',
	'job_id': 14111,
	'post_timestamp': 1579721662,
	'relevance': 1.0
}
```

### 3.1.3. The /search endpoint ###

`/search` accepts GET or POST requests.

#### 3.1.3.1. Arguments ####

`title` *String*, Required

The job title to search for.

`count` *Int*, Optional

Maximum number of jobs to return. In the future, this will be ordered by relevance.

`threshold` *Float*, Optional

Minimum relevance of jobs to return. Not currently implemented.

`city` *String*, Optional

City in which to search.

`state_province` *String*, Optional

State or province in which to search.

`country` *String*, Optional

Country in which to search.

#### 3.1.3.2. Example request ####
```json
{
	'title': 'Developer',
	'count': 10,
	'threshold': 0.4,
	'state_province': 'Nevada',
	'country': 'United States'
}
```

#### 3.1.3.3. Returns ####

Returns a [search object](#311-the-search-object) if the search succeeds, or an [error](#3-errors) otherwise. Errors will usually be due to a missing required argument or malformed request.


## 3.2. Job Details ##

Job Details provide additional details about a job listing.

### 3.2.1. The details object ###

The details object is returned by [the /details endpoint](#322-the-details-endpoint).

#### 3.2.1.1. Attributes ####

`title` *String*

The title of the job.

`job_id` *Int*

The id of the job in the database.

`description` *String*

The description of the job.

`location_city` *String*

The city of the job.

`location_state_province` *String*

The state or province of the job.

`location_country` *String*

The country of the job.

`keywords` *List* of *String*

Keywords associated with the job.

`keyphrases` *List* of *String*

Keyphrases associated with the job.

`company_name` *String* or *null*

The company offering the job.

`company_description` *String* or *null*

The description of the company offering the job.

`company_revenue` *Int* or *null*

The revenue of the company offering the job, if available.

`company_size` *Int* or *null*

The employee count of the company offering the job, if available.

`pay_min` *Int* or *null*

The minimum salary of the job, if salary is a range.

`pay_max` *Int* or *null*

The maximum salary of the job, if salary is a range.

`pay_exact` *Int* or *null*

The salary of the job, if available.

`seniority` *String* or *null*

The seniority level of the job.

#### 3.2.1.2. Example ####

```json
{
	'title': 'Data Engineer',
	'job_id': 13299,
	'description': 'This is a long job description about the Data Engineer position. Requires 32 years of experience with Tensorflow, and four PhDs.',
	'location_city': 'Toronto',
	'location_state_province': 'Ontario',
	'location_country': 'Canada',
	'keywords': ['Tensorflow', 'Python', 'R', 'COBOL', 'Internship']
	'keyphrases': ['Data Pipeline', 'Share-based compensation']
	'company_name': 'George's Data Warehouse',
	'company_description': 'How hard can it be to convert a warehouse into the data kind?',
	'company_revenue': 15000,
	'company_size': null,
	'pay_min': null,
	'pay_max': null
	'pay_exact': 30000,
	'seniority': 'Entry-level'
}
```

### 3.2.2. The /details endpoint ###

`/details` accepts GET or POST requests.

#### 3.2.2.1. Arguments ####

`job_id` *Int*, Required

The job ID to get details for.

#### 3.2.2.2. Example request ####
```json
{
	'job_id': 15979
}
```

#### 3.2.2.3. Returns ####

Returns a [details object](#321-the-details-object) if the job is found, or an [error](#3-errors) otherwise. Errors will usually be due to an invalid job ID.


# 4. Errors #

TODO