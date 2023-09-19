---
title: "Simple Fixes to the IP Flow Information Export (IPFIX) IANA Registry"
abbrev: "IPFIX IANA Fixes"
category: std

docname: draft-ietf-opsawg-ipfix-fixes-latest
submissiontype: IETF
number:
date:
consensus: true
v: 3
area: "Operations and Management"
workgroup: "OPSAWG"
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
     IANA-IPFIX:
        title: IP Flow Information Export (IPFIX) Entities
        target: https://www.iana.org/assignments/ipfix/ipfix.xhtml
     IANA-EH:
        title: Internet Protocol Version 6 (IPv6) Parameters, IPv6 Extension Header Types
        target: https://www.iana.org/assignments/ipv6-parameters/ipv6-parameters.xhtml#ipv6-parameters-1
     IANA-TCP:
        title: Transmission Control Protocol (TCP) Parameters, TCP Option Kind Numbers
        target: https://www.iana.org/assignments/tcp-parameters/tcp-parameters.xhtml#tcp-parameters-1
     IANA-Protocols:
        title: Protocol Numbers
        target: https://www.iana.org/assignments/protocol-numbers/protocol-numbers.xhtml
informative:


--- abstract

This document provides simple fixes to the IANA IP Flow Information Export (IPFIX) registry. Specifically, this document provides updates to fix a shortcoming in the description of some Information Elements (IE), updates to ensure a consistent structure when calling an existing IANA registry, and updates to fix broken pointers, orphan section references, etc. The updates are also meant to bringing some consistency among the entries of the registry.


--- middle

# Introduction

As the OPSAWG is currently considering {{?I-D.ietf-opsawg-rfc7125-update}} which updates {{?RFC7125}}, the WG realized that some other parts of the IANA IP Flow Information Export (IPFIX) registry {{IANA-IPFIX}} were not up-to-date. Indeed, since its initial creation in 2007, some IPFIX Information Elements (IEs) are not adequately specified any longer (while they were at some point in time in the past). This document intends to update the IANA registry and bringing some consistency among the entries of the registry.

As discussed with IANA, the "Additional Information" entry in {{IANA-IPFIX}} should contain a link to an existing registry, when applicable, as opposed to having:

- A link to an exiting registry in the "Description" entry.
- The registry detailed values repeated in the "Description" entry. This practice has the drawback that the description must be updated each time the registry is updated.

Therefore, this document lists a set of simple fixes to the IPFIX IANA registry {{IANA-IPFIX}}. These fixes are classified as follows:

- Updates that fix a shortcoming in the description of an IE ({{desc}}).
- Updates that require adding a pointer to an existing IANA registry ({{to-iana}}).
- Updates that are meant to ensure a consistent structure when calling an existing IANA registry ({{consistent}}).
- Miscellaneous updates that fix broken pointers, orphan section references, etc. ({{misc}}).

These updates are also meant to facilitate the automatic extraction of the values maintained in IANA registries (e.g., with a cron job), required by Collectors to be able to support new IPFIX IEs and, more importantly, adequately interpret new values in registries specified by those IPFIX IEs.

Note that, as per {{Section 5 of !RFC7012}}, {{IANA-IPFIX}} is the normative reference for the IPFIX IEs that were defined in {{?RFC5102}}. Therefore, the updates in this document do not update any part of {{!RFC7011}}.

# Conventions and Definitions

{::boilerplate bcp14-tagged}

This document uses the IPFIX-specific terminology (Information Element, Template,
   Collector,  Data Record, Flow Record, Exporting Process,
   Collecting Process, etc.) defined in
   Section 2 of {{!RFC7011}}. As in {{!RFC7011}}, these IPFIX-specific terms
   have the first letter of a word capitalized.

# Why An RFC is Needed for These Updates?

Many of the edits in this document may be handled by the IPFIX Experts (informally called the IE-DOCTORS {{!RFC7013}}). However, and given that many of the impacted IEs were created via the IETF stream, the following from {{Section 5.1 of !RFC7013}} should be followed:

   > This process should not in any way be construed as allowing the IE-DOCTORS to overrule IETF consensus.  Specifically, Information Elements in the IANA IE registry that were added with IETF consensus require IETF consensus for revision or deprecation.

# Update the Description {#desc}

## ipv6ExtensionHeaders Information Element

### Issues

The current specification of ipv6ExtensionHeaders Information Element should be updated to:

1. Reflect missing IPv6 EHs, specifically 139, 140, 253, and 254.
2. Specify how to automatically update the registry when a new value is assigned in {{IANA-EH}}.
3. As per {{IANA-Protocols}}, 108 does not correspond to an EH.
4. Specify the procedure to follow when all bits are exhausted.

The following section proposes a fix for the first three issues. {{!I-D.ietf-opsawg-ipfix-tcpo-v6eh}} specifies a new option to fix the last issue.

### Updates to the ipv6ExtensionHeaders Description

* OLD:

