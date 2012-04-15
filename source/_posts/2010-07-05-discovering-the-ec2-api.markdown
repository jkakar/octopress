---
layout: post
title: "Discovering the EC2 API"
date: 2010-07-05 12:25
comments: false
categories: cloud
---

I've been using the EC2 API quite a lot lately, while working on the
[Landscape](https://landscape.canonical.com/) project.  The
[API documentation](http://docs.amazonwebservices.com/AWSEC2/latest/APIReference/)
is excellent, but I want to know how it behaves when things go wrong.
What kind of failure is produced when I forget to pass a parameter?
What happens when I pass a bogus parameter?  How does it behave when I
pass numbered parameters that aren't in sequence, like
`Name.7=foo&Name.42=bar`? How does Amazon's implementation differ from
[Eucalyptus](http://eucalyptus.com/) or [Nova](http://novacc.org/)?

I couldn't find the answers I wanted in the documentation so I wrote a
simple tool to invoke a method with an arbitrary set of parameters
against an EC2 API endpoint.  After sending the request, it prints the
HTTP status code and response to the screen.  It's called
`txaws-discover` and is part of the
[txAWS](https://launchpad.net/txaws) project.  For example, to run the
`DescribeRegions` method simply provide credentials, an endpoint, the
method name and whatever parameters you want to pass with it:

``` bash
txaws-discover --key NUJOZS2V6RWQUJ3G8JUT \
    --secret +Ki9Wk5Y4kudFh1EcnB3hthC9PtVU+CcfMJZ4DVl \
    --endpoint https://ec2.us-east-1.amazonaws.com \
    --action DescribeRegions \
    --RegionName.0 us-west-1
```

This command produces the following output:

``` xml
HTTP status code: 200


<DescribeRegionsResponse xmlns="http://ec2.amazonaws.com/doc/2008-12-01/">
    <requestId>1e9beacc-0044-4ad6-bd2c-c615351ae46d</requestId>
    <regionInfo>
        <item>
            <regionName>us-west-1</regionName>
            <regionEndpoint>ec2.us-west-1.amazonaws.com</regionEndpoint>
        </item>
    </regionInfo>
</DescribeRegionsResponse>
```

The credentials and API endpoint can be defined in environment
variables to make `txaws-discover` easier to use:

``` bash
export AWS_ACCESS_KEY_ID=NUJOZS2V6RWQUJ3G8JUT
export AWS_SECRET_ACCESS_KEY=+Ki9Wk5Y4kudFh1EcnB3hthC9PtVU+CcfMJZ4DVl
export AWS_ENDPOINT=https://ec2.us-east-1.amazonaws.com
```

With those defined, the command above can be shortened:

```
txaws-discover --action DescribeRegions --RegionName.0 us-west-1
```

It's in [lp:txaws](https://code.launchpad.net/~txaws-dev/txaws/trunk)
and has proven to be very helpful as a learning tool.
