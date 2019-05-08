# ![LOGO](logo.png) StackExchange **flow**ground Connector

## Description

A generated **flow**ground connector for the StackExchange API (version 2.0).

Generated from: https://api.apis.guru/v2/specs/stackexchange.com/2.0/swagger.json<br/>
Generated at: 2019-05-07T17:44:12+03:00

## API Description

Stack Exchange is a network of 130+ Q&A communities including Stack Overflow.


## Authorization

Supported authorization schemes:
- OAuth2

For OAuth 2.0 you need to specify OAuth Client credentials as environment variables in the connector repository:
* `OAUTH_CLIENT_ID` - your OAuth client id
* `OAUTH_CLIENT_SECRET` - your OAuth client secret

## Actions

### Reads the properties for a set of access tokens.<br/>
>  <br/>
> {accessTokens} can contain up to 20 access tokens. These are obtained by authenticating a user using OAuth 2.0.<br/>
>  <br/>
> This method returns a list of access_tokens.

#### Input Parameters
* `accessTokens` - _required_ - String list (semicolon delimited).
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.


### Immediately expires the access tokens passed. This method is meant to allow an application to discard any active access tokens it no longer needs.<br/>
>  <br/>
> {accessTokens} can contain up to 20 access tokens. These are obtained by authenticating a user using OAuth 2.0.<br/>
>  <br/>
> This method returns a list of access_tokens.

#### Input Parameters
* `accessTokens` - _required_ - String list (semicolon delimited).
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.


### Returns all the undeleted answers in the system.<br/>
>  <br/>
> The sorts accepted by this method operate on the follow fields of the answer object:<br/>
>  - activity - last_activity_date<br/>
>  - creation - creation_date<br/>
>  - votes - score<br/>
>   activity is the default sort.<br/>
>  <br/>
>  It is possible to create moderately complex queries using sort, min, max, fromdate, and todate.<br/>
>  <br/>
> This method returns a list of answers.

#### Input Parameters
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number

* `min` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number

* `sort` - _optional_
    Possible values: activity, creation, votes.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Gets the set of answers identified by ids.<br/>
>  <br/>
> This is meant for batch fetcing of questions. A useful trick to poll for updates is to sort by activity, with a minimum date of the last time you polled.<br/>
>  <br/>
> {ids} can contain up to 100 semicolon delimited ids, to find ids programatically look for answer_id on answer objects.<br/>
>  <br/>
> The sorts accepted by this method operate on the follow fields of the answer object:<br/>
>  - activity - last_activity_date<br/>
>  - creation - creation_date<br/>
>  - votes - score<br/>
>   activity is the default sort.<br/>
>  <br/>
>  It is possible to create moderately complex queries using sort, min, max, fromdate, and todate.<br/>
>  <br/>
> This method returns a list of answers.

#### Input Parameters
* `ids` - _required_ - Number list (semicolon delimited).
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number

* `min` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number

* `sort` - _optional_
    Possible values: activity, creation, votes.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Gets the comments on a set of answers.<br/>
>  <br/>
> If you know that you have an answer id and need the comments, use this method. If you know you have a question id, use /questions/{id}/comments. If you are unsure, use /posts/{id}/comments.<br/>
>  <br/>
> {ids} can contain up to 100 semicolon delimited ids, to find ids programatically look for answer_id on answer objects.<br/>
>  <br/>
> The sorts accepted by this method operate on the follow fields of the comment object:<br/>
>  - creation - creation_date<br/>
>  - votes - score<br/>
>   creation is the default sort.<br/>
>  <br/>
>  It is possible to create moderately complex queries using sort, min, max, fromdate, and todate.<br/>
>  <br/>
> This method returns a list of comments.

#### Input Parameters
* `ids` - _required_ - Number list (semicolon delimited).
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = creation => date
sort = votes => number

* `min` - _optional_ - sort = creation => date
sort = votes => number

* `sort` - _optional_
    Possible values: creation, votes.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Passing valid access_tokens to this method causes the application that created them to be de-authorized by the user associated with each access_token. This will remove the application from their apps tab, and cause all other existing access_tokens to be destroyed.<br/>
>  <br/>
> This method is meant for uninstalling applications, recovering from access_token leaks, or simply as a stronger form of /access-tokens/{accessTokens}/invalidate.<br/>
>  <br/>
> Nothing prevents a user from re-authenticate to an application that has de-authenticated itself, the user will be prompted to approve the application again however.<br/>
>  <br/>
> {accessTokens} can contain up to 20 access tokens. These are obtained by authenticating a user using OAuth 2.0.<br/>
>  <br/>
> This method returns a list of access_tokens.

#### Input Parameters
* `accessTokens` - _required_ - String list (semicolon delimited).
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.


### Returns all the badges in the system.<br/>
>  <br/>
> Badge sorts are a tad complicated. For the purposes of sorting (and min/max) tag_based is considered to be greater than named.<br/>
>  <br/>
> This means that you can get a list of all tag based badges by passing min=tag_based, and conversely all the named badges by passing max=named, with sort=type.<br/>
>  <br/>
> For ranks, bronze is greater than silver which is greater than gold. Along with sort=rank, set max=gold for just gold badges, max=silver&min=silver for just silver, and min=bronze for just bronze.<br/>
>  <br/>
> rank is the default sort.<br/>
>  <br/>
> This method returns a list of badges.

#### Input Parameters
* `inname` - _optional_
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = rank => string
sort = name => string
sort = type => string

* `min` - _optional_ - sort = rank => string
sort = name => string
sort = type => string

* `sort` - _optional_
    Possible values: rank, name, type.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Gets all explicitly named badges in the system.<br/>
>  <br/>
> A named badged stands in opposition to a tag-based badge. These are referred to as general badges on the sites themselves.<br/>
>  <br/>
> For the rank sort, bronze is greater than silver which is greater than gold. Along with sort=rank, set max=gold for just gold badges, max=silver&min=silver for just silver, and min=bronze for just bronze.<br/>
>  <br/>
> rank is the default sort.<br/>
>  <br/>
> This method returns a list of badges.

#### Input Parameters
* `inname` - _optional_
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = rank => string
sort = name => string

* `min` - _optional_ - sort = rank => string
sort = name => string

* `sort` - _optional_
    Possible values: rank, name.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns recently awarded badges in the system.<br/>
>  <br/>
> As these badges have been awarded, they will have the badge.user property set.<br/>
>  <br/>
> This method returns a list of badges.

#### Input Parameters
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns the badges that are awarded for participation in specific tags.<br/>
>  <br/>
> For the rank sort, bronze is greater than silver which is greater than gold. Along with sort=rank, set max=gold for just gold badges, max=silver&min=silver for just silver, and min=bronze for just bronze.<br/>
>  <br/>
> rank is the default sort.<br/>
>  <br/>
> This method returns a list of badges.

#### Input Parameters
* `inname` - _optional_
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = rank => string
sort = name => string

* `min` - _optional_ - sort = rank => string
sort = name => string

* `sort` - _optional_
    Possible values: rank, name.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Gets the badges identified in id.<br/>
>  <br/>
> Note that badge ids are not constant across sites, and thus should be looked up via the /badges method. A badge id on a single site is, however, guaranteed to be stable.<br/>
>  <br/>
> Badge sorts are a tad complicated. For the purposes of sorting (and min/max) tag_based is considered to be greater than named.<br/>
>  <br/>
> This means that you can get a list of all tag based badges by passing min=tag_based, and conversely all the named badges by passing max=named, with sort=type.<br/>
>  <br/>
> For ranks, bronze is greater than silver which is greater than gold. Along with sort=rank, set max=gold for just gold badges, max=silver&min=silver for just silver, and min=bronze for just bronze.<br/>
>  <br/>
> rank is the default sort.<br/>
>  <br/>
> {ids} can contain up to 100 semicolon delimited ids, to find ids programatically look for badge_id on badge objects.<br/>
>  <br/>
> This method returns a list of badges.

#### Input Parameters
* `ids` - _required_ - Number list (semicolon delimited).
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = rank => string
sort = name => string
sort = type => string

* `min` - _optional_ - sort = rank => string
sort = name => string
sort = type => string

* `sort` - _optional_
    Possible values: rank, name, type.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns recently awarded badges in the system, constrained to a certain set of badges.<br/>
>  <br/>
> As these badges have been awarded, they will have the badge.user property set.<br/>
>  <br/>
> {ids} can contain up to 100 semicolon delimited ids, to find ids programatically look for badge_id on badge objects.<br/>
>  <br/>
> This method returns a list of badges.

#### Input Parameters
* `ids` - _required_ - Number list (semicolon delimited).
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Gets all the comments on the site.<br/>
>  <br/>
> If you're filtering for interesting comments (by score, creation date, etc.) make use of the sort paramter with appropriate min and max values.<br/>
>  <br/>
> If you're looking to query conversations between users, instead use the /users/{ids}/mentioned and /users/{ids}/comments/{toid} methods.<br/>
>  <br/>
> The sorts accepted by this method operate on the follow fields of the comment object:<br/>
>  - creation - creation_date<br/>
>  - votes - score<br/>
>   creation is the default sort.<br/>
>  <br/>
>  It is possible to create moderately complex queries using sort, min, max, fromdate, and todate.<br/>
>  <br/>
> This method returns a list of comments.

#### Input Parameters
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = creation => date
sort = votes => number

* `min` - _optional_ - sort = creation => date
sort = votes => number

* `sort` - _optional_
    Possible values: creation, votes.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Gets the comments identified in id.<br/>
>  <br/>
> This method is most useful if you have a cache of comment ids obtained through other means (such as /questions/{id}/comments) but suspect the data may be stale.<br/>
>  <br/>
> {ids} can contain up to 100 semicolon delimited ids, to find ids programatically look for comment_id on comment objects.<br/>
>  <br/>
> The sorts accepted by this method operate on the follow fields of the comment object:<br/>
>  - creation - creation_date<br/>
>  - votes - score<br/>
>   creation is the default sort.<br/>
>  <br/>
>  It is possible to create moderately complex queries using sort, min, max, fromdate, and todate.<br/>
>  <br/>
> This method returns a list of comments.

