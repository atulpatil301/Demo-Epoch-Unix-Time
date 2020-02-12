# Epoch-Unix-Time


## Task
Develop an independent CloudFormation template which takes State/Province as a parameter and exports the Unix time for the given State/Province in Europe in the stack.

Present your findings and challenges once assignment is done.

## Goal
To understand if the candidate can read documentation and implement them in real projects.

## Guidance
Make use of Python and AWS CloudFormation (YAML Syntax).
Unix time for London can be found by using the WorldTimeAPI timezone service. Below is an example of the API, which can be used to retrieve the Unix time for London.


## Example
$ curl -s http://worldtimeapi.org/api/timezone/Europe/London.txt
```
abbreviation: GMT
client_ip: 123.252.131.74
datetime: 2020-02-11T12:32:16.567278+00:00
day_of_week: 2
day_of_year: 42
dst: false
dst_from: 
dst_offset: 0
dst_until: 
raw_offset: 0
timezone: Europe/London
unixtime: 1581424336
utc_datetime: 2020-02-11T12:32:16.567278+00:00
utc_offset: +00:00
```


## Notes
The Unix time can be parsed from the API output for a given state/province.
There is no standard CloudFormation resource for the Unix time; the developer will need to make use of CloudFormation Custom Resources to achieve the goal.
