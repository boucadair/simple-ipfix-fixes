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
        author:
        -
          organization: "IANA"
        target: https://www.iana.org/assignments/ipfix/ipfix.xhtml
        date: false

informative:
     RFC5103:
     RFC6235:
     CCO-NF9FMT:
       title: NetFlow Version 9 Flow-Record Format
       author:
        -
          organization: "Cisco"
       target: https://www.cisco.com/en/US/technologies/tk648/tk362/technologies_white_paper09186a00800a3db9.html
       date: May 2011
     Forwarding-Status:
        title: Forwarding Status (Value 89)
        author:
        -
          organization: "IANA"
        target: https://www.iana.org/assignments/ipfix/ipfix.xhtml#forwarding-status
        date: false


--- abstract

This document provides simple fixes to the IANA IP Flow Information Export (IPFIX) registry. Specifically, this document provides updates to fix shortcomings in the description of some Information Elements (IE), updates to ensure a consistent structure when citing an existing IANA registry, and updates to fix broken pointers, orphaned section references, etc. The updates are also meant to bring some consistency among the entries of the registry.


--- middle

# Introduction

When OPSAWG was considering {{?RFC9565}} which updates {{?RFC7125}}, the WG realized that some parts of the IANA IP Flow Information Export (IPFIX) registry {{IANA-IPFIX}} were not up-to-date. This document intends to update the IANA registry and bring some consistency among the entries of the registry.

As discussed with IANA during the publication process of {{?RFC9487}}, the "Additional Information" entry in {{IANA-IPFIX}} should contain a link to an existing registry, when applicable, as opposed to having:

- A link to an existing registry in the "Description" entry.
- The registry detailed values repeated in the "Description" entry. This practice has the drawback that the description must be updated each time the registry is updated.

Therefore, this document lists a set of simple fixes to the IPFIX IANA registry {{IANA-IPFIX}}. These fixes are classified as follows:

- Updates that fix a shortcoming in the description of an IE ({{desc}}).
- Updates that require adding a pointer to an existing IANA registry ({{to-iana}}).
- Updates that are meant to ensure a consistent structure when calling an existing IANA registry ({{consistent}}).
- Miscellaneous updates that fix broken pointers, orphaned section references, etc. ({{misc}}).

These updates are also meant to facilitate the automatic extraction of the values maintained in IANA registries (e.g., with a cron job), required by Collectors to be able to support new IPFIX IEs and, more importantly, adequately interpret new values in registries specified by those IPFIX IEs.

Note that, as per {{Section 5 of !RFC7012}}, {{IANA-IPFIX}} is the normative reference for the IPFIX IEs that were defined in {{?RFC5102}}. Therefore, the updates in this document do not update any part of {{!RFC7011}}.

Likewise, this document is not marked as formally updating {{?RFC5477}}, {{?RFC5610}}, {{?RFC5655}}, {{?RFC6235}}, {{?RFC6759}}, {{?RFC7014}}, {{?RFC7015}}, {{?RFC7133}}, {{?RFC7270}}, {{?RFC8038}}, and {{?RFC8158}}.

# Conventions and Definitions

{::boilerplate bcp14-tagged}

This document uses the IPFIX-specific terminology (Information Element, Template,
   Collector,  Data Record, Flow Record, Exporting Process,
   Collecting Process, etc.) defined in
   Section 2 of {{!RFC7011}}. As in {{!RFC7011}}, these IPFIX-specific terms
   have the first letter of a word capitalized.

# Why An RFC is Needed for These Updates?

Many of the edits in this document may be handled by the IPFIX Experts (informally called the IE-DOCTORS {{!RFC7013}}). However, and given that many of the impacted IEs were created via the IETF stream, the following from {{Section 5.1 of !RFC7013}} is followed:

   > This process should not in any way be construed as allowing the IE-DOCTORS to overrule IETF consensus.  Specifically, Information Elements in the IANA IE registry that were added with IETF consensus require IETF consensus for revision or deprecation.

# Update the Description {#desc}

## sourceTransportPort

### OLD

Description:
: The source port identifier in the transport header. For the transport protocols UDP, TCP, and SCTP, this is the source port number given in the respective header. This field MAY also be used for future transport protocols that have 16-bit source port identifiers.