#### Input Parameters
* `ids` - _required_ - Number list (semicolon delimited).
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = creation => date
sort = votes => number

* `min` - _optional_ - sort = creation => date
sort = votes => number

* `sort` - _optional_
    Possible values: creation, votes.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Deletes a comment.<br/>
>  <br/>
> Use an access_token with write_access to delete a comment.<br/>
>  <br/>
> In practice, this method will never return an object.

#### Input Parameters
* `id` - _required_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.

* `preview` - _optional_

### Edit an existing comment.<br/>
>  <br/>
> Use an access_token with write_access to edit an existing comment.<br/>
>  <br/>
> This method return the created comment.

#### Input Parameters
* `id` - _required_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.

* `body` - _optional_
* `preview` - _optional_

### Returns the various error codes that can be produced by the API.<br/>
>  <br/>
> This method is provided for discovery, documentation, and testing purposes, it is not expected many applications will consume it during normal operation.<br/>
>  <br/>
> For testing purposes, look into the /errors/{id} method which simulates errors given a code.<br/>
>  <br/>
> This method returns a list of errors.

#### Input Parameters
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.


### This method allows you to generate an error.<br/>
>  <br/>
> This method is only intended for use when testing an application or library. Unlike other methods in the API, its contract is not frozen, and new error codes may be added at any time.<br/>
>  <br/>
> This method results in an error, which will be expressed with a 400 HTTP status code and setting the error* properties on the wrapper object.

#### Input Parameters
* `id` - _required_

### Returns a stream of events that have occurred on the site.<br/>
>  <br/>
> The API considers the following "events":<br/>
>  - posting a question<br/>
>  - posting an answer<br/>
>  - posting a comment<br/>
>  - editing a post<br/>
>  - creating a user<br/>
>   <br/>
>  <br/>
> Events are only accessible for 15 minutes after they occurred, and by default only events in the last 5 minutes are returned. You can specify the age of the oldest event returned by setting the since parameter.<br/>
>  <br/>
> It is advised that developers batch events by ids and make as few subsequent requests to other methods as possible.<br/>
>  <br/>
> This method returns a list of events.

#### Input Parameters
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.

* `since` - _optional_ - Unix date.

### Creates a new filter given a list of includes, excludes, a base filter, and whether or not this filter should be "unsafe".<br/>
>  <br/>
> Filter "safety" is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.<br/>
>  <br/>
> If no base filter is specified, the default filter is assumed. When building a filter from scratch, the none built-in filter is useful.<br/>
>  <br/>
> When the size of the parameters being sent to this method grows to large, problems can occur. This method will accept POST requests to mitigate this.<br/>
>  <br/>
> It is not expected that many applications will call this method at runtime, filters should be pre-calculated and "baked in" in the common cases. Furthermore, there are a number of built-in filters which cover common use cases.<br/>
>  <br/>
> This method returns a single filter.

#### Input Parameters
* `base` - _optional_
* `exclude` - _optional_ - String list (semicolon delimited).
* `include` - _optional_ - String list (semicolon delimited).
* `unsafe` - _optional_

### Returns the fields included by the given filters, and the "safeness" of those filters.<br/>
>  <br/>
> It is not expected that this method will be consumed by many applications at runtime, it is provided to aid in debugging.<br/>
>  <br/>
> {filters} can contain up to 20 semicolon delimited filters. Filters are obtained via calls to /filters/create, or by using a built-in filter.<br/>
>  <br/>
> This method returns a list of filters.

#### Input Parameters
* `filters` - _required_ - String list (semicolon delimited).

### Returns a user's inbox.<br/>
>  <br/>
> This method requires an access_token, with a scope containing "read_inbox".<br/>
>  <br/>
> This method returns a list of inbox items.

#### Input Parameters
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.


### Returns the unread items in a user's inbox.<br/>
>  <br/>
> This method requires an access_token, with a scope containing "read_inbox".<br/>
>  <br/>
> This method returns a list of inbox items.

#### Input Parameters
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `since` - _optional_ - Unix date.

### Returns a collection of statistics about the site.<br/>
>  <br/>
> Data to facilitate per-site customization, discover related sites, and aggregate statistics is all returned by this method.<br/>
>  <br/>
> This data is cached very aggressively, by design. Query sparingly, ideally no more than once an hour.<br/>
>  <br/>
> This method returns an info object.

#### Input Parameters
* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns the user associated with the passed access_token.<br/>
>  <br/>
> This method returns a user.

#### Input Parameters
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = reputation => number
sort = creation => date
sort = name => string
sort = modified => date

* `min` - _optional_ - sort = reputation => number
sort = creation => date
sort = name => string
sort = modified => date

* `sort` - _optional_
    Possible values: reputation, creation, name, modified.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns the answers owned by the user associated with the given access_token.<br/>
>  <br/>
> This method returns a list of answers.

#### Input Parameters
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number

* `min` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number

* `sort` - _optional_
    Possible values: activity, creation, votes.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns all of a user's associated accounts, given an access_token for them.<br/>
>  <br/>
> This method returns a list of network users.

#### Input Parameters
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.


### Returns the badges earned by the user associated with the given access_token.<br/>
>  <br/>
> This method returns a list of badges.

#### Input Parameters
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = rank => string
sort = name => string
sort = type => string

* `min` - _optional_ - sort = rank => string
sort = name => string
sort = type => string

* `sort` - _optional_
    Possible values: rank, name, type.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns the comments owned by the user associated with the given access_token.<br/>
>  <br/>
> This method returns a list of comments.

#### Input Parameters
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = creation => date
sort = votes => number

* `min` - _optional_ - sort = creation => date
sort = votes => number

* `sort` - _optional_
    Possible values: creation, votes.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns the comments owned by the user associated with the given access_token that are in reply to the user identified by {toId}.<br/>
>  <br/>
> This method returns a list of comments.

#### Input Parameters
* `toId` - _required_
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = creation => date
sort = votes => number

* `min` - _optional_ - sort = creation => date
sort = votes => number

* `sort` - _optional_
    Possible values: creation, votes.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns the questions favorites by the user associated with the given access_token.<br/>
>  <br/>
> This method returns a list of questions.

#### Input Parameters
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number
sort = added => date

* `min` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number
sort = added => date

* `sort` - _optional_
    Possible values: activity, creation, votes, added.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns the user identified by access_token's inbox.<br/>
>  <br/>
> This method requires an access_token, with a scope containing "read_inbox".<br/>
>  <br/>
> This method returns a list of inbox items.

#### Input Parameters
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns the unread items in the user identified by access_token's inbox.<br/>
>  <br/>
> This method requires an access_token, with a scope containing "read_inbox".<br/>
>  <br/>
> This method returns a list of inbox items.

#### Input Parameters
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.

* `since` - _optional_ - Unix date.

### Returns the comments mentioning the user associated with the given access_token.<br/>
>  <br/>
> This method returns a list of comments.

#### Input Parameters
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = creation => date
sort = votes => number

* `min` - _optional_ - sort = creation => date
sort = votes => number

* `sort` - _optional_
    Possible values: creation, votes.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns a record of merges that have occurred involving a user identified by an access_token.<br/>
>  <br/>
> This method allows you to take now invalid account ids and find what account they've become, or take currently valid account ids and find which ids were equivalent in the past.<br/>
>  <br/>
> This is most useful when confirming that an account_id is in fact "new" to an application.<br/>
>  <br/>
> Account merges can happen for a wide range of reasons, applications should not make assumptions that merges have particular causes.<br/>
>  <br/>
> Note that accounts are managed at a network level, users on a site may be merged due to an account level merge but there is no guarantee that a merge has an effect on any particular site.<br/>
>  <br/>
> This method returns a list of account_merge.

#### Input Parameters
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.


### Returns a user's notifications, given an access_token.<br/>
>  <br/>
> This method requires an access_token, with a scope containing "read_inbox".<br/>
>  <br/>
> This method returns a list of notifications.

#### Input Parameters
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns a user's unread notifications, given an access_token.<br/>
>  <br/>
> This method requires an access_token, with a scope containing "read_inbox".<br/>
>  <br/>
> This method returns a list of notifications.

#### Input Parameters
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns the privileges the user identified by access_token has.<br/>
>  <br/>
> This method returns a list of privileges.

#### Input Parameters
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns the questions owned by the user associated with the given access_token.<br/>
>  <br/>
> This method returns a list of questions.

#### Input Parameters
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number

* `min` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number

* `sort` - _optional_
    Possible values: activity, creation, votes.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns the questions that have active bounties offered by the user associated with the given access_token.<br/>
>  <br/>
> This method returns a list of questions.

#### Input Parameters
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number

* `min` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number

* `sort` - _optional_
    Possible values: activity, creation, votes.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns the questions owned by the user associated with the given access_token that have no answers.<br/>
>  <br/>
> This method returns a list of questions.

#### Input Parameters
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number

* `min` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number

* `sort` - _optional_
    Possible values: activity, creation, votes.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns the questions owned by the user associated with the given access_token that have no accepted answer.<br/>
>  <br/>
> This method returns a list of questions.

#### Input Parameters
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number

* `min` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number

* `sort` - _optional_
    Possible values: activity, creation, votes.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns the questions owned by the user associated with the given access_token that are not considered answered.<br/>
>  <br/>
> This method returns a list of questions.

#### Input Parameters
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number

* `min` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number

* `sort` - _optional_
    Possible values: activity, creation, votes.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns the reputation changed for the user associated with the given access_token.<br/>
>  <br/>
> This method returns a list of reputation changes.

#### Input Parameters
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns user's public reputation history.<br/>
>  <br/>
> This method returns a list of reputation_history.