~~~
 Description:
    IPv6 extension headers observed in packets of this Flow.  The
    information is encoded in a set of bit fields.  For each IPv6
    option header, there is a bit in this set.  The bit is set to 1 if
    any observed packet of this Flow contains the corresponding IPv6
    extension header.  Otherwise, if no observed packet of this Flow
    contained the respective IPv6 extension header, the value of the
    corresponding bit is 0.

             0     1     2     3     4     5     6     7
         +-----+-----+-----+-----+-----+-----+-----+-----+
         | DST | HOP | Res | UNK |FRA0 | RH  |FRA1 | Res |  ...
         +-----+-----+-----+-----+-----+-----+-----+-----+

             8     9    10    11    12    13    14    15
         +-----+-----+-----+-----+-----+-----+-----+-----+
     ... |           Reserved    | MOB | ESP | AH  | PAY | ...
         +-----+-----+-----+-----+-----+-----+-----+-----+

            16    17    18    19    20    21    22    23
         +-----+-----+-----+-----+-----+-----+-----+-----+
     ... |                  Reserved                     | ...
         +-----+-----+-----+-----+-----+-----+-----+-----+

            24    25    26    27    28    29    30    31
         +-----+-----+-----+-----+-----+-----+-----+-----+
     ... |                  Reserved                     |
         +-----+-----+-----+-----+-----+-----+-----+-----+

     Bit    IPv6 Option   Description

     0, DST      60       Destination option header
     1, HOP       0       Hop-by-hop option header
     2, Res               Reserved
     3, UNK               Unknown Layer 4 header
                          (compressed, encrypted, not supported)
     4, FRA0     44       Fragment header - first fragment
     5, RH       43       Routing header
     6, FRA1     44       Fragmentation header - not first fragment
     7, Res               Reserved
     8 to 11              Reserved
     12, MOB     135      IPv6 mobility [RFC3775]
     13, ESP      50      Encrypted security payload
     14, AH       51      Authentication Header
     15, PAY     108      Payload compression header
     16 to 31             Reserved

 Abstract Data Type: unsigned32

 Data Type Semantics: flags

 ElementId: 64

 Status: current

 Reference: [RFC5102]

 Additional Information:
    See [RFC8200] for the general definition of IPv6 extension headers
    and for the specification of the hop-by-hop options header, the
    routing header, the fragment header, and the destination options
    header. See [RFC4302] for the specification of the authentication
    header. See [RFC4303] for the specification of the encapsulating
    security payload. The diagram provided in [RFC5102] is incorrect.
    The diagram in this registry is taken from Errata 1738.
    See [RFC Errata 1738].
~~~

* NEW:

Description:
: IPv6 extension headers observed in packets of this Flow. The
    information is encoded in a set of bit fields.  For each IPv6
    option header, there is a bit in this set.  The bit is set to 1 if
    any observed packet of this Flow contains the corresponding IPv6
    extension header.  Otherwise, if no observed packet of this Flow
    contained the respective IPv6 extension header, the value of the
    corresponding bit is 0. The IPv6 EH associated with each bit
    is provided in  [NEW_IPFIX_IPv6EH_SUBREGISTRY]. This IE is used
    only when the observed extension headers are in the 0-31
    range.
: If the observed EHs exceeds that range,
    ipv6ExtensionHeadersFull Information Element MUST be used
    {{!I-D.ietf-opsawg-ipfix-tcpo-v6eh}}.

Abstract Data Type:
: unsigned32

Data Type Semantics:
: flags

ElementId:
: 64

Status:
: current

Reference:
: [RFC5102]This-Document

Additional Information:
: See the assigned bits to each IPv6 extension header in [NEW_IPFIX_IPv6EH_SUBREGISTRY].
: See [RFC8200] for the general definition of IPv6 extension headers and [IANA-EH] for assigned extension headers.

## tcpOptions

### Issues

Only options having a kind =< 63 can be included in a tcpOptions IE. An update is thus required to specify how any observed TCP option in a packet can be exported using IPFIX. Also, there is no way to report the observed Experimental Identifiers (ExIDs) that are carried in shared TCP options (kind=253 or 254) {{!RFC6994}}.

The following section updates the description of the tcpOptions IE to explicitly indicate the applicable kind range and to point to the new IEs defined in {{!I-D.ietf-opsawg-ipfix-tcpo-v6eh}}.

### Update the Description of the tcpOptions IE

This document requests IANA to update the description of the tcpOptions IE in the IANA IPFIX registry {{IANA-IPFIX}} as follows:

* OLD Description:
: TCP options in packets of this Flow.  The information is encoded
      in a set of bit fields.  For each TCP option, there is a bit in
      this set.  The bit is set to 1 if any observed packet of this Flow
      contains the corresponding TCP option.  Otherwise, if no observed
      packet of this Flow contained the respective TCP option, the value
      of the corresponding bit is 0.
      Options are mapped to bits according to their option numbers.
      Option number X is mapped to bit X.  TCP option numbers are
      maintained by IANA.

~~~~
            0     1     2     3     4     5     6     7
        +-----+-----+-----+-----+-----+-----+-----+-----+
        |   7 |   6 |   5 |   4 |   3 |   2 |   1 |   0 |  ...
        +-----+-----+-----+-----+-----+-----+-----+-----+

            8     9    10    11    12    13    14    15
        +-----+-----+-----+-----+-----+-----+-----+-----+
    ... |  15 |  14 |  13 |  12 |  11 |  10 |   9 |   8 |...
        +-----+-----+-----+-----+-----+-----+-----+-----+

           16    17    18    19    20    21    22    23
        +-----+-----+-----+-----+-----+-----+-----+-----+
    ... |  23 |  22 |  21 |  20 |  19 |  18 |  17 |  16 |...
        +-----+-----+-----+-----+-----+-----+-----+-----+

                              . . .

           56    57    58    59    60    61    62    63
        +-----+-----+-----+-----+-----+-----+-----+-----+
    ... |  63 |  62 |  61 |  60 |  59 |  58 |  57 |  56 |
        +-----+-----+-----+-----+-----+-----+-----+-----+
~~~~

* NEW Description:
: TCP options in packets of this Flow.  The information is encoded
      in a set of bit fields.  For each TCP option, there is a bit in
      this set.  The bit is set to 1 if any observed packet of this Flow
      contains the corresponding TCP option.  Otherwise, if no observed
      packet of this Flow contained the respective TCP option, the value
      of the corresponding bit is 0.
      Options are mapped to bits according to their option numbers.
      Option number X is mapped to bit X.  TCP option numbers are
      maintained by IANA. This information element is used only
      when the observed kinds are within the 0-63 range. If not, the tcpOptionsFull IE {{!I-D.ietf-opsawg-ipfix-tcpo-v6eh}} MUST be used.