Additional Information:
: See {{?RFC0768}} for the definition of the UDP source port field.
: See {{?RFC9293}} for the definition of the TCP source port field.
: See {{?RFC9260}} for the definition of SCTP.
: Additional information on defined UDP and TCP port numbers can be found at [https://www.iana.org/assignments/service-names-port-numbers].

### NEW

Description:
: The source port identifier in the transport protocol header. For transport protocols such as UDP, TCP, SCTP, and DCCP, this is the source port number given in the respective header. This field MAY also be used for future transport protocols that have 16-bit source port identifiers.

Additional Information:
: See {{?RFC0768}} for the definition of the UDP source port field.
: See {{?RFC9293}} for the definition of the TCP source port field.
: See {{?RFC9260}} for the definition of the SCTP source port number field.
: See {{?RFC4340}} for the definition of the DCCP source port field.
: See the assigned transport protocol (e.g., UDP, TCP, SCTP, and DCCP) port numbers at https://www.iana.org/assignments/service-names-port-numbers.

## destinationTransportPort

### OLD

Description:
: The destination port identifier in the transport header. For the transport protocols UDP, TCP, and SCTP, this is the destination port number given in the respective header. This field MAY also be used for future transport protocols that have 16-bit destination port identifiers.

Additional Information:
: See {{?RFC0768}} for the definition of the UDP source port field.
: See {{?RFC9293}} for the definition of the TCP source port field.
: See {{?RFC9260}} for the definition of SCTP.
: Additional information on defined UDP and TCP port numbers can be found at [https://www.iana.org/assignments/service-names-port-numbers].

### NEW

Description:
: The destination port identifier in the transport protocol header. For transport protocols such as UDP, TCP, SCTP, and DCCP, this is the destination port number given in the respective header. This field MAY also be used for future transport protocols that have 16-bit destination port identifiers.

Additional Information:
: See {{?RFC0768}} for the definition of the UDP destination port field.
: See {{?RFC9293}} for the definition of the TCP destination port field.
: See {{?RFC9260}} for the definition of the SCTP destination port number field.
: See {{?RFC4340}} for the definition of the DCCP destination port field.
: See the assigned transport protocol (e.g., UDP, TCP, SCTP, and DCCP) port numbers at https://www.iana.org/assignments/service-names-port-numbers.


## forwardingStatus

The current forwardingStatus entry in {{IANA-IPFIX}} deviates from what is provided in {{?RFC7270}}. In particular, the registered Abstract Data Type is unsigned8, while it must be unsigned32. The following update fixes that issue. The description is also updated to clarify the use of the reduced-size encoding as per {{Section 6.2 of !RFC7011}}.

### OLD

~~~
   - Description:  This Information Element describes the forwarding
                   status of the flow and any attached reasons.

                   The layout of the encoding is as follows:

                   MSB  -  0   1   2   3   4   5   6   7  -  LSB
                         +---+---+---+---+---+---+---+---+
                         | Status|  Reason code or flags |
                         +---+---+---+---+---+---+---+---+

                   See the Forwarding Status sub-registries at
                   [Forwarding-Status].

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

### NEW

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

   - Additional Information: See "NetFlow Version 9 Flow-Record Format"
             [CCO-NF9FMT]. See the Forwarding Status sub-registries
             at [Forwarding-Status].

   - Abstract Data Type: unsigned32
~~~

## collectorTransportPort

### OLD

Description:
: The destination port identifier to which the Exporting Process sends Flow information. For the transport protocols UDP, TCP, and SCTP, this is the destination port number. This field MAY also be used for future transport protocols that have 16-bit source port identifiers.

Additional Information:
: See {{?RFC0768}} for the definition of the UDP source port field.
: See {{?RFC9293}} for the definition of the TCP source port field.
: See {{?RFC9260}} for the definition of SCTP.
: Additional information on defined UDP and TCP port numbers can be found at [https://www.iana.org/assignments/service-names-port-numbers].

### NEW

Description:
: The destination port identifier to which the Exporting Process sends Flow information. For transport protocols such as UDP, TCP, and SCTP, this is the destination port number. This field MAY also be used for future transport protocols that have 16-bit source port identifiers.

Additional Information:
: See {{?RFC0768}} for the definition of the UDP destination port field.
: See {{?RFC9293}} for the definition of the TCP destination port field.
: See {{?RFC9260}} for the definition of the SCTP destination port number field.
: See the assigned transport protocol (e.g., TCP, UDP, and SCTP) port numbers at https://www.iana.org/assignments/service-names-port-numbers.

## exporterTransportPort

### OLD

Description:
: The source port identifier from which the Exporting Process sends Flow information. For the transport protocols UDP, TCP, and SCTP, this is the source port number. This field MAY also be used for future transport protocols that have 16-bit source port identifiers. This field may be useful for distinguishing multiple Exporting Processes that use the same IP address.

Additional Information:
: See {{?RFC0768}} for the definition of the UDP source port field.
: See {{?RFC9293}} for the definition of the TCP source port field.
: See {{?RFC9260}} for the definition of SCTP.
: Additional information on defined UDP and TCP port numbers can be found at [https://www.iana.org/assignments/service-names-port-numbers].

### NEW

Description:
: The source port identifier from which the Exporting Process sends Flow information. For transport protocols such as UDP, TCP, and SCTP, this is the source port number. This field MAY also be used for future transport protocols that have 16-bit source port identifiers.

Additional Information:
: See {{?RFC0768}} for the definition of the UDP source port field.
: See {{?RFC9293}} for the definition of the TCP source port field.
: See {{?RFC9260}} for the definition of the SCTP source port number field.
: See the assigned transport protocol (e.g., UDP, TCP, and SCTP) port numbers at https://www.iana.org/assignments/service-names-port-numbers.


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

### OLD

Description:
: This field identifies the control protocol that allocated the top-of-stack label. Values for this field are listed in the MPLS label type registry.
: See https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-mpls-label-type.

Additional Information:
: See {{?RFC3031}} for the MPLS label structure.
: See the list of MPLS label types assigned by IANA at [https://www.iana.org/assignments/mpls-label-values].

### NEW

Description:
: This field identifies the control protocol that allocated the top-of-stack label. Values for this field are listed in the MPLS label type registry.

Additional Information:
: See the list of MPLS label types assigned by IANA at [https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-mpls-label-type].
: See {{?RFC3031}} for the MPLS label structure.

## classificationEngineId

### OLD

Description:
: A unique identifier for the engine that determined the Selector ID. Thus, the Classification Engine ID defines the context for the Selector ID. The Classification Engine can be considered a specific registry for application assignments.
: Values for this field are listed in the Classification Engine IDs registry. See https://www.iana.org/assignments/ipfix/ipfix.xhtml#classification-engine-ids.

### NEW

Description:
: A unique identifier for the engine that determined the Selector ID. Thus, the Classification Engine ID defines the context for the Selector ID. The Classification Engine can be considered a specific registry for application assignments.
: Values for this field are listed in the Classification Engine IDs registry.

Additional Information:
: See https://www.iana.org/assignments/ipfix/ipfix.xhtml#classification-engine-ids.

## flowEndReason

### OLD

Description:
: The reason for Flow termination. Values are listed in the flowEndReason registry. See https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-flow-end-reason.


### NEW

Description:
: The reason for Flow termination. Values are listed in the flowEndReason registry.

Additional Information:
: See the flowEndReason registry available at [https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-flow-end-reason].

## natOriginatingAddressRealm

### OLD

Description:
: Indicates whether the session was created because traffic originated in the private or public address realm. postNATSourceIPv4Address, postNATDestinationIPv4Address, postNAPTSourceTransportPort, and postNAPTDestinationTransportPort are qualified with the address realm in perspective.
: Values are listed in the natOriginatingAddressRealm registry. See https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-nat-originating-address-realm.

Additional Information:
: See {{?RFC3022}} for the definition of NAT.

### NEW

Description:
: Indicates whether the session was created because traffic originated in the private or public address realm. postNATSourceIPv4Address, postNATDestinationIPv4Address, postNAPTSourceTransportPort, and postNAPTDestinationTransportPort are qualified with the address realm in perspective.
: Values are listed in the natOriginatingAddressRealm registry.

Additional Information:
: See the assigned NAT originating address realm values at [https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-nat-originating-address-realm].
: See {{?RFC3022}} for the definition of NAT.

## natEvent

### OLD

Description:
: This Information Element identifies a NAT event. This IE identifies the type of a NAT event. Examples of NAT events include, but are not limited to, NAT translation create, NAT translation delete, Threshold Reached, or Threshold Exceeded, etc. Values for this Information Element are listed in the "NAT Event Type" registry, see https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-nat-event-type.

Additional Information:
: See {{?RFC3022}} for the definition of NAT.
: See {{?RFC3234}} for the definition of middleboxes.
: See {{?RFC8158}} for the definitions of values 4-16.

### NEW

Description:
: This Information Element identifies a NAT event. This IE identifies the type of a NAT event. Examples of NAT events include, but are not limited to, NAT translation create, NAT translation delete, Threshold Reached, or Threshold Exceeded, etc. Values for this Information Element are listed in the "NAT Event Type" registry.

Additional Information:
: See the assigned NAT Event Types at [https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-nat-event-type].
: See {{?RFC3022}} for the definition of NAT.
: See {{?RFC3234}} for the definition of middleboxes.
: See {{?RFC8158}} for the definitions of values 4-16.

## firewallEvent

### OLD

Description:
: Indicates a firewall event. Allowed values are listed in the firewallEvent registry.
: See https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-firewall-event.

### NEW

Description:
: Indicates a firewall event. Allowed values are listed in the firewallEvent registry.

Additional Information:
: See the assigned firewall events at [https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-firewall-event].

## biflowDirection

### OLD

Description:
:  A description of the direction assignment method used to assign the Biflow Source and Destination. This Information Element MAY be present in a Flow Data Record, or applied to all flows exported from an Exporting Process or Observation Domain using IPFIX Options. If this Information Element is not present in a Flow Record or associated with a Biflow via scope, it is assumed that the configuration of the direction assignment method is done out-of-band. Note that when using IPFIX Options to apply this Information Element to all flows within an Observation Domain or from an Exporting Process, the Option SHOULD be sent reliably. If reliable transport is not available (i.e., when using UDP), this Information Element SHOULD appear in each Flow Record. Values are listed in the biflowDirection registry. See [https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-biflow-direction].

### NEW

Description:
: A description of the direction assignment method used to assign the Biflow Source and Destination. This Information Element MAY be present in a Flow Data Record, or applied to all flows exported from an Exporting Process or Observation Domain using IPFIX Options. If this Information Element is not present in a Flow Record or associated with a Biflow via scope, it is assumed that the configuration of the direction assignment method is done out-of-band. Note that when using IPFIX Options to apply this Information Element to all flows within an Observation Domain or from an Exporting Process, the Option SHOULD be sent reliably. If reliable transport is not available (i.e., when using UDP), this Information Element SHOULD appear in each Flow Record. Values are listed in the biflowDirection registry.

Additional Information:
: See the assigned biflow direction values at [https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-biflow-direction].


## observationPointType

### OLD

Description:
: Type of observation point. Values are listed in the observationPointType registry. See https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-observation-point-type.

### NEW

Description:
: Type of observation point. Values are listed in the observationPointType registry.

Additional Information:
: See the assigned observation point types at [https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-observation-point-type].

## anonymizationTechnique

### OLD

Description:
: A description of the anonymization technique applied to a referenced Information Element within a referenced Template. Each technique may be applicable only to certain Information Elements and recommended only for certain Information Elements. Values are listed in the anonymizationTechnique registry. See https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-anonymization-technique.

### NEW

Description:
: A description of the anonymization technique applied to a referenced Information Element within a referenced Template. Each technique may be applicable only to certain Information Elements and recommended only for certain Information Elements. Values are listed in the anonymizationTechnique registry.

Additional Information:
: See the assigned anonymization techniques at [https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-anonymization-technique].

## natType

### OLD

Description:
: Values are listed in the natType registry.
: See https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-nat-type.

Additional Information:
: See {{?RFC3022}} for the definition of NAT.
: See {{?RFC1631}} for the definition of NAT44.
: See {{?RFC6144}} for the definition of NAT64.
: See {{?RFC6146}} for the definition of NAT46.
: See {{?RFC6296}} for the definition of NAT66.
: See {{?RFC0791}} for the definition of IPv4.
: See {{?RFC8200}} for the definition of IPv6.

### NEW

Description:
: This Information Element identifies the NAT type applied to packets of the Flow.
: Values are listed in the natType registry.

Additional Information:
: See the assigned NAT types at [https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-nat-type].
: See {{?RFC3022}} for the definition of NAT and NAT44.
: See {{?RFC6144}} for the definition of NAT46.
: See {{?RFC6146}} for the definition of NAT64.
: See {{?RFC6296}} for the definition of NPTv6.
: See {{?RFC0791}} for the definition of IPv4.
: See {{?RFC8200}} for the definition of IPv6.

> Note to IANA: This change also corrects errors in the pointers provided for NAT46/NAT64.

## selectorAlgorithm

### OLD

Description:
: This Information Element identifies the packet selection methods (e.g., Filtering, Sampling) that are applied by the Selection Process. Most of these methods have parameters. Further Information Elements are needed to fully specify packet selection with these methods and all their parameters. The methods listed below are defined in {{?RFC5475}}. For their parameters, Information Elements are defined in the information model document. The names of these Information Elements are listed for each method identifier. Further method identifiers may be added to the list below. It might be necessary to define new Information Elements to specify their parameters.
: The following packet selection methods identifiers are defined here: https://www.iana.org/assignments/psamp-parameters.
: There is a broad variety of possible parameters that could be used for Property match Filtering (5) but currently there are no agreed parameters specified.

### NEW

Description:
: This Information Element identifies the packet selection methods (e.g., Filtering, Sampling) that are applied by the Selection Process. Most of these methods have parameters. Further Information Elements are needed to fully specify packet selection with these methods and all their parameters. For the methods parameters, Information Elements are defined in the information model document {{?RFC5102}}. The names of these Information Elements are listed for each method identifier. Further method identifiers may be added to the list. It might be necessary to define new Information Elements to specify their parameters.
: There is a broad variety of possible parameters that could be used for Property match Filtering (5) but currently there are no agreed parameters specified.

Additional Information:
: See the assigned PSAMP parameters at [https://www.iana.org/assignments/psamp-parameters].

## informationElementDataType

### OLD

Description:
: A description of the abstract data type of an IPFIX information element. These are taken from the abstract data types defined in section 3.1 of the IPFIX Information Model {{?RFC5102}}; see that section for more information on the types described in the [informationElementDataType] subregistry. These types are registered in the IANA IPFIX Information Element Data Type subregistry. This subregistry is intended to assign numbers for type names, not to provide a mechanism for adding data types to the IPFIX Protocol, and as such requires a Standards Action {{?RFC8126}} to modify.

### NEW

Description:
: A description of the abstract data type of an IPFIX information element.These are taken from the abstract data types defined in Section 3.1 of the IPFIX Information Model {{?RFC5102}}; see that section for more information on the types described in the [informationElementDataType] subregistry. These types are registered in the IANA IPFIX Information Element Data Type subregistry.
: The [informationElementDataType] subregistry is intended to assign numbers for type names, not to provide a mechanism for adding data types to the IPFIX Protocol, and as such requires a Standards Action {{?RFC8126}} to modify.

Additional Information:
: See the assigned element data types at [https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-information-element-data-types].

## informationElementSemantics

### OLD

Description:
: A description of the semantics of an IPFIX Information Element. These are taken from the data type semantics defined in section 3.2 of the IPFIX Information Model {{?RFC5102}}; see that section for more information on the types defined in the [IPFIX Information Element Semantics] subregistry. This field may take the values in the semantics registry; the special value 0x00 (default) is used to note that no semantics apply to the field; it cannot be manipulated by a Collecting Process or File Reader that does not understand it a priori. These semantics are registered in the IANA IPFIX Information Element Semantics subregistry. This subregistry is intended to assign numbers for semantics names, not to provide a mechanism for adding semantics to the IPFIX Protocol, and as such requires a Standards Action {{?RFC8126}} to modify.

### NEW

Description:
: A description of the semantics of an IPFIX Information Element. These are taken from the data type semantics defined in Section 3.2 of the IPFIX Information Model {{?RFC5102}}; see that section for more information on the types defined in the [IPFIX Information Element Semantics] subregistry. This field may take the values in the [IPFIX Information Element Semantics] subregistry. The special value 0x00 (default) is used to note that no semantics apply to the field; it cannot be manipulated by a Collecting Process or File Reader that does not understand it a priori.
: The [IPFIX Information Element Semantics] subregistry is intended to assign numbers for semantics names, not to provide a mechanism for adding semantics to the IPFIX Protocol, and as such requires a Standards Action {{?RFC8126}} to modify.

Additional Information:
: See the assigned semantics of an IPFIX Information Element at [https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-information-element-semantic].

## informationElementUnits

### OLD

Description:
: A description of the units of an IPFIX Information Element. These correspond to the units implicitly defined in the Information Element definitions in section 5 of the IPFIX Information Model {{?RFC5102}}; see that section for more information on the types described in the informationElementsUnits subregistry. This field may take the values in Table 3 below; the special value 0x00 (none) is used to note that the field is unitless. These types are registered in the [IANA IPFIX Information Element Units] subregistry.

### NEW

Description:
: A description of the units of an IPFIX Information Element. These correspond to the units implicitly defined in the Information Element definitions in Section 5 of the IPFIX Information Model {{?RFC5102}}; see that section for more information on the types described in the informationElementsUnits subregistry. These types can take the values in the [IANA IPFIX Information Element Units] subregistry. The special value 0x00 (none) is used to note that the field is unitless.

Additional Information:
: See the assigned units of an IPFIX Information Element at [IANA IPFIX Information Element Units].


## portRangeStart

### OLD

Description:
: The port number identifying the start of a range of ports. A value of zero indicates that the range start is not specified, ie the range is defined in some other way.
: Additional information on defined TCP port numbers can be found at https://www.iana.org/assignments/service-names-port-numbers.

### NEW

Description:
: The port number identifying the start of a range of port numbers. A value of zero indicates that the range start is not specified, i.e., the range is defined in some other way.

Additional Information:
: See the assigned transport protocol (e.g., UDP, TCP, SCTP, and DCCP) port numbers at https://www.iana.org/assignments/service-names-port-numbers.

## portRangeEnd

### OLD

Description:
: The port number identifying the end of a range of ports. A value of zero indicates that the range end is not specified, ie the range is defined in some other way. Additional information on defined TCP port numbers can be found at https://www.iana.org/assignments/service-names-port-numbers.

### NEW

Description:
: The port number identifying the end of a range of port numbers. A value of zero indicates that the range end is not specified, i.e., the range is defined in some other way.

Additional Information:
: See the assigned transport protocol (e.g., UDP, TCP, SCTP, and DCCP) port numbers at https://www.iana.org/assignments/service-names-port-numbers.

## ingressInterfaceType

### OLD

Description:
: The type of interface where packets of this Flow are being received. The value matches the value of managed object 'ifType' as defined in https://www.iana.org/assignments/ianaiftype-mib.

Additional Information:
: https://www.iana.org/assignments/ianaiftype-mib

### NEW

Description:
: The type of interface where packets of this Flow are being received. The value matches the value of managed object 'ifType'.

Additional Information:
: See the assigned ingress interface types at [https://www.iana.org/assignments/ianaiftype-mib].

## egressInterfaceType

### OLD

Description:
: The type of interface where packets of this Flow are being sent. The value matches the value of managed object 'ifType' as defined in https://www.iana.org/assignments/ianaiftype-mib.

Additional Information:
: https://www.iana.org/assignments/ianaiftype-mib

### NEW

Description:
: The type of interface where packets of this Flow are being sent. The value matches the value of managed object 'ifType'.

Additional Information:
: See the assigned egress interface types at [https://www.iana.org/assignments/ianaiftype-mib].


## valueDistributionMethod

### OLD

Description:
: A description of the method used to distribute the counters from Contributing Flows into the Aggregated Flow records described by an associated scope, generally a Template. The method is deemed to apply to all the non-key Information Elements in the referenced scope for which value distribution is a valid operation; if the originalFlowsInitiated and/or originalFlowsCompleted Information Elements appear in the Template, they are not subject to this distribution method, as they each infer their own distribution method. The valueDistributionMethod registry is intended to list a complete set of possible value distribution methods.
: See https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-value-distribution-method.

### NEW

Description:
: A description of the method used to distribute the counters from Contributing Flows into the Aggregated Flow records described by an associated scope, generally a Template. The method is deemed to apply to all the non-key Information Elements in the referenced scope for which value distribution is a valid operation; if the originalFlowsInitiated and/or originalFlowsCompleted Information Elements appear in the Template, they are not subject to this distribution method, as they each infer their own distribution method. The valueDistributionMethod registry is intended to list a complete set of possible value distribution methods.

Additional Information:
: See the assigned value distribution methods at [https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-value-distribution-method].

## flowSelectorAlgorithm

### OLD

Description:
: This Information Element identifies the Intermediate Flow Selection Process technique (e.g., Filtering, Sampling) that is applied by the Intermediate Flow Selection Process. Most of these techniques have parameters. Its configuration parameter(s) MUST be clearly specified. Further Information Elements are needed to fully specify packet selection with these methods and all their parameters. Further method identifiers may be added to the flowSelectorAlgorithm registry. It might be necessary to define new Information Elements to specify their parameters.
: Please note that the purpose of the flow selection techniques described in this document is the improvement of measurement functions as defined in the Scope (Section 1).
: The Intermediate Flow Selection Process Techniques identifiers are defined at https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-flowselectoralgorithm.

### NEW

Description:
: This Information Element identifies the Intermediate Flow Selection Process technique (e.g., Filtering, Sampling) that is applied by the Intermediate Flow Selection Process. Most of these techniques have parameters. Its configuration parameter(s) MUST be clearly specified. Further Information Elements are needed to fully specify packet selection with these methods and all their parameters. Further method identifiers may be added to the flowSelectorAlgorithm registry. It might be necessary to define new Information Elements to specify their parameters.

Additional Information:
: See the assigned flow selector algorithms at [https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-flowselectoralgorithm].

## dataLinkFrameType

### OLD

Description:
: This Information Element specifies the type of the selected data link frame. Data link types are defined in the dataLinkFrameType registry. See https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-data-link-frame-type.
: Further values may be assigned by IANA. Note that the assigned values are bits so that multiple observations can be OR'd together. The data link layer is defined in [ISO/IEC.7498-1:1994].

Additional Information:
: (IEEE802.3)(IEEE802.11)(ISO/IEC.7498-1:1994)

### NEW

Description:
: This Information Element specifies the type of the selected data link frame. Data link types are defined in the dataLinkFrameType registry.
: Further values may be assigned by IANA. Note that the assigned values are bits so that multiple observations can be OR'd together.

Additional Information:
: See the assigned data link frame types at [https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-data-link-frame-type].
: More information about the data link layer can be found in (IEEE802.3)(IEEE802.11)(ISO/IEC.7498-1:1994).

## mibCaptureTimeSemantics

### OLD

Description:
: Indicates when in the lifetime of the Flow the MIB value was retrieved from the MIB for a mibObjectIdentifier. This is used to indicate if the value exported was collected from the MIB closer to Flow creation or Flow export time and refers to the Timestamp fields included in the same Data Record.
: This field SHOULD be used when exporting a mibObjectValue that specifies counters or statistics. If the MIB value was sampled by SNMP prior to the IPFIX Metering Process or Exporting Process retrieving the value (i.e., the data is already stale) and it is important to know the exact sampling time, then an additional observationTime* element should be paired with the OID using IPFIX Structured Data {{?RFC6313}}. Similarly, if different MIB capture times apply to different mibObjectValue elements within the Data Record, then individual mibCaptureTimeSemantics Information Elements should be paired with each OID using IPFIX Structured Data.
: Values are listed in the mibCaptureTimeSemantics registry. See https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-mib-capture-time-semantics.

### NEW

Description:
: Indicates when in the lifetime of the Flow the MIB value was retrieved from the MIB for a mibObjectIdentifier. This is used to indicate if the value exported was collected from the MIB closer to Flow creation or Flow export time and refers to the Timestamp fields included in the same Data Record.
: This field SHOULD be used when exporting a mibObjectValue that specifies counters or statistics. If the MIB value was sampled by SNMP prior to the IPFIX Metering Process or Exporting Process retrieving the value (i.e., the data is already stale) and it is important to know the exact sampling time, then an additional observationTime* element should be paired with the OID using IPFIX Structured Data {{?RFC6313}}. Similarly, if different MIB capture times apply to different mibObjectValue elements within the Data Record, then individual mibCaptureTimeSemantics Information Elements should be paired with each OID using IPFIX Structured Data.
: Values are listed in the mibCaptureTimeSemantics registry.

Additional Information:
: See the assigned values for the MIB capture time semantics at [https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-mib-capture-time-semantics].

## natQuotaExceededEvent

### OLD

Description:
: This Information Element identifies the type of a NAT Quota Exceeded event. Values for this Information Element are listed in the "NAT Quota Exceeded Event Type" registry, see https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-nat-quota-exceeded-event.

Additional Information:
: See {{?RFC0791}} for the definition of the IPv4 source address field.
: See {{?RFC3022}} for the definition of NAT.
: See {{?RFC3234}} for the definition of middleboxes.

### NEW

Description:
: This Information Element identifies the type of a NAT Quota Exceeded event. Values for this Information Element are listed in the "NAT Quota Exceeded Event Type" registry.

Additional Information:
: See the assigned events for exceeded NAT quota at [https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-nat-quota-exceeded-event].
: See {{?RFC0791}} for the definition of the IPv4 source address field.
: See {{?RFC3022}} for the definition of NAT.
: See {{?RFC3234}} for the definition of middleboxes.

## natThresholdEvent

### OLD

Description:
: This Information Element identifies a type of a NAT Threshold event. Values for this Information Element are listed in the "NAT Threshold Event Type" registry, see https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-nat-threshold-event.

Additional Information:
: See {{?RFC0791}} for the definition of the IPv4 source address field.
: See {{?RFC3022}} for the definition of NAT.
: See {{?RFC3234}} for the definition of middleboxes.

### NEW

Description:
: This Information Element identifies a type of a NAT Threshold event. Values for this Information Element are listed in the "NAT Threshold Event Type" registry.

Additional Information:
: See the assigned values for the NAT Threshold events at [https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-nat-threshold-event].
: See {{?RFC0791}} for the definition of the IPv4 source address field.
: See {{?RFC3022}} for the definition of NAT.
: See {{?RFC3234}} for the definition of middleboxes.

# Misc {#misc}

This document requests IANA to update the description of the following entries in {{IANA-IPFIX}}.

## collectionTimeMilliseconds

### OLD

Description:
: The absolute timestamp at which the data within the scope containing this Information Element was received by a Collecting Process. This Information Element SHOULD be bound to its containing IPFIX Message via IPFIX Options and the messageScope Information Element, as defined below.

### NEW

Description:
: The absolute timestamp at which the data within the scope containing this Information Element was received by a Collecting Process. This Information Element SHOULD be bound to its containing IPFIX Message via IPFIX Options and the messageScope Information Element.

## messageMD5Checksum

### OLD

Description:
:  The MD5 checksum of the IPFIX Message containing this record. This Information Element SHOULD be bound to its containing IPFIX Message via an options record and the messageScope Information Element, as defined below, and SHOULD appear only once in a given IPFIX Message. To calculate the value of this Information Element, first buffer the containing IPFIX Message, setting the value of this Information Element to all zeroes. Then calculate the MD5 checksum of the resulting buffer as defined in {{?RFC1321}}, place the resulting value in this Information Element, and export the buffered message.
: This Information Element is intended as a simple checksum only; therefore collision resistance and algorithm agility are not required, and MD5 is an appropriate message digest. This Information Element has a fixed length of 16 octets.

### NEW

Description:
: The MD5 checksum of the IPFIX Message containing this record. This Information Element SHOULD be bound to its containing IPFIX Message via an options record and the messageScope Information Element, and SHOULD appear only once in a given IPFIX Message. To calculate the value of this Information Element, first buffer the containing IPFIX Message, setting the value of this Information Element to all zeroes. Then calculate the MD5 checksum of the resulting buffer as defined in {{?RFC1321}}, place the resulting value in this Information Element, and export the buffered message.
: This Information Element is intended as a simple checksum only; therefore collision resistance and algorithm agility are not required, and MD5 is an appropriate message digest. This Information Element has a fixed length of 16 octets.

## anonymizationFlags

### OLD

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

### NEW

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
|        |          | SHOULD have this flag set, and vice versa.)   |
+--------+----------+-----------------------------------------------+
~~~

## informationElementDescription

### OLD

Description:
: A UTF-8 {{?RFC3629}} encoded Unicode string containing a human-readable description of an Information Element. The content of the informationElementDescription MAY be annotated with one or more language tags {{?RFC4646}}, encoded in-line {{?RFC2482}} within the UTF-8 string, in order to specify the language in which the description is written. Description text in multiple languages MAY tag each section with its own language tag; in this case, the description information in each language SHOULD have equivalent meaning. In the absence of any language tag, the "i-default" {{?RFC2277}} language SHOULD be assumed.
: See the Security Considerations section for notes on string handling for Information Element type records.

### NEW

Description:
: A UTF-8 {{?RFC3629}} encoded Unicode string containing a human-readable description of an Information Element. The content of the informationElementDescription MAY be annotated with one or more language tags {{?RFC4646}}, encoded in-line {{?RFC2482}} within the UTF-8 string, in order to specify the language in which the description is written. Description text in multiple languages MAY tag each section with its own language tag; in this case, the description information in each language SHOULD have equivalent meaning. In the absence of any language tag, the "i-default" {{?RFC2277}} language SHOULD be assumed.
: See the Security Considerations Section of {{?RFC5610}} for notes on string handling for Information Element type records.


## distinctCountOfDestinationIPAddress

### OLD

Description:
: The count of distinct destination IP address values for Original Flows contributing to this Aggregated Flow, without regard to IP version. This Information Element is preferred to the version-specific counters below, unless it is important to separate the counts by version.

### NEW

Description:
: The count of distinct destination IP address values for Original Flows contributing to this Aggregated Flow, without regard to IP version. This Information Element is preferred to the version-specific counters, unless it is important to separate the counts by version.

## externalAddressRealm

### OLD

Description:
: This Information Element represents the external address realm where the packet is originated from or destined to. The detailed definition is in the internal address realm as specified above.

### NEW

Description:
: This Information Element represents the external address realm where the packet is originated from or destined to.
: See the internalAddressRealm IE for the detailed definition.


# Security Considerations

This document does not add new security considerations to those
already discussed for IPFIX in {{Section 8 of !RFC7012}}.


# IANA Considerations

Sections 4 to 7 include actions for IANA. These actions are not repeated here.

This document also requests IANA to add the RFC number to be assigned to this document to the reference clause of the "IPFIX Information Elements" registry {{IANA-IPFIX}}.

Also, this document requests IANA to consistently reference the "Service Name and Transport Protocol Port Number" through the registry as follows

OLD:
: Additional information on defined UDP and TCP port numbers can be found at http://www.iana.org/assignments/port-numbers.

NEW:
: See the assigned transport protocol (e.g., UDP, TCP, SCTP, and DCCP) port numbers at https://www.iana.org/assignments/service-names-port-numbers.


--- back

# Acknowledgments
{:numbered="false"}

Many thanks to Paul Aitken for the review and many suggestions that enhanced this specification. Special thanks to Andrew Feren for sharing data about scans of IPFIX data he collected.

Thomas Graf tagged an issue with the forwardingStatus Information Element and for the Shepherd review.

Thanks to Eric Vyncke for the review and comments.

Thanks to Qin Wu for the opsdir review, Behcet Sarikay for the genart review, Martin Duke for the tsvart review, and Donald Eastlake for the intdir review.

Thanks to Mahesh Jethanandani for the AD review.