#### Input Parameters
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns user's full reputation history, including private events.<br/>
>  <br/>
>  This method requires an access_token, with a scope containing "private_info".<br/>
>  <br/>
> This method returns a list of reputation_history.

#### Input Parameters
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns the suggested edits the user identified by access_token has submitted.<br/>
>  <br/>
> This method returns a list of suggested-edits.

#### Input Parameters
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = creation => date
sort = approval => date
sort = rejection => date

* `min` - _optional_ - sort = creation => date
sort = approval => date
sort = rejection => date

* `sort` - _optional_
    Possible values: creation, approval, rejection.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns the tags the user identified by the access_token passed is active in.<br/>
>  <br/>
> This method returns a list of tags.

#### Input Parameters
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = popular => number
sort = activity => date
sort = name => string

* `min` - _optional_ - sort = popular => number
sort = activity => date
sort = name => string

* `sort` - _optional_
    Possible values: popular, activity, name.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns the top 30 answers the user associated with the given access_token has posted in response to questions with the given tags.<br/>
>  <br/>
> This method returns a list of answers.

#### Input Parameters
* `tags` - _required_ - String list (semicolon delimited).
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number

* `min` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number

* `sort` - _optional_
    Possible values: activity, creation, votes.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns the top 30 questions the user associated with the given access_token has posted in response to questions with the given tags.<br/>
>  <br/>
> This method returns a list of questions.

#### Input Parameters
* `tags` - _required_ - String list (semicolon delimited).
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number
sort = hot => none
sort = week => none
sort = month => none
sort = relevance => none

* `min` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number
sort = hot => none
sort = week => none
sort = month => none
sort = relevance => none

* `sort` - _optional_
    Possible values: activity, creation, votes, hot, week, month, relevance.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns a subset of the actions the user identified by the passed access_token has taken on the site.<br/>
>  <br/>
> This method returns a list of user timeline objects.

#### Input Parameters
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns the user identified by access_token's top 30 tags by answer score.<br/>
>  <br/>
> This method returns a list of top tag objects.

#### Input Parameters
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns the user identified by access_token's top 30 tags by question score.<br/>
>  <br/>
> This method returns a list of top tag objects.

#### Input Parameters
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns the write permissions a user has via the api, given an access token.<br/>
>  <br/>
> The Stack Exchange API gives users the ability to create, edit, and delete certain types. This method returns whether the passed user is capable of performing those actions at all, as well as how many times a day they can.<br/>
>  <br/>
> This method does not consider the user's current quota (ie. if they've already exhausted it for today) nor any additional restrictions on write access, such as editing deleted comments.<br/>
>  <br/>
> This method returns a list of write_permissions.

#### Input Parameters
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns a user's notifications.<br/>
>  <br/>
> This method requires an access_token, with a scope containing "read_inbox".<br/>
>  <br/>
> This method returns a list of notifications.

#### Input Parameters
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.


### Returns a user's unread notifications.<br/>
>  <br/>
> This method requires an access_token, with a scope containing "read_inbox".<br/>
>  <br/>
> This method returns a list of notifications.

#### Input Parameters
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.


### Fetches all posts (questions and answers) on the site.<br/>
>  <br/>
> In many ways this method is the union of /questions and /answers, returning both sets of data albeit only the common fields.<br/>
>  <br/>
> Most applications should use the question or answer specific methods, but /posts is available for those rare cases where any activity is of intereset. Examples of such queries would be: "all posts on Jan. 1st 2011" or "top 10 posts by score of all time".<br/>
>  <br/>
> The sorts accepted by this method operate on the follow fields of the post object:<br/>
>  - activity - last_activity_date<br/>
>  - creation - creation_date<br/>
>  - votes - score<br/>
>   activity is the default sort.<br/>
>  <br/>
>  It is possible to create moderately complex queries using sort, min, max, fromdate, and todate.<br/>
>  <br/>
> This method returns a list of posts.

#### Input Parameters
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number

* `min` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number

* `sort` - _optional_
    Possible values: activity, creation, votes.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Fetches a set of posts by ids.<br/>
>  <br/>
> This method is meant for grabbing an object when unsure whether an id identifies a question or an answer. This is most common with user entered data.<br/>
>  <br/>
> {ids} can contain up to 100 semicolon delimited ids, to find ids programatically look for post_id, answer_id, or question_id on post, answer, and question objects respectively.<br/>
>  <br/>
> The sorts accepted by this method operate on the follow fields of the post object:<br/>
>  - activity - last_activity_date<br/>
>  - creation - creation_date<br/>
>  - votes - score<br/>
>   activity is the default sort.<br/>
>  <br/>
>  It is possible to create moderately complex queries using sort, min, max, fromdate, and todate.<br/>
>  <br/>
> This method returns a list of posts.

#### Input Parameters
* `ids` - _required_ - Number list (semicolon delimited).
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number

* `min` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number

* `sort` - _optional_
    Possible values: activity, creation, votes.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Gets the comments on the posts identified in ids, regardless of the type of the posts.<br/>
>  <br/>
> This method is meant for cases when you are unsure of the type of the post id provided. Generally, this would be due to obtaining the post id directly from a user.<br/>
>  <br/>
> {ids} can contain up to 100 semicolon delimited ids, to find ids programatically look for post_id, answer_id, or question_id on post, answer, and question objects respectively.<br/>
>  <br/>
> The sorts accepted by this method operate on the follow fields of the comment object:<br/>
>  - creation - creation_date<br/>
>  - votes - score<br/>
>   creation is the default sort.<br/>
>  <br/>
>  It is possible to create moderately complex queries using sort, min, max, fromdate, and todate.<br/>
>  <br/>
> This method returns a list of comments.

#### Input Parameters
* `ids` - _required_ - Number list (semicolon delimited).
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = creation => date
sort = votes => number

* `min` - _optional_ - sort = creation => date
sort = votes => number

* `sort` - _optional_
    Possible values: creation, votes.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns edit revisions for the posts identified in ids.<br/>
>  <br/>
> {ids} can contain up to 100 semicolon delimited ids, to find ids programatically look for post_id, answer_id, or question_id on post, answer, and question objects respectively.<br/>
>  <br/>
> This method returns a list of revisions.

#### Input Parameters
* `ids` - _required_ - Number list (semicolon delimited).
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns suggsted edits on the posts identified in ids.<br/>
>  <br/>
>  - creation - creation_date<br/>
>  - approval - approval_date<br/>
>  - rejection - rejection_date<br/>
>   creation is the default sort.<br/>
>  <br/>
>  {ids} can contain up to 100 semicolon delimited ids, to find ids programatically look for post_id, answer_id, or question_id on post, answer, and question objects respectively.<br/>
>  <br/>
> This method returns a list of suggested-edits.

#### Input Parameters
* `ids` - _required_ - Number list (semicolon delimited).
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = creation => date
sort = approval => date
sort = rejection => date

* `min` - _optional_ - sort = creation => date
sort = approval => date
sort = rejection => date

* `sort` - _optional_
    Possible values: creation, approval, rejection.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Create a new comment.<br/>
>  <br/>
> Use an access_token with write_access to create a new comment on a post.<br/>
>  <br/>
> This method returns the created comment.

#### Input Parameters
* `id` - _required_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.

* `body` - _optional_
* `preview` - _optional_

### Returns the earnable privileges on a site.<br/>
>  <br/>
> Privileges define abilities a user can earn (via reputation) on any Stack Exchange site.<br/>
>  <br/>
> While fairly stable, over time they do change. New ones are introduced with new features, and the reputation requirements change as a site matures.<br/>
>  <br/>
> This method returns a list of privileges.

#### Input Parameters
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Gets all the questions on the site.<br/>
>  <br/>
> This method allows you make fairly flexible queries across the entire corpus of questions on a site. For example, getting all questions asked in the the week of Jan 1st 2011 with scores of 10 or more is a single query with parameters sort=votes&min=10&fromdate=1293840000&todate=1294444800.<br/>
>  <br/>
> To constrain questions returned to those with a set of tags, use the tagged parameter with a semi-colon delimited list of tags. This is an and contraint, passing tagged=c;java will return only those questions with both tags. As such, passing more than 5 tags will always return zero results.<br/>
>  <br/>
> The sorts accepted by this method operate on the follow fields of the question object:<br/>
>  - activity - last_activity_date<br/>
>  - creation - creation_date<br/>
>  - votes - score<br/>
>  - hot - by the formula ordering the hot tab Does not accept min or max<br/>
>  - week - by the formula ordering the week tab Does not accept min or max<br/>
>  - month - by the formula ordering the month tab Does not accept min or max<br/>
>   activity is the default sort.<br/>
>  <br/>
>  It is possible to create moderately complex queries using sort, min, max, fromdate, and todate.<br/>
>  <br/>
> This method returns a list of questions.

#### Input Parameters
* `tagged` - _optional_ - String list (semicolon delimited).
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number
sort = hot => none
sort = week => none
sort = month => none
sort = relevance => none

* `min` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number
sort = hot => none
sort = week => none
sort = month => none
sort = relevance => none

* `sort` - _optional_
    Possible values: activity, creation, votes, hot, week, month, relevance.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns all the questions with active bounties in the system.<br/>
>  <br/>
> The sorts accepted by this method operate on the follow fields of the question object:<br/>
>  - activity - last_activity_date<br/>
>  - creation - creation_date<br/>
>  - votes - score<br/>
>   activity is the default sort.<br/>
>  <br/>
>  It is possible to create moderately complex queries using sort, min, max, fromdate, and todate.<br/>
>  <br/>
> This method returns a list of questions.

#### Input Parameters
* `tagged` - _optional_ - String list (semicolon delimited).
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number

* `min` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number

* `sort` - _optional_
    Possible values: activity, creation, votes.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns questions which have received no answers.<br/>