~~~
            0     1     2     3     4     5     6     7
        +-----+-----+-----+-----+-----+-----+-----+-----+
        |   7 |   6 |   5 |   4 |   3 |   2 |   1 |   0 |  ...
        +-----+-----+-----+-----+-----+-----+-----+-----+

            8     9    10    11    12    13    14    15
        +-----+-----+-----+-----+-----+-----+-----+-----+
    ... |  15 |  14 |  13 |  12 |  11 |  10 |   9 |   8 |...
        +-----+-----+-----+-----+-----+-----+-----+-----+

           16    17    18    19    20    21    22    23
        +-----+-----+-----+-----+-----+-----+-----+-----+
    ... |  23 |  22 |  21 |  20 |  19 |  18 |  17 |  16 |...
        +-----+-----+-----+-----+-----+-----+-----+-----+

                              . . .

           56    57    58    59    60    61    62    63
        +-----+-----+-----+-----+-----+-----+-----+-----+
    ... |  63 |  62 |  61 |  60 |  59 |  58 |  57 |  56 |
        +-----+-----+-----+-----+-----+-----+-----+-----+
~~~

## forwardingStatus

The current forwardingStatus entry in {{IANA-IPFIX}} deviates from what is provided in {{!RFC7270}}. In particular, the registered Abstract Data Type is unsigned8, while it must be unsigned32. The following update fixes that issue. The description is also updated to clarify the use of the reduced-size encoding as per {{Section 6.2 of !RFC7011}}.

* OLD:

~~~
   - Description:  This Information Element describes the forwarding
                   status of the flow and any attached reasons.

                   The layout of the encoding is as follows:

                   MSB  -  0   1   2   3   4   5   6   7  -  LSB
                         +---+---+---+---+---+---+---+---+
                         | Status|  Reason code or flags |
                         +---+---+---+---+---+---+---+---+

                   See the Forwarding Status sub-registries at
                   https://www.iana.org/assignments/ipfix/ipfix.xhtml#forwarding-status.

                   Examples:

                   value : 0x40 = 64
                   binary: 01000000
                   decode: 01        -> Forward
                             000000  -> No further information

                   value : 0x89 = 137
                   binary: 10001001
                   decode: 10        -> Drop
                             001001  -> Bad TTL

   - Additional Information: See "NetFlow Version 9 Flow-Record Format"
             [CCO-NF9FMT].

   - Abstract Data Type: unsigned8
~~~

* NEW:

~~~
   - Description:  This Information Element describes the forwarding
                   status of the flow and any attached reasons.
                   IPFIX reduced-size encoding is used as required.

                   A structure is currently associated with the first
                   byte. Future versions may be defined to associate
                   meanings with the remaining bits.

                   The current version of the Information Element
                   should be exported as unsigned8.

                   The layout of the encoding is as follows:

                   MSB  -  0   1   2   3   4   5   6   7  -  LSB
                         +---+---+---+---+---+---+---+---+
                         | Status|  Reason code or flags |
                         +---+---+---+---+---+---+---+---+

                   Examples:

                   value : 0x40 = 64
                   binary: 01000000
                   decode: 01        -> Forward
                             000000  -> No further information

                   value : 0x89 = 137
                   binary: 10001001
                   decode: 10        -> Drop
                             001001  -> Bad TTL

   - Additional Information: See the Forwarding Status sub-registries
       at https://www.iana.org/assignments/ipfix/ipfix.xhtml#forwarding-status.

   - Abstract Data Type: unsigned32
~~~


# Point to An Existing IANA Registry {#to-iana}

This document requests IANA to update the following entries by adding the indicated "Additional Information" to the {{IANA-IPFIX}} registry:

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

# Consistent Citation of IANA Registries {#consistent}

This document requests IANA to update {{IANA-IPFIX}} for each of the IE entries listed in the following subsections.

## mplsTopLabelType

