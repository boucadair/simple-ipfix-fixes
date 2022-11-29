---
title: "Simple Fixes to the IPFIX IANA Registry"
abbrev: "IPFIX IANA Fixes"
category: info

docname: draft-boucla-opsawg-ipfix-fixes-latest
submissiontype: IETF
number:
date:
consensus: true
v: 3
area: "Operations and Management"
workgroup: "Operations and Management Area Working Group"
keyword:
 - IPFIX
author:
 -
    fullname: Mohamed Boucadair
    organization: Orange
    email: mohamed.boucadair@orange.com

 -
    fullname: Benoit Claise
    organization: Huawei
    email: benoit.claise@huawei.com

normative:
     RFC7012: #ipfix
     IANA-IPFIX:
        title: IP Flow Information Export (IPFIX) Entities
        target: https://www.iana.org/assignments/ipfix/ipfix.xhtml
        date: 2022-11

informative:


--- abstract

This document describes simple fixes to the IANA IPFIX registry.


--- middle

# Introduction

This document lists a set of fixes to the IPFIX IANA registry {{IANA-IPFIX}}.


# Conventions and Definitions

{::boilerplate bcp14-tagged}


# Point to An Existing IANA Registry

IANA is requested to update the following entries by adding the indicated pointer to an IANA registry under "Additional Information" of {{IANA-IPFIX}}:

| IE                     | Additional Information |
| icmpTypeCodeIPv4       | https://www.iana.org/assignments/icmp-parameters/icmp-parameters.xhtml     |
| igmpType      | https://www.iana.org/assignments/igmp-type-numbers/igmp-type-numbers.xhtml#igmp-type-numbers-1     |
| icmpTypeCodeIPv6       | https://www.iana.org/assignments/icmpv6-parameters/icmpv6-parameters.xhtml    |
| icmpTypeIPv4       | https://www.iana.org/assignments/icmp-parameters/icmp-parameters.xhtml#icmp-parameters-types    |
| icmpCodeIPv4       | https://www.iana.org/assignments/icmp-parameters/icmp-parameters.xhtml#icmp-parameters-codes    |
| icmpTypeIPv6       | https://www.iana.org/assignments/icmpv6-parameters/icmpv6-parameters.xhtml#icmpv6-parameters-2  |
| icmpCodeIPv6       | https://www.iana.org/assignments/icmpv6-parameters/icmpv6-parameters.xhtml#icmpv6-parameters-3  |
| privateEnterpriseNumber       |https://www.iana.org/assignments/enterprise-numbers/enterprise-numbers    |
{: title="Cite an IANA Registry under Additional Information"}

# Consistent Citation of Registries

## natOriginatingAddressRealm

OLD:

| Description                     | Additional Information |
| Indicates whether the session was created because traffic originated in the private or public address realm. postNATSourceIPv4Address, postNATDestinationIPv4Address, postNAPTSourceTransportPort, and postNAPTDestinationTransportPort are qualified with the address realm in perspective. Values are listed in the natOriginatingAddressRealm registry. See https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-nat-originating-address-realm. | See RFC3022 for the definition of NAT. |
{: title="XXXXX"}

NEW:

| Description                     | Additional Information |
|  Indicates whether the session was created because traffic originated in the private or public address realm. postNATSourceIPv4Address, postNATDestinationIPv4Address, postNAPTSourceTransportPort, and postNAPTDestinationTransportPort are qualified with the address realm in perspective. Values are listed in the natOriginatingAddressRealm registry. | See https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-nat-originating-address-realm. See RFC3022 for the definition of NAT.     |
{: title="XXXXX"}



# Update the Description

These IEs cannot echo some values that can be included in a packet. This section can be moved to another document that will updated RFC7012.

## tcpOptions

OLD:

| Description                     | Additional Information |
| x       |xxx    |
{: title="XXXXX"}

NEW:

| Description                     | Additional Information |
| x       |xxx    |
{: title="XXXXX"}

## ipv4Options

OLD:

| Description                     | Additional Information |
| x       |xxx    |
{: title="XXXXX"}

NEW:

| Description                     | Additional Information |
| x       |xxx    |
{: title="XXXXX"}


## ipv6ExtensionHeaders

OLD:

| Description                     | Additional Information |
| x       | xxx |
{: title="XXXXX"}

NEW:

| Description                     | Additional Information |
| x       | xxx |
{: title="XXXXX"}


# Security Considerations

IPFIX security considerations are discussed in {{Section 8 of RFC7012}}.


# IANA Considerations

Requested IANA actions are described in the main document. These actions are not repeated here.


--- back

# Acknowledgments
{:numbered="false"}

TODO acknowledge.