>  <br/>
> Compare with /questions/unanswered which mearly returns questions that the sites consider insufficiently well answered.<br/>
>  <br/>
> This method corresponds roughly with the this site tab.<br/>
>  <br/>
> To constrain questions returned to those with a set of tags, use the tagged parameter with a semi-colon delimited list of tags. This is an and contraint, passing tagged=c;java will return only those questions with both tags. As such, passing more than 5 tags will always return zero results.<br/>
>  <br/>
> The sorts accepted by this method operate on the follow fields of the question object:<br/>
>  - activity - last_activity_date<br/>
>  - creation - creation_date<br/>
>  - votes - score<br/>
>   activity is the default sort.<br/>
>  <br/>
>  It is possible to create moderately complex queries using sort, min, max, fromdate, and todate.<br/>
>  <br/>
> This method returns a list of questions.

#### Input Parameters
* `tagged` - _optional_ - String list (semicolon delimited).
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number

* `min` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number

* `sort` - _optional_
    Possible values: activity, creation, votes.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns questions the site considers to be unanswered.<br/>
>  <br/>
> Note that just because a question has an answer, that does not mean it is considered answered. While the rules are subject to change, at this time a question must have at least one upvoted answer to be considered answered.<br/>
>  <br/>
> To constrain questions returned to those with a set of tags, use the tagged parameter with a semi-colon delimited list of tags. This is an and contraint, passing tagged=c;java will return only those questions with both tags. As such, passing more than 5 tags will always return zero results.<br/>
>  <br/>
> Compare with /questions/no-answers.<br/>
>  <br/>
> This method corresponds roughly with the unanswered tab.<br/>
>  <br/>
> The sorts accepted by this method operate on the follow fields of the question object:<br/>
>  - activity - last_activity_date<br/>
>  - creation - creation_date<br/>
>  - votes - score<br/>
>   activity is the default sort.<br/>
>  <br/>
>  It is possible to create moderately complex queries using sort, min, max, fromdate, and todate.<br/>
>  <br/>
> This method returns a list of questions.

#### Input Parameters
* `tagged` - _optional_ - String list (semicolon delimited).
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number

* `min` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number

* `sort` - _optional_
    Possible values: activity, creation, votes.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns the questions identified in {ids}.<br/>
>  <br/>
> This is most useful for fetching fresh data when maintaining a cache of question ids, or polling for changes.<br/>
>  <br/>
> {ids} can contain up to 100 semicolon delimited ids, to find ids programatically look for question_id on question objects.<br/>
>  <br/>
> The sorts accepted by this method operate on the follow fields of the question object:<br/>
>  - activity - last_activity_date<br/>
>  - creation - creation_date<br/>
>  - votes - score<br/>
>   activity is the default sort.<br/>
>  <br/>
>  It is possible to create moderately complex queries using sort, min, max, fromdate, and todate.<br/>
>  <br/>
> This method returns a list of questions.

#### Input Parameters
* `ids` - _required_ - Number list (semicolon delimited).
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number

* `min` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number

* `sort` - _optional_
    Possible values: activity, creation, votes.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Gets the answers to a set of questions identified in id.<br/>
>  <br/>
> This method is most useful if you have a set of interesting questions, and you wish to obtain all of their answers at once or if you are polling for new or updates answers (in conjunction with sort=activity).<br/>
>  <br/>
> {ids} can contain up to 100 semicolon delimited ids, to find ids programatically look for question_id on question objects.<br/>
>  <br/>
> The sorts accepted by this method operate on the follow fields of the answer object:<br/>
>  - activity - last_activity_date<br/>
>  - creation - creation_date<br/>
>  - votes - score<br/>
>   activity is the default sort.<br/>
>  <br/>
>  It is possible to create moderately complex queries using sort, min, max, fromdate, and todate.<br/>
>  <br/>
> This method returns a list of answers.

#### Input Parameters
* `ids` - _required_ - Number list (semicolon delimited).
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number

* `min` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number

* `sort` - _optional_
    Possible values: activity, creation, votes.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Gets the comments on a question.<br/>
>  <br/>
> If you know that you have an question id and need the comments, use this method. If you know you have a answer id, use /answers/{ids}/comments. If you are unsure, use /posts/{ids}/comments.<br/>
>  <br/>
> {ids} can contain up to 100 semicolon delimited ids, to find ids programatically look for question_id on question objects.<br/>
>  <br/>
> The sorts accepted by this method operate on the follow fields of the comment object:<br/>
>  - creation - creation_date<br/>
>  - votes - score<br/>
>   creation is the default sort.<br/>
>  <br/>
>  It is possible to create moderately complex queries using sort, min, max, fromdate, and todate.<br/>
>  <br/>
> This method returns a list of comments.

#### Input Parameters
* `ids` - _required_ - Number list (semicolon delimited).
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = creation => date
sort = votes => number

* `min` - _optional_ - sort = creation => date
sort = votes => number

* `sort` - _optional_
    Possible values: creation, votes.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Gets questions which link to those questions identified in {ids}.<br/>
>  <br/>
> This method only considers questions that are linked within a site, and will never return questions from another Stack Exchange site.<br/>
>  <br/>
> A question is considered "linked" when it explicitly includes a hyperlink to another question, there are no other heuristics.<br/>
>  <br/>
> {ids} can contain up to 100 semicolon delimited ids, to find ids programatically look for question_id on question objects.<br/>
>  <br/>
> The sorts accepted by this method operate on the follow fields of the question object:<br/>
>  - activity - last_activity_date<br/>
>  - creation - creation_date<br/>
>  - votes - score<br/>
>  - rank - a priority sort by site applies, subject to change at any time Does not accept min or max<br/>
>   activity is the default sort.<br/>
>  <br/>
>  It is possible to create moderately complex queries using sort, min, max, fromdate, and todate.<br/>
>  <br/>
> This method returns a list of questions.

#### Input Parameters
* `ids` - _required_ - Number list (semicolon delimited).
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number
sort = rank => none

* `min` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number
sort = rank => none

* `sort` - _optional_
    Possible values: activity, creation, votes, rank.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns questions that the site considers related to those identified in {ids}.<br/>
>  <br/>
> The algorithm for determining if questions are related is not documented, and subject to change at any time. Futhermore, these values are very heavily cached, and may not update immediately after a question has been editted. It is also not guaranteed that a question will be considered related to any number (even non-zero) of questions, and a consumer should be able to handle a variable number of returned questions.<br/>
>  <br/>
> {ids} can contain up to 100 semicolon delimited ids, to find ids programatically look for question_id on question objects.<br/>
>  <br/>
> The sorts accepted by this method operate on the follow fields of the question object:<br/>
>  - activity - last_activity_date<br/>
>  - creation - creation_date<br/>
>  - votes - score<br/>
>  - rank - a priority sort by site applies, subject to change at any time Does not accept min or max<br/>
>   activity is the default sort.<br/>
>  <br/>
>  It is possible to create moderately complex queries using sort, min, max, fromdate, and todate.<br/>
>  <br/>
> This method returns a list of questions.

#### Input Parameters
* `ids` - _required_ - Number list (semicolon delimited).
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number
sort = rank => none

* `min` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number
sort = rank => none

* `sort` - _optional_
    Possible values: activity, creation, votes, rank.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns a subset of the events that have happened to the questions identified in id.<br/>
>  <br/>
> This provides data similar to that found on a question's timeline page.<br/>
>  <br/>
> Voting data is scrubbed to deter inferencing of voter identity.<br/>
>  <br/>
> {ids} can contain up to 100 semicolon delimited ids, to find ids programatically look for question_id on question objects.<br/>
>  <br/>
> This method returns a list of question timeline events.

#### Input Parameters
* `ids` - _required_ - Number list (semicolon delimited).
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns edit revisions identified by ids in {ids}.<br/>
>  <br/>
> {ids} can contain up to 20 semicolon delimited ids, to find ids programatically look for revision_guid on revision objects. Note that unlike most other id types in the API, revision_guid is a string.<br/>
>  <br/>
> This method returns a list of revisions.

#### Input Parameters
* `ids` - _required_ - Guid list (semicolon delimited).
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Searches a site for any questions which fit the given criteria.<br/>
>  <br/>
> This method is intentionally quite limited. For more general searching, you should use a proper internet search engine restricted to the domain of the site in question.<br/>
>  <br/>
> At least one of tagged or intitle must be set on this method. nottagged is only used if tagged is also set, for performance reasons.<br/>
>  <br/>
> tagged and nottagged are semi-colon delimited list of tags. At least 1 tag in tagged will be on each returned question if it is passed, making it the OR equivalent of the AND version of tagged on /questions.<br/>
>  <br/>
> The sorts accepted by this method operate on the follow fields of the question object:<br/>
>  - activity - last_activity_date<br/>
>  - creation - creation_date<br/>
>  - votes - score<br/>
>  - relevance - matches the relevance tab on the site itself Does not accept min or max<br/>
>   activity is the default sort.<br/>
>  <br/>
>  It is possible to create moderately complex queries using sort, min, max, fromdate, and todate.<br/>
>  <br/>
> This method returns a list of questions.

#### Input Parameters
* `tagged` - _optional_ - String list (semicolon delimited).
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number
sort = relevance => none

* `min` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number
sort = relevance => none

* `sort` - _optional_
    Possible values: activity, creation, votes, relevance.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.

* `intitle` - _optional_
* `nottagged` - _optional_ - String list (semicolon delimited).