* OLD:
    - Description:
    : This field identifies the control protocol that allocated the top-of-stack label. Values for this field are listed in the MPLS label type registry.
    : See https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-mpls-label-type.

    - Additional Information:
    : See {{?RFC3031}} for the MPLS label structure.
    : See the list of MPLS label types assigned by IANA at [https://www.iana.org/assignments/mpls-label-values].

* NEW:
    - Description:
    : This field identifies the control protocol that allocated the top-of-stack label. Values for this field are listed in the MPLS label type registry.

    - Additional Information:
    : See the list of MPLS label types assigned by IANA at [https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-mpls-label-type].
    : See {{?RFC3031}} for the MPLS label structure.

## classificationEngineId

* OLD:
    - Description:
    : A unique identifier for the engine that determined the Selector ID. Thus, the Classification Engine ID defines the context for the Selector ID. The Classification Engine can be considered a specific registry for application assignments.
    : Values for this field are listed in the Classification Engine IDs registry. See https://www.iana.org/assignments/ipfix/ipfix.xhtml#classification-engine-ids.

   - Additional Information:

* NEW:
    - Description:
    : A unique identifier for the engine that determined the Selector ID. Thus, the Classification Engine ID defines the context for the Selector ID. The Classification Engine can be considered a specific registry for application assignments.
    : Values for this field are listed in the Classification Engine IDs registry.

    - Additional Information:
    : See https://www.iana.org/assignments/ipfix/ipfix.xhtml#classification-engine-ids.

## flowEndReason

* OLD:
    - Description:
    : The reason for Flow termination. Values are listed in the flowEndReason registry. See https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-flow-end-reason.

   - Additional Information:

* NEW:
    - Description:
    : The reason for Flow termination. Values are listed in the flowEndReason registry.

    - Additional Information:
    : See the Classification Engine IDs registry available at [https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-flow-end-reason].

## natOriginatingAddressRealm

* OLD:
    - Description:
    : Indicates whether the session was created because traffic originated in the private or public address realm. postNATSourceIPv4Address, postNATDestinationIPv4Address, postNAPTSourceTransportPort, and postNAPTDestinationTransportPort are qualified with the address realm in perspective.
    : Values are listed in the natOriginatingAddressRealm registry. See https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-nat-originating-address-realm.

   - Additional Information:
   : See {{?RFC3022}} for the definition of NAT.

* NEW:
    - Description:
    : Indicates whether the session was created because traffic originated in the private or public address realm. postNATSourceIPv4Address, postNATDestinationIPv4Address, postNAPTSourceTransportPort, and postNAPTDestinationTransportPort are qualified with the address realm in perspective.
    : Values are listed in the natOriginatingAddressRealm registry.

    - Additional Information:
    : See the assigned NAT originating address realm at [https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-nat-originating-address-realm]. See {{?RFC3022}} for the definition of NAT.

## natEvent

* OLD:
   - Description:
   : This Information Element identifies a NAT event. This IE identifies the type of a NAT event. Examples of NAT events include, but are not limited to, NAT translation create, NAT translation delete, Threshold Reached, or Threshold Exceeded, etc. Values for this Information Element are listed in the "NAT Event Type" registry, see https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-nat-event-type.

   - Additional Information:
   : See {{?RFC3022}} for the definition of NAT.
   : See {{?RFC3234}} for the definition of middleboxes.
   : See {{?RFC8158}} for the definitions of values 4-16.

* NEW:
   - Description:
   : This Information Element identifies a NAT event. This IE identifies the type of a NAT event. Examples of NAT events include, but are not limited to, NAT translation create, NAT translation delete, Threshold Reached, or Threshold Exceeded, etc. Values for this Information Element are listed in the "NAT Event Type" registry.

   - Additional Information:
   : See the assigned NAT Event Types at [https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-nat-event-type].
   : See {{?RFC3022}} for the definition of NAT.
   : See {{?RFC3234}} for the definition of middleboxes.
   : See {{?RFC8158}} for the definitions of values 4-16.

## firewallEvent

* OLD:
   - Description:
   : Indicates a firewall event. Allowed values are listed in the firewallEvent registry.
   : See https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-firewall-event.

   - Additional Information:

* NEW:
   - Description:
   : Indicates a firewall event. Allowed values are listed in the firewallEvent registry.

   - Additional Information:
   : See the assigned firewall events at [https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-firewall-event].

## biflowDirection

* OLD:
   - Description:
   :  A description of the direction assignment method used to assign the Biflow Source and Destination. This Information Element MAY be present in a Flow Data Record, or applied to all flows exported from an Exporting Process or Observation Domain using IPFIX Options. If this Information Element is not present in a Flow Record or associated with a Biflow via scope, it is assumed that the configuration of the direction assignment method is done out-of-band. Note that when using IPFIX Options to apply this Information Element to all flows within an Observation Domain or from an Exporting Process, the Option SHOULD be sent reliably. If reliable transport is not available (i.e., when using UDP), this Information Element SHOULD appear in each Flow Record. Values are listed in the biflowDirection registry. See [https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-biflow-direction].

   - Additional Information:

* NEW:
   - Description:
   : A description of the direction assignment method used to assign the Biflow Source and Destination. This Information Element MAY be present in a Flow Data Record, or applied to all flows exported from an Exporting Process or Observation Domain using IPFIX Options. If this Information Element is not present in a Flow Record or associated with a Biflow via scope, it is assumed that the configuration of the direction assignment method is done out-of-band. Note that when using IPFIX Options to apply this Information Element to all flows within an Observation Domain or from an Exporting Process, the Option SHOULD be sent reliably. If reliable transport is not available (i.e., when using UDP), this Information Element SHOULD appear in each Flow Record. Values are listed in the biflowDirection registry.

   - Additional Information:
   : See the assigned biflow direction values at [https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-biflow-direction].


## observationPointType

* OLD:
   - Description:
   : Type of observation point. Values are listed in the observationPointType registry. See https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-observation-point-type.

   - Additional Information:

* NEW:
   - Description:
   : Type of observation point. Values are listed in the observationPointType registry.

   - Additional Information:
   : See the assigned observation point type at [https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-observation-point-type].

## anonymizationTechnique

* OLD:
   - Description:
   : A description of the anonymization technique applied to a referenced Information Element within a referenced Template. Each technique may be applicable only to certain Information Elements and recommended only for certain Information Elements. Values are listed in the anonymizationTechnique registry. See https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-anonymization-technique.

   - Additional Information:

* NEW:
   - Description:
   : A description of the anonymization technique applied to a referenced Information Element within a referenced Template. Each technique may be applicable only to certain Information Elements and recommended only for certain Information Elements. Values are listed in the anonymizationTechnique registry.

   - Additional Information:
   : See the assigned anonymization techniques at [https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-anonymization-technique].

## natType

* OLD:
   - Description:
   : Values are listed in the natType registry.
   : See https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-nat-type.

   - Additional Information:
   : See {{?RFC3022}} for the definition of NAT.
   : See {{?RFC1631}} for the definition of NAT44.
   : See {{?RFC6144}} for the definition of NAT64.
   : See {{?RFC6146}} for the definition of NAT46.
   : See {{?RFC6296}} for the definition of NAT66.
   : See {{?RFC0791}} for the definition of IPv4.
   : See {{?RFC8200}} for the definition of IPv6.

* NEW:
   - Description:
   : Values are listed in the natType registry.

   - Additional Information:
   : See the assigned NAT types at [https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-nat-type].
   : See {{?RFC3022}} for the definition of NAT.
   : See {{?RFC1631}} for the definition of NAT44.
   : See {{?RFC6144}} for the definition of NAT46.
   : See {{?RFC6146}} for the definition of NAT64.
   : See {{?RFC6296}} for the definition of NPTv6.
   : See {{?RFC0791}} for the definition of IPv4.
   : See {{?RFC8200}} for the definition of IPv6.


> Note: This change also corrects errors in the pointers provided NAT46/NAT64.

## selectorAlgorithm

* OLD:
   - Description:
   : This Information Element identifies the packet selection methods (e.g., Filtering, Sampling) that are applied by the Selection Process. Most of these methods have parameters. Further Information Elements are needed to fully specify packet selection with these methods and all their parameters. The methods listed below are defined in {{?RFC5475}}. For their parameters, Information Elements are defined in the information model document. The names of these Information Elements are listed for each method identifier. Further method identifiers may be added to the list below. It might be necessary to define new Information Elements to specify their parameters.
   : The following packet selection methods identifiers are defined here: https://www.iana.org/assignments/psamp-parameters.
   : There is a broad variety of possible parameters that could be used for Property match Filtering (5) but currently there are no agreed parameters specified.

   - Additional Information:

* NEW:
   - Description:
   : This Information Element identifies the packet selection methods (e.g., Filtering, Sampling) that are applied by the Selection Process. Most of these methods have parameters. Further Information Elements are needed to fully specify packet selection with these methods and all their parameters. For the methods parameters, Information Elements are defined in the information model document. The names of these Information Elements are listed for each method identifier. Further method identifiers may be added to the list. It might be necessary to define new Information Elements to specify their parameters.
   : There is a broad variety of possible parameters that could be used for Property match Filtering (5) but currently there are no agreed parameters specified.

   - Additional Information:
   : See the assigned PSAMP parameters at [https://www.iana.org/assignments/psamp-parameters].

## informationElementDataType

* OLD:
   - Description:
   : A description of the abstract data type of an IPFIX information element.These are taken from the abstract data types defined in section 3.1 of the IPFIX Information Model {{?RFC5102}}; see that section for more information on the types described in the [informationElementDataType] subregistry. These types are registered in the IANA IPFIX Information Element Data Type subregistry. This subregistry is intended to assign numbers for type names, not to provide a mechanism for adding data types to the IPFIX Protocol, and as such requires a Standards Action {{?RFC8126}} to modify.

   - Additional Information:

* NEW:
   - Description:
   : A description of the abstract data type of an IPFIX information element.These are taken from the abstract data types defined in Section 3.1 of the IPFIX Information Model {{?RFC5102}}; see that section for more information on the types described in the [informationElementDataType] subregistry. These types are registered in the IANA IPFIX Information Element Data Type subregistry.
   : The [informationElementDataType] subregistry is intended to assign numbers for type names, not to provide a mechanism for adding data types to the IPFIX Protocol, and as such requires a Standards Action {{?RFC8126}} to modify.

   - Additional Information:
   : See the assigned emelement data types at [https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-information-element-data-types].

## informationElementSemantics

* OLD:
   - Description:
   : A description of the semantics of an IPFIX Information Element. These are taken from the data type semantics defined in section 3.2 of the IPFIX Information Model {{?RFC5102}}; see that section for more information on the types defined in the [IPFIX Information Element Semantics] subregistry. This field may take the values in the semantics registry; the special value 0x00 (default) is used to note that no semantics apply to the field; it cannot be manipulated by a Collecting Process or File Reader that does not understand it a priori. These semantics are registered in the IANA IPFIX Information Element Semantics subregistry. This subregistry is intended to assign numbers for semantics names, not to provide a mechanism for adding semantics to the IPFIX Protocol, and as such requires a Standards Action {{?RFC8126}} to modify.

   - Additional Information:

* NEW:
   - Description:
   : A description of the semantics of an IPFIX Information Element. These are taken from the data type semantics defined in Section 3.2 of the IPFIX Information Model {{?RFC5102}}; see that section for more information on the types defined in the [IPFIX Information Element Semantics] subregistry. This field may take the values in the [IPFIX Information Element Semantics] subregistry; the special value 0x00 (default) is used to note that no semantics apply to the field; it cannot be manipulated by a Collecting Process or File Reader that does not understand it a priori.
   : The [IPFIX Information Element Semantics] subregistry is intended to assign numbers for semantics names, not to provide a mechanism for adding semantics to the IPFIX Protocol, and as such requires a Standards Action {{?RFC8126}} to modify.

   - Additional Information:
   : See the assigned semantics of an IPFIX Information Element at [https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-information-element-semantic].

## informationElementUnits

* OLD:
   - Description:
   : A description of the units of an IPFIX Information Element. These correspond to the units implicitly defined in the Information Element definitions in section 5 of the IPFIX Information Model {{?RFC5102}}; see that section for more information on the types described in the informationElementsUnits subregistry. This field may take the values in Table 3 below; the special value 0x00 (none) is used to note that the field is unitless. These types are registered in the [IANA IPFIX Information Element Units] subregistry.

   - Additional Information:

* NEW:
   - Description:
   : A description of the units of an IPFIX Information Element. These correspond to the units implicitly defined in the Information Element definitions in Section 5 of the IPFIX Information Model {{?RFC5102}}; see that section for more information on the types described in the informationElementsUnits subregistry. These types can take the values in the [IANA IPFIX Information Element Units] subregistry. The special value 0x00 (none) is used to note that the field is unitless.

   - Additional Information: See the assigned units of an IPFIX Information Element at [IANA IPFIX Information Element Units].


## portRangeStart

* OLD:
   - Description:
   : The port number identifying the start of a range of ports. A value of zero indicates that the range start is not specified, ie the range is defined in some other way.
   : Additional information on defined TCP port numbers can be found at https://www.iana.org/assignments/service-names-port-numbers.

   - Additional Information:

* NEW:
   - Description:
   : The port number identifying the start of a range of ports. A value of zero indicates that the range start is not specified, i.e., the range is defined in some other way.

   - Additional Information:
   : Additional information on defined TCP port numbers can be found at https://www.iana.org/assignments/service-names-port-numbers.

## portRangeEnd

* OLD:
   - Description:
   : The port number identifying the end of a range of ports. A value of zero indicates that the range end is not specified, ie the range is defined in some other way. Additional information on defined TCP port numbers can be found at https://www.iana.org/assignments/service-names-port-numbers.

   - Additional Information:

* NEW:
   - Description:
   : The port number identifying the end of a range of ports. A value of zero indicates that the range end is not specified, i.e., the range is defined in some other way.

   - Additional Information:
   : Additional information on defined TCP port numbers can be found at https://www.iana.org/assignments/service-names-port-numbers.

## ingressInterfaceType

* OLD:
   - Description:
   : The type of interface where packets of this Flow are being received. The value matches the value of managed object 'ifType' as defined in https://www.iana.org/assignments/ianaiftype-mib.

   - Additional Information:
   : https://www.iana.org/assignments/ianaiftype-mib

* NEW:
   - Description:
   : The type of interface where packets of this Flow are being received. The value matches the value of managed object 'ifType'.

   - Additional Information:
   : See the assigned ingress interface types at [https://www.iana.org/assignments/ianaiftype-mib].

## egressInterfaceType

* OLD:
   - Description:
   : The type of interface where packets of this Flow are being sent. The value matches the value of managed object 'ifType' as defined in https://www.iana.org/assignments/ianaiftype-mib.

   - Additional Information:
   : https://www.iana.org/assignments/ianaiftype-mib

* NEW:
   - Description:
   : The type of interface where packets of this Flow are being sent. The value matches the value of managed object 'ifType'.

   - Additional Information:
   : See the assigned egress interface types at [https://www.iana.org/assignments/ianaiftype-mib].


## valueDistributionMethod

* OLD:
    - Description:
    : A description of the method used to distribute the counters from Contributing Flows into the Aggregated Flow records described by an associated scope, generally a Template. The method is deemed to apply to all the non-key Information Elements in the referenced scope for which value distribution is a valid operation; if the originalFlowsInitiated and/or originalFlowsCompleted Information Elements appear in the Template, they are not subject to this distribution method, as they each infer their own distribution method. The valueDistributionMethod registry is intended to list a complete set of possible value distribution methods.
    : See https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-value-distribution-method.

   - Additional Information:

* NEW:
    - Description:
    : A description of the method used to distribute the counters from Contributing Flows into the Aggregated Flow records described by an associated scope, generally a Template. The method is deemed to apply to all the non-key Information Elements in the referenced scope for which value distribution is a valid operation; if the originalFlowsInitiated and/or originalFlowsCompleted Information Elements appear in the Template, they are not subject to this distribution method, as they each infer their own distribution method. The valueDistributionMethod registry is intended to list a complete set of possible value distribution methods.

    - Additional Information:
    : See the assigned distributed methods at [https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-value-distribution-method].

## flowSelectorAlgorithm

* OLD:
    - Description:
    : This Information Element identifies the Intermediate Flow Selection Process technique (e.g., Filtering, Sampling) that is applied by the Intermediate Flow Selection Process. Most of these techniques have parameters. Its configuration parameter(s) MUST be clearly specified. Further Information Elements are needed to fully specify packet selection with these methods and all their parameters. Further method identifiers may be added to the flowSelectorAlgorithm registry. It might be necessary to define new Information Elements to specify their parameters.
    : Please note that the purpose of the flow selection techniques described in this document is the improvement of measurement functions as defined in the Scope (Section 1).
    : The Intermediate Flow Selection Process Techniques identifiers are defined at https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-flowselectoralgorithm.

   - Additional Information:

* NEW:
   - Description:
   : This Information Element identifies the Intermediate Flow Selection Process technique (e.g., Filtering, Sampling) that is applied by the Intermediate Flow Selection Process. Most of these techniques have parameters. Its configuration parameter(s) MUST be clearly specified. Further Information Elements are needed to fully specify packet selection with these methods and all their parameters. Further method identifiers may be added to the flowSelectorAlgorithm registry. It might be necessary to define new Information Elements to specify their parameters.

    - Additional Information:
    : See the assigned flow selector algorithms at [https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-flowselectoralgorithm].

## dataLinkFrameType

* OLD:
    - Description:
    : This Information Element specifies the type of the selected data link frame. Data link types are defined in the dataLinkFrameType registry. See https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-data-link-frame-type.
    : Further values may be assigned by IANA. Note that the assigned values are bits so that multiple observations can be OR'd together. The data link layer is defined in [ISO/IEC.7498-1:1994].

    - Additional Information:
    : [IEEE802.3][IEEE802.11][ISO/IEC.7498-1:1994]

* NEW:
    - Description:
    : This Information Element specifies the type of the selected data link frame. Data link types are defined in the dataLinkFrameType registry.
    : Further values may be assigned by IANA. Note that the assigned values are bits so that multiple observations can be OR'd together.

    - Additional Information:
    : See the assigned data link frame types at [https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-data-link-frame-type].
    : More information about the data link layer can be found in [IEEE802.3][IEEE802.11][ISO/IEC.7498-1:1994].

## mibCaptureTimeSemantics

* OLD:
    - Description:
    : Indicates when in the lifetime of the Flow the MIB value was retrieved from the MIB for a mibObjectIdentifier. This is used to indicate if the value exported was collected from the MIB closer to Flow creation or Flow export time and refers to the Timestamp fields included in the same Data Record.
    : This field SHOULD be used when exporting a mibObjectValue that specifies counters or statistics. If the MIB value was sampled by SNMP prior to the IPFIX Metering Process or Exporting Process retrieving the value (i.e., the data is already stale) and it is important to know the exact sampling time, then an additional observationTime* element should be paired with the OID using IPFIX Structured Data {{?RFC6313}}. Similarly, if different MIB capture times apply to different mibObjectValue elements within the Data Record, then individual mibCaptureTimeSemantics Information Elements should be paired with each OID using IPFIX Structured Data.
    : Values are listed in the mibCaptureTimeSemantics registry. See https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-mib-capture-time-semantics.

    - Additional Information:

* NEW:
    - Description:
    : Indicates when in the lifetime of the Flow the MIB value was retrieved from the MIB for a mibObjectIdentifier. This is used to indicate if the value exported was collected from the MIB closer to Flow creation or Flow export time and refers to the Timestamp fields included in the same Data Record.
    : This field SHOULD be used when exporting a mibObjectValue that specifies counters or statistics. If the MIB value was sampled by SNMP prior to the IPFIX Metering Process or Exporting Process retrieving the value (i.e., the data is already stale) and it is important to know the exact sampling time, then an additional observationTime* element should be paired with the OID using IPFIX Structured Data {{?RFC6313}}. Similarly, if different MIB capture times apply to different mibObjectValue elements within the Data Record, then individual mibCaptureTimeSemantics Information Elements should be paired with each OID using IPFIX Structured Data.
    : Values are listed in the mibCaptureTimeSemantics registry.

    - Additional Information:
    : See the assigned values for the MIB capture time semantics at [https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-mib-capture-time-semantics].

## natQuotaExceededEvent

* OLD:
    - Description:
    : This Information Element identifies the type of a NAT Quota Exceeded event. Values for this Information Element are listed in the "NAT Quota Exceeded Event Type" registry, see https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-nat-quota-exceeded-event.

    - Additional Information:
    : See {{?RFC0791}} for the definition of the IPv4 source address field.
    : See {{?RFC3022}} for the definition of NAT.
    : See {{?RFC3234}} for the definition of middleboxes.

* NEW:
    - Description:
    : This Information Element identifies the type of a NAT Quota Exceeded event. Values for this Information Element are listed in the "NAT Quota Exceeded Event Type" registry.

    - Additional Information:
    : See the assigned events for exceeded NAT quota at [https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-nat-quota-exceeded-event].
    : See {{?RFC0791}} for the definition of the IPv4 source address field.
    : See {{?RFC3022}} for the definition of NAT.
    : See {{?RFC3234}} for the definition of middleboxes.

## natThresholdEvent

* OLD:
    - Description:
    : This Information Element identifies a type of a NAT Threshold event. Values for this Information Element are listed in the "NAT Threshold Event Type" registry, see https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-nat-threshold-event.

    - Additional Information:
    : See {{?RFC0791}} for the definition of the IPv4 source address field.
    : See {{?RFC3022}} for the definition of NAT.
    : See {{?RFC3234}} for the definition of middleboxes.

* NEW:
    - Description:
    : This Information Element identifies a type of a NAT Threshold event. Values for this Information Element are listed in the "NAT Threshold Event Type" registry.

    - Additional Information:
    : See the assigned values for the NAT Threshold events at [https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-nat-threshold-event].
    : See {{?RFC0791}} for the definition of the IPv4 source address field.
    : See {{?RFC3022}} for the definition of NAT.
    : See {{?RFC3234}} for the definition of middleboxes.

# Misc {#misc}

This document requests IANA to update the description of the following entries in {{IANA-IPFIX}}.

## collectionTimeMilliseconds

* OLD:
   - Description:
   : The absolute timestamp at which the data within the scope containing this Information Element was received by a Collecting Process. This Information Element SHOULD be bound to its containing IPFIX Message via IPFIX Options and the messageScope Information Element, as defined below.

* NEW:
   - Description:
   : The absolute timestamp at which the data within the scope containing this Information Element was received by a Collecting Process. This Information Element SHOULD be bound to its containing IPFIX Message via IPFIX Options and the messageScope Information Element.

## messageMD5Checksum

* OLD:
    - Description:
    :  The MD5 checksum of the IPFIX Message containing this record. This Information Element SHOULD be bound to its containing IPFIX Message via an options record and the messageScope Information Element, as defined below, and SHOULD appear only once in a given IPFIX Message. To calculate the value of this Information Element, first buffer the containing IPFIX Message, setting the value of this Information Element to all zeroes. Then calculate the MD5 checksum of the resulting buffer as defined in {{?RFC1321}}, place the resulting value in this Information Element, and export the buffered message.
    : This Information Element is intended as a simple checksum only; therefore collision resistance and algorithm agility are not required, and MD5 is an appropriate message digest. This Information Element has a fixed length of 16 octets.

* NEW:
    - Description:
    : The MD5 checksum of the IPFIX Message containing this record. This Information Element SHOULD be bound to its containing IPFIX Message via an options record and the messageScope Information Element, and SHOULD appear only once in a given IPFIX Message. To calculate the value of this Information Element, first buffer the containing IPFIX Message, setting the value of this Information Element to all zeroes. Then calculate the MD5 checksum of the resulting buffer as defined in {{?RFC1321}}, place the resulting value in this Information Element, and export the buffered message.
    : This Information Element is intended as a simple checksum only; therefore collision resistance and algorithm agility are not required, and MD5 is an appropriate message digest. This Information Element has a fixed length of 16 octets.

## anonymizationFlags

* OLD:

~~~
+--------+----------+-----------------------------------------------+
| bit(s) | name     | description                                   |
| (LSB = |          |                                               |
| 0)     |          |                                               |
+--------+----------+-----------------------------------------------+
| 0-1    | SC       | Stability Class: see the Stability Class      |
|        |          | table below, and section Section 5.1.         |
| 2      | PmA      | Perimeter Anonymization: when set (1),        |
|        |          | source- Information Elements as described in  |
|        |          | [RFC5103] are interpreted as external         |
|        |          | addresses, and destination- Information       |
|        |          | Elements as described in [RFC5103] are        |
|        |          | interpreted as internal addresses, for the    |
|        |          | purposes of associating                       |
|        |          | anonymizationTechnique to Information         |
|        |          | Elements only; see Section 7.2.2 for details. |
|        |          | This bit MUST NOT be set when associated with |
|        |          | a non-endpoint (i.e., source- or              |
|        |          | destination-) Information Element.  SHOULD be |
|        |          | consistent within a record (i.e., if a        |
|        |          | source- Information Element has this flag     |
|        |          | set, the corresponding destination- element   |
|        |          | SHOULD have this flag set, and vice-versa.)   |
+--------+----------+-----------------------------------------------+
~~~

* NEW:

~~~
+--------+----------+-----------------------------------------------+
| bit(s) | name     | description                                   |
| (LSB = |          |                                               |
| 0)     |          |                                               |
+--------+----------+-----------------------------------------------+
| 0-1    | SC       | Stability Class: see the Stability Class      |
|        |          | table below, and Section 5.1 of [RFC6235].    |
| 2      | PmA      | Perimeter Anonymization: when set (1),        |
|        |          | source- Information Elements as described in  |
|        |          | [RFC5103] are interpreted as external         |
|        |          | addresses, and destination- Information       |
|        |          | Elements as described in [RFC5103] are        |
|        |          | interpreted as internal addresses, for the    |
|        |          | purposes of associating                       |
|        |          | anonymizationTechnique to Information         |
|        |          | Elements only; see Section 7.2.2 of [RFC6235] |
|        |          | for details.                                  |
|        |          | This bit MUST NOT be set when associated with |
|        |          | a non-endpoint (i.e., source- or              |
|        |          | destination-) Information Element.  SHOULD be |
|        |          | consistent within a record (i.e., if a        |
|        |          | source- Information Element has this flag     |
|        |          | set, the corresponding destination- element   |
|        |          | SHOULD have this flag set, and vice-versa.)   |
+--------+----------+-----------------------------------------------+
~~~

## informationElementDescription

* OLD:
    - Description:
    : A UTF-8 {{?RFC3629}} encoded Unicode string containing a human-readable description of an Information Element. The content of the informationElementDescription MAY be annotated with one or more language tags {{?RFC4646}}, encoded in-line {{?RFC2482}} within the UTF-8 string, in order to specify the language in which the description is written. Description text in multiple languages MAY tag each section with its own language tag; in this case, the description information in each language SHOULD have equivalent meaning. In the absence of any language tag, the "i-default" {{?RFC2277}} language SHOULD be assumed.
    : See the Security Considerations section for notes on string handling for Information Element type records.

* NEW:
    - Description:
    : A UTF-8 {{?RFC3629}} encoded Unicode string containing a human-readable description of an Information Element. The content of the informationElementDescription MAY be annotated with one or more language tags {{?RFC4646}}, encoded in-line {{?RFC2482}} within the UTF-8 string, in order to specify the language in which the description is written. Description text in multiple languages MAY tag each section with its own language tag; in this case, the description information in each language SHOULD have equivalent meaning. In the absence of any language tag, the "i-default" {{?RFC2277}} language SHOULD be assumed.
    : See the Security Considerations Section of {{?RFC5610}} for notes on string handling for Information Element type records.


## distinctCountOfDestinationIPAddress

* OLD:
    - Description:
    : The count of distinct destination IP address values for Original Flows contributing to this Aggregated Flow, without regard to IP version. This Information Element is preferred to the version-specific counters below, unless it is important to separate the counts by version.

* NEW:
   - Description:
   : The count of distinct destination IP address values for Original Flows contributing to this Aggregated Flow, without regard to IP version. This Information Element is preferred to the version-specific counters, unless it is important to separate the counts by version.

## externalAddressRealm

* OLD:
    - Description:
    : This Information Element represents the external address realm where the packet is originated from or destined to. The detailed definition is in the internal address realm as specified above.

* NEW:
   - Description:
   : This Information Element represents the external address realm where the packet is originated from or destined to.
   : See the internalAddressRealm IE for the detailed definition.


# Security Considerations

IPFIX security considerations are discussed in {{Section 8 of !RFC7012}}.


# IANA Considerations

Sections 4 to 7 include actions for IANA. These actions are not repeated here.

This document also requests IANA to update the reference clause of the "IPFIX Information Elements" registry {{IANA-IPFIX}} with the reference to this document.

## IPFIX Subregistry for IPv6 Extension Headers

This document requests IANA to create a new registry entitled "ipv6ExtensionHeaders Bits" under the IANA IPFIX registry group {{IANA-IPFIX}}.

The initial values of this registry are as follows:

~~~
   Bit Label   IPv6     Description
               Option
    0  DST      60      Destination Options for IPv6
    1  HOP       0      IPv6 Hop-by-Hop Option
    2                   Unassigned
    3  UNK              Unknown Layer 4 header
                        (compressed, encrypted, not supported)
    4  FRA0     44      Fragment header - first fragment
    5  RH       43      Routing header
    6  FRA1     44      Fragmentation header - not first fragment
    7 to 11             Unassigned
    12 MOB     135      Mobility Header
    13 ESP      50      Encapsulating Security Payload
    14 AH       51      Authentication Header
    15                  Unassigned
    16 HIP     139      Host Identity Protocol
    17 SHIM6   140      Shim6 Protocol
    18         253      Use for experimentation and testing
    19         254      Use for experimentation and testing
    20 to 255           Unassigned
~~~



Values are not added directly into this registry. When a new code is assigned to an IPv6 EH in {{IANA-EH}}, a free bit is selected by IANA for this EH from "ipv6ExtensionHeaders Bits" registry and the registry is updated with the details that mirror the assigned EH. The "Label" mirrors the "keyword" of an EH as indicated in {{IANA-Protocols}}, while the "IPv6 Option" mirrors the "Protocol Number" in {{IANA-EH}}.

IANA is requested to add the following note to the new registry:

Note:
: Values are not added directly into this registry. New codes are assigned to an IPv6 EH in {{IANA-EH}}.

Also, IANA is requested to add the following note to {{IANA-EH}}:

Note:
: When a new code is assigned to an IPv6 Extension Header, a free bit in [NEW_IPFIX_IPv6EH_SUBREGISTRY] is selected for this new Extension Header. [NEW_IPFIX_IPv6EH_SUBREGISTRY] is updated accordingly. Modifications to existing registrations must be mirrored in [NEW_IPFIX_IPv6EH_SUBREGISTRY].

> Note to the RFC Editor: Please replace [NEW_IPFIX_IPv6EH_SUBREGISTRY] with the link used by IANA for this new registry.

--- back

# Acknowledgments
{:numbered="false"}

Thanks to Paul Aitken for the review.

Thomas Graf tagged an issue with the forwardingStatus Information Element.