### Searches a site for any questions which fit the given criteria.<br/>
>  <br/>
> Search criteria are expressed using the following parameters:<br/>
>   - q - a free form text parameter, will match all question properties based on an undocumented algorithm.<br/>
>  - accepted - true to return only questions with accepted answers, false to return only those without. Omit to elide constraint.<br/>
>  - answers - the minimum number of answers returned questions must have.<br/>
>  - body - text which must appear in returned questions' bodies.<br/>
>  - closed - true to return only closed questions, false to return only open ones. Omit to elide constraint.<br/>
>  - migrated - true to return only questions migrated away from a site, false to return only those not. Omit to elide constraint.<br/>
>  - notice - true to return only questions with post notices, false to return only those without. Omit to elide constraint.<br/>
>  - nottagged - a semicolon delimited list of tags, none of which will be present on returned questions.<br/>
>  - tagged - a semicolon delimited list of tags, of which at least one will be present on all returned questions.<br/>
>  - title - text which must appear in returned questions' titles.<br/>
>  - user - the id of the user who must own the questions returned.<br/>
>  - url - a url which must be contained in a post, may include a wildcard.<br/>
>  - views - the minimum number of views returned questions must have.<br/>
>  - wiki - true to return only community wiki questions, false to return only non-community wiki ones. Omit to elide constraint.<br/>
>   <br/>
> At least one additional parameter must be set if nottagged is set, for performance reasons.<br/>
>  <br/>
> The sorts accepted by this method operate on the follow fields of the question object:<br/>
>  - activity - last_activity_date<br/>
>  - creation - creation_date<br/>
>  - votes - score<br/>
>  - relevance - matches the relevance tab on the site itself Does not accept min or max<br/>
>   activity is the default sort.<br/>
>  <br/>
>  It is possible to create moderately complex queries using sort, min, max, fromdate, and todate.<br/>
>  <br/>
> This method returns a list of questions.

#### Input Parameters
* `tagged` - _optional_ - String list (semicolon delimited).
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number
sort = relevance => none

* `min` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number
sort = relevance => none

* `sort` - _optional_
    Possible values: activity, creation, votes, relevance.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.

* `accepted` - _optional_
    Possible values: true, false.
* `answers` - _optional_
* `body` - _optional_
* `closed` - _optional_
    Possible values: true, false.
* `migrated` - _optional_
    Possible values: true, false.
* `notice` - _optional_
    Possible values: true, false.
* `nottagged` - _optional_ - String list (semicolon delimited).
* `q` - _optional_
* `title` - _optional_
* `url` - _optional_
* `user` - _optional_
* `views` - _optional_
* `wiki` - _optional_
    Possible values: true, false.

### Returns questions which are similar to a hypothetical one based on a title and tag combination.<br/>
>  <br/>
> This method is roughly equivalent to a site's related questions suggestion on the ask page.<br/>
>  <br/>
> This method is useful for correlating data outside of a Stack Exchange site with similar content within one.<br/>
>  <br/>
> Note that title must always be passed as a parameter. tagged and nottagged are optional, semi-colon delimited lists of tags.<br/>
>  <br/>
> If tagged is passed it is treated as a preference, there is no guarantee that questions returned will have any of those tags. nottagged is treated as a requirement, no questions will be returned with those tags.<br/>
>  <br/>
> The sorts accepted by this method operate on the follow fields of the question object:<br/>
>  - activity - last_activity_date<br/>
>  - creation - creation_date<br/>
>  - votes - score<br/>
>  - relevance - order by "how similar" the questions are, most likely candidate first with a descending order Does not accept min or max<br/>
>   activity is the default sort.<br/>
>  <br/>
>  It is possible to create moderately complex queries using sort, min, max, fromdate, and todate.<br/>
>  <br/>
> This method returns a list of questions.

#### Input Parameters
* `tagged` - _optional_ - String list (semicolon delimited).
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number
sort = relevance => none

* `min` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number
sort = relevance => none

* `sort` - _optional_
    Possible values: activity, creation, votes, relevance.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.

* `nottagged` - _optional_ - String list (semicolon delimited).
* `title` - _optional_

### Returns all sites in the network.<br/>
>  <br/>
> This method allows for discovery of new sites, and changes to existing ones. Be aware that unlike normal API methods, this method should be fetched very infrequently, it is very unusual for these values to change more than once on any given day. It is suggested that you cache its return for at least one day, unless your app encounters evidence that it has changed (such as from the /info method).<br/>
>  <br/>
> The pagesize parameter for this method is unbounded, in acknowledgement that for many applications repeatedly fetching from /sites would complicate start-up tasks needlessly.<br/>
>  <br/>
> This method returns a list of sites.

#### Input Parameters
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.


### Returns all the suggested edits in the systems.<br/>
>  <br/>
> This method returns a list of suggested-edits.<br/>
>  <br/>
> The sorts accepted by this method operate on the follow fields of the suggested_edit object:<br/>
>  - creation - creation_date<br/>
>  - approval - approval_date Does not return unapproved suggested_edits<br/>
>  - rejection - rejection_date Does not return unrejected suggested_edits<br/>
>   creation is the default sort.<br/>
>  <br/>
>  It is possible to create moderately complex queries using sort, min, max, fromdate, and todate.

#### Input Parameters
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = creation => date
sort = approval => date
sort = rejection => date

* `min` - _optional_ - sort = creation => date
sort = approval => date
sort = rejection => date

* `sort` - _optional_
    Possible values: creation, approval, rejection.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns suggested edits identified in ids.<br/>
>  <br/>
> {ids} can contain up to 100 semicolon delimited ids, to find ids programatically look for suggested_edit_id on suggested_edit objects.<br/>
>  <br/>
> The sorts accepted by this method operate on the follow fields of the suggested_edit object:<br/>
>  - creation - creation_date<br/>
>  - approval - approval_date Does not return unapproved suggested_edits<br/>
>  - rejection - rejection_date Does not return unrejected suggested_edits<br/>
>   creation is the default sort.<br/>
>  <br/>
>  It is possible to create moderately complex queries using sort, min, max, fromdate, and todate.<br/>
>  <br/>
> This method returns a list of suggested-edits.

#### Input Parameters
* `ids` - _required_ - Number list (semicolon delimited).
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = creation => date
sort = approval => date
sort = rejection => date

* `min` - _optional_ - sort = creation => date
sort = approval => date
sort = rejection => date

* `sort` - _optional_
    Possible values: creation, approval, rejection.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns the tags found on a site.<br/>
>  <br/>
> The inname parameter lets a consumer filter down to tags that contain a certain substring. For example, inname=own would return both "download" and "owner" amongst others.<br/>
>  <br/>
> This method returns a list of tags.<br/>
>  <br/>
> The sorts accepted by this method operate on the follow fields of the tag object:<br/>
>  - popular - count<br/>
>  - activity - the creation_date of the last question asked with the tag<br/>
>  - name - name<br/>
>   popular is the default sort.<br/>
>  <br/>
>  It is possible to create moderately complex queries using sort, min, max, fromdate, and todate.

#### Input Parameters
* `inname` - _optional_
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = popular => number
sort = activity => date
sort = name => string

* `min` - _optional_ - sort = popular => number
sort = activity => date
sort = name => string

* `sort` - _optional_
    Possible values: popular, activity, name.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns the tags found on a site that only moderators can use.<br/>
>  <br/>
> The inname parameter lets a consumer filter down to tags that contain a certain substring. For example, inname=own would return both "download" and "owner" amongst others.<br/>
>  <br/>
> This method returns a list of tags.<br/>
>  <br/>
> The sorts accepted by this method operate on the follow fields of the tag object:<br/>
>  - popular - count<br/>
>  - activity - the creation_date of the last question asked with the tag<br/>
>  - name - name<br/>
>   popular is the default sort.<br/>
>  <br/>
>  It is possible to create moderately complex queries using sort, min, max, fromdate, and todate.

#### Input Parameters
* `inname` - _optional_
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = popular => number
sort = activity => date
sort = name => string

* `min` - _optional_ - sort = popular => number
sort = activity => date
sort = name => string

* `sort` - _optional_
    Possible values: popular, activity, name.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns the tags found on a site that fulfill required tag constraints on questions.<br/>
>  <br/>
> The inname parameter lets a consumer filter down to tags that contain a certain substring. For example, inname=own would return both "download" and "owner" amongst others.<br/>
>  <br/>
> This method returns a list of tags.<br/>
>  <br/>
> The sorts accepted by this method operate on the follow fields of the tag object:<br/>
>  - popular - count<br/>
>  - activity - the creation_date of the last question asked with the tag<br/>
>  - name - name<br/>
>   popular is the default sort.<br/>
>  <br/>
>  It is possible to create moderately complex queries using sort, min, max, fromdate, and todate.

#### Input Parameters
* `inname` - _optional_
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = popular => number
sort = activity => date
sort = name => string

* `min` - _optional_ - sort = popular => number
sort = activity => date
sort = name => string

* `sort` - _optional_
    Possible values: popular, activity, name.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns all tag synonyms found a site.<br/>
>  <br/>
> When searching for synonyms of specific tags, it is better to use /tags/{tags}/synonyms over this method.<br/>
>  <br/>
> The sorts accepted by this method operate on the follow fields of the tag_synonym object:<br/>
>  - creation - creation_date<br/>
>  - applied - applied_count<br/>
>  - activity - last_applied_date<br/>
>   creation is the default sort.<br/>
>  <br/>
>  It is possible to create moderately complex queries using sort, min, max, fromdate, and todate.<br/>
>  <br/>
> This method returns a list of tag_synonyms.

#### Input Parameters
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = creation => date
sort = applied => number
sort = activity => date

* `min` - _optional_ - sort = creation => date
sort = applied => number
sort = activity => date

* `sort` - _optional_
    Possible values: creation, applied, activity.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns the frequently asked questions for the given set of tags in {tags}.<br/>
>  <br/>
> For a question to be returned, it must have all the tags in {tags} and be considered "frequently asked". The exact algorithm for determining whether a question is considered a FAQ is subject to change at any time.<br/>
>  <br/>
> {tags} can contain up to 5 individual tags per request.<br/>
>  <br/>
> This method returns a list of questions.

#### Input Parameters
* `tags` - _required_ - String list (semicolon delimited).
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns tag objects representing the tags in {tags} found on the site.<br/>
>  <br/>
> This method diverges from the standard naming patterns to avoid to conflicting with existing methods, due to the free form nature of tag names.<br/>
>  <br/>
> This method returns a list of tags.<br/>
>  <br/>
> The sorts accepted by this method operate on the follow fields of the tag object:<br/>
>  - popular - count<br/>
>  - activity - the creation_date of the last question asked with the tag<br/>
>  - name - name<br/>
>   popular is the default sort.<br/>
>  <br/>
>  It is possible to create moderately complex queries using sort, min, max, fromdate, and todate.

#### Input Parameters
* `tags` - _required_ - String list (semicolon delimited).
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = popular => number
sort = activity => date
sort = name => string

* `min` - _optional_ - sort = popular => number
sort = activity => date
sort = name => string

* `sort` - _optional_
    Possible values: popular, activity, name.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns the tags that are most related to those in {tags}.<br/>
>  <br/>
> Including multiple tags in {tags} is equivalent to asking for "tags related to tag #1 and tag #2" not "tags related to tag #1 or tag #2".<br/>
>  <br/>
> count on tag objects returned is the number of question with that tag that also share all those in {tags}.<br/>
>  <br/>
> {tags} can contain up to 4 individual tags per request.<br/>
>  <br/>
> This method returns a list of tags.

#### Input Parameters
* `tags` - _required_ - String list (semicolon delimited).
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Gets all the synonyms that point to the tags identified in {tags}. If you're looking to discover all the tag synonyms on a site, use the /tags/synonyms methods instead of call this method on all tags.<br/>
>  <br/>
> {tags} can contain up to 20 individual tags per request.<br/>
>  <br/>
> The sorts accepted by this method operate on the follow fields of the tag_synonym object:<br/>
>  - creation - creation_date<br/>
>  - applied - applied_count<br/>
>  - activity - last_applied_date<br/>
>   creation is the default sort.<br/>
>  <br/>
>  It is possible to create moderately complex queries using sort, min, max, fromdate, and todate.<br/>
>  <br/>
> This method returns a list of tag synonyms.

#### Input Parameters
* `tags` - _required_ - String list (semicolon delimited).
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = creation => date
sort = applied => number
sort = activity => date

* `min` - _optional_ - sort = creation => date
sort = applied => number
sort = activity => date

* `sort` - _optional_
    Possible values: creation, applied, activity.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns the wikis that go with the given set of tags in {tags}.<br/>
>  <br/>
> Be aware that not all tags have wikis.<br/>
>  <br/>
> {tags} can contain up to 20 individual tags per request.<br/>
>  <br/>
> This method returns a list of tag wikis.

#### Input Parameters
* `tags` - _required_ - String list (semicolon delimited).
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns the top 30 answerers active in a single tag, of either all-time or the last 30 days.<br/>
>  <br/>
> This is a view onto the data presented on the tag info page on the sites.<br/>
>  <br/>
> This method returns a list of tag score objects.

#### Input Parameters
* `tag` - _required_
* `period` - _required_
    Possible values: all_time, month.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns the top 30 askers active in a single tag, of either all-time or the last 30 days.<br/>
>  <br/>
> This is a view onto the data presented on the tag info page on the sites.<br/>
>  <br/>
> This method returns a list of tag score objects.

#### Input Parameters
* `tag` - _required_
* `period` - _required_
    Possible values: all_time, month.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns all users on a site.<br/>
>  <br/>
> This method returns a list of users.<br/>
>  <br/>
> The sorts accepted by this method operate on the follow fields of the user object:<br/>
>  - reputation - reputation<br/>
>  - creation - creation_date<br/>
>  - name - display_name<br/>
>  - modified - last_modified_date<br/>
>   reputation is the default sort.<br/>
>  <br/>
>  It is possible to create moderately complex queries using sort, min, max, fromdate, and todate.<br/>
>  <br/>
> The inname parameter lets consumers filter the results down to just those users with a certain substring in their display name. For example, inname=kevin will return all users with both users named simply "Kevin" or those with Kevin as one of (or part of) their names; such as "Kevin Montrose".

#### Input Parameters
* `inname` - _optional_
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = reputation => number
sort = creation => date
sort = name => string
sort = modified => date

* `min` - _optional_ - sort = reputation => number
sort = creation => date
sort = name => string
sort = modified => date

* `sort` - _optional_
    Possible values: reputation, creation, name, modified.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Gets those users on a site who can exercise moderation powers.<br/>
>  <br/>
> Note, employees of Stack Exchange Inc. will be returned if they have been granted moderation powers on a site even if they have never been appointed or elected explicitly. This method checks abilities, not the manner in which they were obtained.<br/>
>  <br/>
> The sorts accepted by this method operate on the follow fields of the user object:<br/>
>  - reputation - reputation<br/>
>  - creation - creation_date<br/>
>  - name - display_name<br/>
>  - modified - last_modified_date<br/>
>   reputation is the default sort.<br/>
>  <br/>
>  It is possible to create moderately complex queries using sort, min, max, fromdate, and todate.<br/>
>  <br/>
> This method returns a list of users.

#### Input Parameters
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = reputation => number
sort = creation => date
sort = name => string
sort = modified => date

* `min` - _optional_ - sort = reputation => number
sort = creation => date
sort = name => string
sort = modified => date

* `sort` - _optional_
    Possible values: reputation, creation, name, modified.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns those users on a site who both have moderator powers, and were actually elected.<br/>
>  <br/>
> This method excludes Stack Exchange Inc. employees, unless they were actually elected moderators on a site (which can only have happened prior to their employment).<br/>
>  <br/>
> The sorts accepted by this method operate on the follow fields of the user object:<br/>
>  - reputation - reputation<br/>
>  - creation - creation_date<br/>
>  - name - display_name<br/>
>  - modified - last_modified_date<br/>
>   reputation is the default sort.<br/>
>  <br/>
>  It is possible to create moderately complex queries using sort, min, max, fromdate, and todate.<br/>
>  <br/>
> This method returns a list of users.

#### Input Parameters
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = reputation => number
sort = creation => date
sort = name => string
sort = modified => date

* `min` - _optional_ - sort = reputation => number
sort = creation => date
sort = name => string
sort = modified => date

* `sort` - _optional_
    Possible values: reputation, creation, name, modified.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Gets the users identified in ids in {ids}.<br/>
>  <br/>
> Typically this method will be called to fetch user profiles when you have obtained user ids from some other source, such as /questions.<br/>
>  <br/>
> {ids} can contain up to 100 semicolon delimited ids, to find ids programatically look for user_id on user or shallow_user objects.<br/>
>  <br/>
> The sorts accepted by this method operate on the follow fields of the user object:<br/>
>  - reputation - reputation<br/>
>  - creation - creation_date<br/>
>  - name - display_name<br/>
>  - modified - last_modified_date<br/>
>   reputation is the default sort.<br/>
>  <br/>
>  It is possible to create moderately complex queries using sort, min, max, fromdate, and todate.<br/>
>  <br/>
> This method returns a list of users.

#### Input Parameters
* `ids` - _required_ - Number list (semicolon delimited).
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = reputation => number
sort = creation => date
sort = name => string
sort = modified => date

* `min` - _optional_ - sort = reputation => number
sort = creation => date
sort = name => string
sort = modified => date

* `sort` - _optional_
    Possible values: reputation, creation, name, modified.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns the answers the users in {ids} have posted.<br/>
>  <br/>
> {ids} can contain up to 100 semicolon delimited ids, to find ids programatically look for user_id on user or shallow_user objects.<br/>
>  <br/>
> The sorts accepted by this method operate on the follow fields of the answer object:<br/>
>  - activity - last_activity_date<br/>
>  - creation - creation_date<br/>
>  - votes - score<br/>
>   activity is the default sort.<br/>
>  <br/>
>  It is possible to create moderately complex queries using sort, min, max, fromdate, and todate.<br/>
>  <br/>
> This method returns a list of answers.

#### Input Parameters
* `ids` - _required_ - Number list (semicolon delimited).
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number

* `min` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number

* `sort` - _optional_
    Possible values: activity, creation, votes.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns all of a user's associated accounts, given their account_ids in {ids}.<br/>
>  <br/>
> {ids} can contain up to 100 semicolon delimited ids, to find ids programatically look for account_id on user objects.<br/>
>  <br/>
> This method returns a list of network_users.

#### Input Parameters
* `ids` - _required_ - Number list (semicolon delimited).
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.


### Get the badges the users in {ids} have earned.<br/>
>  <br/>
> Badge sorts are a tad complicated. For the purposes of sorting (and min/max) tag_based is considered to be greater than named.<br/>
>  <br/>
> This means that you can get a list of all tag based badges a user has by passing min=tag_based, and conversely all the named badges by passing max=named, with sort=type.<br/>
>  <br/>
> For ranks, bronze is greater than silver which is greater than gold. Along with sort=rank, set max=gold for just gold badges, max=silver&min=silver for just silver, and min=bronze for just bronze.<br/>
>  <br/>
> rank is the default sort.<br/>
>  <br/>
> {ids} can contain up to 100 semicolon delimited ids, to find ids programatically look for user_id on user or shallow_user objects.<br/>
>  <br/>
> This method returns a list of badges.

#### Input Parameters
* `ids` - _required_ - Number list (semicolon delimited).
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = rank => string
sort = name => string
sort = type => string
sort = awarded => date

* `min` - _optional_ - sort = rank => string
sort = name => string
sort = type => string
sort = awarded => date

* `sort` - _optional_
    Possible values: rank, name, type, awarded.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Get the comments posted by users in {ids}.<br/>
>  <br/>
> {ids} can contain up to 100 semicolon delimited ids, to find ids programatically look for user_id on user or shallow_user objects.<br/>
>  <br/>
> The sorts accepted by this method operate on the follow fields of the comment object:<br/>
>  - creation - creation_date<br/>
>  - votes - score<br/>
>   creation is the default sort.<br/>
>  <br/>
>  It is possible to create moderately complex queries using sort, min, max, fromdate, and todate.<br/>
>  <br/>
> This method returns a list of comments.

#### Input Parameters
* `ids` - _required_ - Number list (semicolon delimited).
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = creation => date
sort = votes => number

* `min` - _optional_ - sort = creation => date
sort = votes => number

* `sort` - _optional_
    Possible values: creation, votes.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Get the comments that the users in {ids} have posted in reply to the single user identified in {toid}.<br/>
>  <br/>
> This method is useful for extracting conversations, especially over time or across multiple posts.<br/>
>  <br/>
> {ids} can contain up to 100 semicolon delimited ids, to find ids programatically look for user_id on user or shallow_user objects. {toid} can contain only 1 id, found in the same manner as those in {ids}.<br/>
>  <br/>
> The sorts accepted by this method operate on the follow fields of the comment object:<br/>
>  - creation - creation_date<br/>
>  - votes - score<br/>
>   creation is the default sort.<br/>
>  <br/>
>  It is possible to create moderately complex queries using sort, min, max, fromdate, and todate.<br/>
>  <br/>
> This method returns a list of comments.

#### Input Parameters
* `ids` - _required_ - Number list (semicolon delimited).
* `toid` - _required_
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = creation => date
sort = votes => number

* `min` - _optional_ - sort = creation => date
sort = votes => number

* `sort` - _optional_
    Possible values: creation, votes.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Get the questions that users in {ids} have favorited.<br/>
>  <br/>
> This method is effectively a view onto a user's favorites tab.<br/>
>  <br/>
> {ids} can contain up to 100 semicolon delimited ids, to find ids programatically look for user_id on user or shallow_user objects.<br/>
>  <br/>
> The sorts accepted by this method operate on the follow fields of the question object:<br/>
>  - activity - last_activity_date<br/>
>  - creation - creation_date<br/>
>  - votes - score<br/>
>  - added - when the user favorited the question<br/>
>   activity is the default sort.<br/>
>  <br/>
>  It is possible to create moderately complex queries using sort, min, max, fromdate, and todate.<br/>
>  <br/>
> This method returns a list of questions.

#### Input Parameters
* `ids` - _required_ - Number list (semicolon delimited).
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number
sort = added => date

* `min` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number
sort = added => date

* `sort` - _optional_
    Possible values: activity, creation, votes, added.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Gets all the comments that the users in {ids} were mentioned in.<br/>
>  <br/>
> Note, to count as a mention the comment must be considered to be "in reply to" a user. Most importantly, this means that a comment can only be in reply to a single user.<br/>
>  <br/>
> {ids} can contain up to 100 semicolon delimited ids, to find ids programatically look for user_id on user or shallow_user objects.<br/>
>  <br/>
> The sorts accepted by this method operate on the follow fields of the comment object:<br/>
>  - creation - creation_date<br/>
>  - votes - score<br/>
>   It is possible to create moderately complex queries using sort, min, max, fromdate, and todate.<br/>
>  <br/>
> This method returns a list of comments.

#### Input Parameters
* `ids` - _required_ - Number list (semicolon delimited).
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = creation => date
sort = votes => number

* `min` - _optional_ - sort = creation => date
sort = votes => number

* `sort` - _optional_
    Possible values: creation, votes.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns a record of merges that have occurred involving the passed account ids.<br/>
>  <br/>
> This method allows you to take now invalid account ids and find what account they've become, or take currently valid account ids and find which ids were equivalent in the past.<br/>
>  <br/>
> This is most useful when confirming that an account_id is in fact "new" to an application.<br/>
>  <br/>
> Account merges can happen for a wide range of reasons, applications should not make assumptions that merges have particular causes.<br/>
>  <br/>
> Note that accounts are managed at a network level, users on a site may be merged due to an account level merge but there is no guarantee that a merge has an effect on any particular site.<br/>
>  <br/>
> This method returns a list of account_merge.

#### Input Parameters
* `ids` - _required_ - Number list (semicolon delimited).
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.


### Gets the questions asked by the users in {ids}.<br/>
>  <br/>
> {ids} can contain up to 100 semicolon delimited ids, to find ids programatically look for user_id on user or shallow_user objects.<br/>
>  <br/>
> The sorts accepted by this method operate on the follow fields of the question object:<br/>
>  - activity - last_activity_date<br/>
>  - creation - creation_date<br/>
>  - votes - score<br/>
>   activity is the default sort.<br/>
>  <br/>
>  It is possible to create moderately complex queries using sort, min, max, fromdate, and todate.<br/>
>  <br/>
> This method returns a list of questions.

#### Input Parameters
* `ids` - _required_ - Number list (semicolon delimited).
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number

* `min` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number

* `sort` - _optional_
    Possible values: activity, creation, votes.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Gets the questions on which the users in {ids} have active bounties.<br/>
>  <br/>
> {ids} can contain up to 100 semicolon delimited ids, to find ids programatically look for user_id on user or shallow_user objects.<br/>
>  <br/>
> The sorts accepted by this method operate on the follow fields of the question object:<br/>
>  - activity - last_activity_date<br/>
>  - creation - creation_date<br/>
>  - votes - score<br/>
>   activity is the default sort.<br/>
>  <br/>
>  It is possible to create moderately complex queries using sort, min, max, fromdate, and todate.<br/>
>  <br/>
> This method returns a list of questions.

#### Input Parameters
* `ids` - _required_ - Number list (semicolon delimited).
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number

* `min` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number

* `sort` - _optional_
    Possible values: activity, creation, votes.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Gets the questions asked by the users in {ids} which have no answers.<br/>
>  <br/>
> Questions returns by this method actually have zero undeleted answers. It is completely disjoint /users/{ids}/questions/unanswered and /users/{ids}/questions/unaccepted, which only return questions with at least one answer, subject to other contraints.<br/>
>  <br/>
> {ids} can contain up to 100 semicolon delimited ids, to find ids programatically look for user_id on user or shallow_user objects.<br/>
>  <br/>
> The sorts accepted by this method operate on the follow fields of the question object:<br/>
>  - activity - last_activity_date<br/>
>  - creation - creation_date<br/>
>  - votes - score<br/>
>   activity is the default sort.<br/>
>  <br/>
>  It is possible to create moderately complex queries using sort, min, max, fromdate, and todate.<br/>
>  <br/>
> This method returns a list of questions.

#### Input Parameters
* `ids` - _required_ - Number list (semicolon delimited).
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number

* `min` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number

* `sort` - _optional_
    Possible values: activity, creation, votes.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Gets the questions asked by the users in {ids} which have at least one answer, but no accepted answer.<br/>
>  <br/>
> Questions returned by this method have answers, but the owner has not opted to accept any of them.<br/>
>  <br/>
> {ids} can contain up to 100 semicolon delimited ids, to find ids programatically look for user_id on user or shallow_user objects.<br/>
>  <br/>
> The sorts accepted by this method operate on the follow fields of the question object:<br/>
>  - activity - last_activity_date<br/>
>  - creation - creation_date<br/>
>  - votes - score<br/>
>   activity is the default sort.<br/>
>  <br/>
>  It is possible to create moderately complex queries using sort, min, max, fromdate, and todate.<br/>
>  <br/>
> This method returns a list of questions.

#### Input Parameters
* `ids` - _required_ - Number list (semicolon delimited).
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number

* `min` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number

* `sort` - _optional_
    Possible values: activity, creation, votes.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Gets the questions asked by the users in {ids} which the site consideres unanswered, while still having at least one answer posted.<br/>
>  <br/>
> These rules are subject to change, but currently any question without at least one upvoted or accepted answer is considered unanswered.<br/>
>  <br/>
> To get the set of questions that a user probably considers unanswered, the returned questions should be unioned with those returned by /users/{id}/questions/no-answers. These methods are distinct so that truly unanswered (that is, zero posted answers) questions can be easily separated from mearly poorly or inadequately answered ones.<br/>
>  <br/>
> {ids} can contain up to 100 semicolon delimited ids, to find ids programatically look for user_id on user or shallow_user objects.<br/>
>  <br/>
> The sorts accepted by this method operate on the follow fields of the question object:<br/>
>  - activity - last_activity_date<br/>
>  - creation - creation_date<br/>
>  - votes - score<br/>
>   activity is the default sort.<br/>
>  <br/>
>  It is possible to create moderately complex queries using sort, min, max, fromdate, and todate.<br/>
>  <br/>
> This method returns a list of questions.

#### Input Parameters
* `ids` - _required_ - Number list (semicolon delimited).
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number

* `min` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number

* `sort` - _optional_
    Possible values: activity, creation, votes.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Gets a subset of the reputation changes for users in {ids}.<br/>
>  <br/>
> Reputation changes are intentionally scrubbed of some data to make it difficult to correlate votes on particular posts with user reputation changes. That being said, this method returns enough data for reasonable display of reputation trends.<br/>
>  <br/>
> {ids} can contain up to 100 semicolon delimited ids, to find ids programatically look for user_id on user or shallow_user objects.<br/>
>  <br/>
> This method returns a list of reputation objects.

#### Input Parameters
* `ids` - _required_ - Number list (semicolon delimited).
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns users' public reputation history.<br/>
>  <br/>
> This method returns a list of reputation_history.

#### Input Parameters
* `ids` - _required_ - Number list (semicolon delimited).
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns the suggested edits a users in {ids} have submitted.<br/>
>  <br/>
> {ids} can contain up to 100 semicolon delimited ids, to find ids programatically look for user_id on user or shallow_user objects.<br/>
>  <br/>
> The sorts accepted by this method operate on the follow fields of the suggested_edit object:<br/>
>  - creation - creation_date<br/>
>  - approval - approval_date Does not return unapproved suggested_edits<br/>
>  - rejection - rejection_date Does not return unrejected suggested_edits<br/>
>   creation is the default sort.<br/>
>  <br/>
>  It is possible to create moderately complex queries using sort, min, max, fromdate, and todate.<br/>
>  <br/>
> This method returns a list of suggested-edits.

#### Input Parameters
* `ids` - _required_ - Number list (semicolon delimited).
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = creation => date
sort = approval => date
sort = rejection => date

* `min` - _optional_ - sort = creation => date
sort = approval => date
sort = rejection => date

* `sort` - _optional_
    Possible values: creation, approval, rejection.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns the tags the users identified in {ids} have been active in.<br/>
>  <br/>
> This route corresponds roughly to user's stats tab, but does not include tag scores. A subset of tag scores are available (on a single user basis) in /users/{id}/top-answer-tags and /users/{id}/top-question-tags.<br/>
>  <br/>
> {ids} can contain up to 100 semicolon delimited ids, to find ids programatically look for user_id on user or shallow_user objects.<br/>
>  <br/>
> The sorts accepted by this method operate on the follow fields of the tag object:<br/>
>  - popular - count<br/>
>  - activity - the creation_date of the last question asked with the tag<br/>
>  - name - name<br/>
>   popular is the default sort.<br/>
>  <br/>
>  It is possible to create moderately complex queries using sort, min, max, fromdate, and todate.<br/>
>  <br/>
> This method returns a list of tags.

#### Input Parameters
* `ids` - _required_ - Number list (semicolon delimited).
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = popular => number
sort = activity => date
sort = name => string

* `min` - _optional_ - sort = popular => number
sort = activity => date
sort = name => string

* `sort` - _optional_
    Possible values: popular, activity, name.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns a subset of the actions the users in {ids} have taken on the site.<br/>
>  <br/>
> This method returns users' posts, edits, and earned badges in the order they were accomplished. It is possible to filter to just a window of activity using the fromdate and todate parameters.<br/>
>  <br/>
> {ids} can contain up to 100 semicolon delimited ids, to find ids programatically look for user_id on user or shallow_user objects.<br/>
>  <br/>
> This method returns a list of user timeline objects.

#### Input Parameters
* `ids` - _required_ - Number list (semicolon delimited).
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns a user's inbox.<br/>
>  <br/>
> This method requires an access_token, with a scope containing "read_inbox".<br/>
>  <br/>
> This method is effectively an alias for /inbox. It is provided for consumers who make strong assumptions about operating within the context of a single site rather than the Stack Exchange network as a whole.<br/>
>  <br/>
> {id} can contain a single id, to find it programatically look for user_id on user or shallow_user objects.<br/>
>  <br/>
> This method returns a list of inbox items.

#### Input Parameters
* `id` - _required_
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns the unread items in a user's inbox.<br/>
>  <br/>
> This method requires an access_token, with a scope containing "read_inbox".<br/>
>  <br/>
> This method is effectively an alias for /inbox/unread. It is provided for consumers who make strong assumptions about operating within the context of a single site rather than the Stack Exchange network as a whole.<br/>
>  <br/>
> {id} can contain a single id, to find it programatically look for user_id on user or shallow_user objects.<br/>
>  <br/>
> This method returns a list of inbox items.

#### Input Parameters
* `id` - _required_
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.

* `since` - _optional_ - Unix date.

### Returns a user's notifications.<br/>
>  <br/>
> This method requires an access_token, with a scope containing "read_inbox".<br/>
>  <br/>
> This method returns a list of notifications.

#### Input Parameters
* `id` - _required_
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns a user's unread notifications.<br/>
>  <br/>
> This method requires an access_token, with a scope containing "read_inbox".<br/>
>  <br/>
> This method returns a list of notifications.

#### Input Parameters
* `id` - _required_
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns the privileges a user has.<br/>
>  <br/>
> Applications are encouraged to calculate privileges themselves, without repeated queries to this method. A simple check against the results returned by /privileges and user.user_type would be sufficient.<br/>
>  <br/>
> {id} can contain only a single, to find it programatically look for user_id on user or shallow_user objects.<br/>
>  <br/>
> This method returns a list of privileges.

#### Input Parameters
* `id` - _required_
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns a user's full reputation history, including private events.<br/>
>  <br/>
> This method requires an access_token, with a scope containing "private_info".<br/>
>  <br/>
> This method returns a list of reputation_history.

#### Input Parameters
* `id` - _required_
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns the top 30 answers a user has posted in response to questions with the given tags.<br/>
>  <br/>
> {id} can contain a single id, to find it programatically look for user_id on user or shallow_user objects. {tags} is limited to 5 tags, passing more will result in an error.<br/>
>  <br/>
> The sorts accepted by this method operate on the follow fields of the answer object:<br/>
>  - activity - last_activity_date<br/>
>  - creation - creation_date<br/>
>  - votes - score<br/>
>   activity is the default sort.<br/>
>  <br/>
>  It is possible to create moderately complex queries using sort, min, max, fromdate, and todate.<br/>
>  <br/>
> This method returns a list of answers.

#### Input Parameters
* `id` - _required_
* `tags` - _required_ - String list (semicolon delimited).
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number

* `min` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number

* `sort` - _optional_
    Possible values: activity, creation, votes.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns the top 30 questions a user has asked with the given tags.<br/>
>  <br/>
> {id} can contain a single id, to find it programatically look for user_id on user or shallow_user objects. {tags} is limited to 5 tags, passing more will result in an error.<br/>
>  <br/>
> The sorts accepted by this method operate on the follow fields of the question object:<br/>
>  - activity - last_activity_date<br/>
>  - creation - creation_date<br/>
>  - votes - score<br/>
>   activity is the default sort.<br/>
>  <br/>
>  It is possible to create moderately complex queries using sort, min, max, fromdate, and todate.<br/>
>  <br/>
> This method returns a list of questions.

#### Input Parameters
* `id` - _required_
* `tags` - _required_ - String list (semicolon delimited).
* `order` - _optional_
    Possible values: desc, asc.
* `max` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number

* `min` - _optional_ - sort = activity => date
sort = creation => date
sort = votes => number

* `sort` - _optional_
    Possible values: activity, creation, votes.
* `fromdate` - _optional_ - Unix date.
* `todate` - _optional_ - Unix date.
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns a single user's top tags by answer score.<br/>
>  <br/>
> This a subset of the data returned on a user's tags tab.<br/>
>  <br/>
> {id} can contain a single id, to find it programatically look for user_id on user or shallow_user objects.<br/>
>  <br/>
> This method returns a list of top_tag objects.

#### Input Parameters
* `id` - _required_
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns a single user's top tags by question score.<br/>
>  <br/>
> This a subset of the data returned on a user's tags tab.<br/>
>  <br/>
> {id} can contain a single id, to find it programatically look for user_id on user or shallow_user objects.<br/>
>  <br/>
> This method returns a list of top_tag objects.

#### Input Parameters
* `id` - _required_
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


### Returns the write permissions a user has via the api.<br/>
>  <br/>
> The Stack Exchange API gives users the ability to create, edit, and delete certain types. This method returns whether the passed user is capable of performing those actions at all, as well as how many times a day they can.<br/>
>  <br/>
> This method does not consider the user's current quota (ie. if they've already exhausted it for today) nor any additional restrictions on write access, such as editing deleted comments.<br/>
>  <br/>
> This method returns a list of write_permissions.

#### Input Parameters
* `id` - _required_
* `pagesize` - _optional_
* `page` - _optional_
* `filter` - _optional_ - #Discussion

The Stack Exchange API allows applications to exclude almost every field returned. For example, if an application did not care about a user's badge counts it could exclude user.badge_counts whenever it calls a method that returns users.

An application excludes fields by creating a filter (via /filter/create) and passing it to a method in the filter parameter.

Filters are immutable and non-expiring. An application can safely "bake in" any filters that are created, it is not necessary (or advisable) to create filters at runtime.

The motivation for filters are several fold. Filters allow applications to reduce API responses to just the fields they are concerned with, saving bandwidth. With the list of fields an application is actually concerned with, the API can avoid unneccessary queries thereby decreasing response time (and reducing load on our infrastructure). Finally, filters allow us to be more conservative in what the API returns by default without a proliferation of parameters (as was seen with body, answers, and comments in the 1.x API family).

#Safety

Filters also carry a notion of safety, which is defined as follows. Any string returned as a result of an API call with a safe filter will be inline-able into HTML without script-injection concerns. That is to say, no additional sanitizing (encoding, HTML tag stripping, etc.) will be necessary on returned strings. Applications that wish to handle sanitizing themselves should create an unsafe filter. All filters are safe by default, under the assumption that double-encoding bugs are more desirable than script injections.

Note that this does not mean that "safe" filter is mearly an "unsafe" one with all fields passed though UrlEncode(...). Many fields can and will contain HTML in all filter types (most notably, the *.body fields).

When using unsafe filters, the API returns the highest fidelity data it can reasonably access for the given request. This means that in cases where the "safe" data is the only accessible data it will be returned even in "unsafe" filters. Notably the *.body fields are unchanged, as they are stored in that form. Fields that are unchanged between safe and unsafe filters are denoted in their types documentation.

#Built In Filters

The following filters are built in:

default, each type documents which fields are returned under the default filter (for example, answers).
withbody, which is default plus the *.body fields
none, which is empty
total, which includes just .total

#Compatibility with V1.x

For ease of transition from earlier API versions, the filters _b, _ba, _bc, _bca, _a, _ac, and _c are also built in. These are unsafe, and exclude a combination of question and answer body, comments, and answers so as to mimic the body, answers, and comments parameters that have been removed in V2.0. New applications should not use these filters.

* `callback` - _optional_ - All API responses are JSON, we do support JSONP with the callback query parameter.

* `site` - _required_ - Each of these methods operates on a single site at a time, identified by the site parameter. This parameter can be the full domain name (ie. "stackoverflow.com"), or a short form identified by api_site_parameter on the site object.


## License

**flow**ground :- Telekom iPaaS / stackexchange-com-connector<br/>
Copyright © 2019, [Deutsche Telekom AG](https://www.telekom.de)<br/>
contact: flowground@telekom.de

All files of this connector are licensed under the Apache 2.0 License. For details
see the file LICENSE on the toplevel directory.
