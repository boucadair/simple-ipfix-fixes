---
title: "Simple Fixes to the IP Flow Information Export (IPFIX) IANA Registry"
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
     IANA-IPFIX:
        title: IP Flow Information Export (IPFIX) Entities
        target: https://www.iana.org/assignments/ipfix/ipfix.xhtml
        date: 2022-11
     IPv6-EH:
        title: Internet Protocol Version 6 (IPv6) Parameters, IPv6 Extension Header Types
        target: https://www.iana.org/assignments/ipv6-parameters/ipv6-parameters.xhtml#ipv6-parameters-1
        date: 2022-11
        

informative:


--- abstract

This document describes simple fixes to the IANA IP Flow Information Export (IPFIX) registry. These fixes are mainly updates to point to newer IANA registries and also updates to the description of some Information Elements (IEs).


--- middle

# Introduction

As the OPSAWG is currently considering {{?I-D.boucadair-opsawg-rfc7125-update}} that updates {{?RFC7125}}, the WG realized that some other parts of the IANA IPFIX registry {{IANA-IPFIX}} were not up to date. Indeed, since its initial creation in 2007, some IPFIX Information Elements (IEs) are not adequately specified any longer (while they were at some point in time in the past). This document intends to update the registry and bringing some consistency.

This document lists a set of simple fixes to the IPFIX IANA registry {{IANA-IPFIX}}. These fixes are classified as follows:

- Updates that fix a shortcoming in the description of an IE ({{desc}}).
- Updates that require adding a pointer to an existing IANA registry ({{to-iana}}).
- Updates that are meant to ensure a consistent structure when calling an existing IANA registry ({{consistent}}).

Note that, as per {{Section 5 of RFC7012}}, {{IANA-IPFIX}} is the normative reference for the IPFIX IEs that were defined in {{?RFC5102}}. Therefore, the updates in this document do not update any part of {{!RFC7125}}.

Fixes that require defining new IEs may be moved to a separate document.

# Conventions and Definitions

{::boilerplate bcp14-tagged}


# Update the Description {#desc}

The IEs listed in the following subsections cannot echo some values that can be seen in a packet.

## tcpOptions

Only options having a kind =< 56 can be included in a tcpOptions IE. An update is required to specify how any observed TCP option in a packet can be exported using IPFIX.

## ipv6ExtensionHeaders

The description should be updated to:
- reflect missing IPv6 EHs, specifically 139, 140, 253, and 254.
- specify how to automatically update the registry when a new value is assigned in {{IPv6-EH}}.
- specify the procedure to follow when all bits are exhausted.


# Point to An Existing IANA Registry {#to-iana}

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

# Consistent Citation of Registries {#consistent}

IANA is requested to update {{IANA-IPFIX}} for each of the IE entries listed in the following subsections.

## flowEndReason

* OLD:
   - Description: The reason for Flow termination. Values are listed in the flowEndReason registry. See https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-flow-end-reason.
   - Additional Information:
* NEW:
   - Description: The reason for Flow termination. Values are listed in the flowEndReason registry.
   - Additional Information: See https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-flow-end-reason.


## natOriginatingAddressRealm

* OLD:
   - Description: Indicates whether the session was created because traffic originated in the private or public address realm. postNATSourceIPv4Address, postNATDestinationIPv4Address, postNAPTSourceTransportPort, and postNAPTDestinationTransportPort are qualified with the address realm in perspective. Values are listed in the natOriginatingAddressRealm registry. See https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-nat-originating-address-realm.
   - Additional Information: See {{?RFC3022}} for the definition of NAT.
* NEW:
   - Description:  Indicates whether the session was created because traffic originated in the private or public address realm. postNATSourceIPv4Address, postNATDestinationIPv4Address, postNAPTSourceTransportPort, and postNAPTDestinationTransportPort are qualified with the address realm in perspective. Values are listed in the natOriginatingAddressRealm registry.
   - Additional Information: See https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-nat-originating-address-realm. See {{?RFC3022}} for the definition of NAT.

## natEvent

* OLD:
   - Description: This Information Element identifies a NAT event. This IE identifies the type of a NAT event. Examples of NAT events include, but are not limited to, NAT translation create, NAT translation delete, Threshold Reached, or Threshold Exceeded, etc. Values for this Information Element are listed in the "NAT Event Type" registry, see https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-nat-event-type.
   - Additional Information: See {{?RFC3022}} for the definition of NAT. See {{?RFC3234}} for the definition of middleboxes. See {{?RFC8158}} for the definitions of values 4-16.
* NEW:
   - Description: This Information Element identifies a NAT event. This IE identifies the type of a NAT event. Examples of NAT events include, but are not limited to, NAT translation create, NAT translation delete, Threshold Reached, or Threshold Exceeded, etc. Values for this Information Element are listed in the "NAT Event Type" registry.
   - Additional Information: See https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-nat-event-type. See {{?RFC3022}} for the definition of NAT. See {{?RFC3234}} for the definition of middleboxes. See {{?RFC8158}} for the definitions of values 4-16.

## firewallEvent

* OLD:
   - Description: Indicates a firewall event. Allowed values are listed in the firewallEvent registry. See https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-firewall-event.
   - Additional Information:
* NEW:
   - Description: Indicates a firewall event. Allowed values are listed in the firewallEvent registry.
   - Additional Information: See https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-firewall-event.

## biflowDirection

* OLD:
   - Description:  A description of the direction assignment method used to assign the Biflow Source and Destination. This Information Element MAY be present in a Flow Data Record, or applied to all flows exported from an Exporting Process or Observation Domain using IPFIX Options. If this Information Element is not present in a Flow Record or associated with a Biflow via scope, it is assumed that the configuration of the direction assignment method is done out-of-band. Note that when using IPFIX Options to apply this Information Element to all flows within an Observation Domain or from an Exporting Process, the Option SHOULD be sent reliably. If reliable transport is not available (i.e., when using UDP), this Information Element SHOULD appear in each Flow Record. Values are listed in the biflowDirection registry. See [https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-biflow-direction].
   - Additional Information:
* NEW:
   - Description: A description of the direction assignment method used to assign the Biflow Source and Destination. This Information Element MAY be present in a Flow Data Record, or applied to all flows exported from an Exporting Process or Observation Domain using IPFIX Options. If this Information Element is not present in a Flow Record or associated with a Biflow via scope, it is assumed that the configuration of the direction assignment method is done out-of-band. Note that when using IPFIX Options to apply this Information Element to all flows within an Observation Domain or from an Exporting Process, the Option SHOULD be sent reliably. If reliable transport is not available (i.e., when using UDP), this Information Element SHOULD appear in each Flow Record. Values are listed in the biflowDirection registry.
   - Additional Information: See https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-biflow-direction.


## observationPointType

* OLD:
   - Description: Type of observation point. Values are listed in the observationPointType registry. See https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-observation-point-type.
   - Additional Information:
* NEW:
   - Description: Type of observation point. Values are listed in the observationPointType registry.
   - Additional Information: See https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-observation-point-type.

## anonymizationTechnique

* OLD:
   - Description: A description of the anonymization technique applied to a referenced Information Element within a referenced Template. Each technique may be applicable only to certain Information Elements and recommended only for certain Information Elements. Values are listed in the anonymizationTechnique registry. See https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-anonymization-technique.
   - Additional Information:
* NEW:
   - Description: A description of the anonymization technique applied to a referenced Information Element within a referenced Template. Each technique may be applicable only to certain Information Elements and recommended only for certain Information Elements. Values are listed in the anonymizationTechnique registry.
   - Additional Information: See https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-anonymization-technique.

## natType

* OLD:
   - Description: Values are listed in the natType registry. See https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-nat-type.
   - Additional Information: See {{?RFC3022}} for the definition of NAT. See {{?RFC1631}} for the definition of NAT44. See {{?RFC6144}} for the definition of NAT64. See {{?RFC6146}} for the definition of NAT46. See {{?RFC6296}} for the definition of NAT66. See {{?RFC0791}} for the definition of IPv4. See {{?RFC8200}} for the definition of IPv6.
* NEW:
   - Description: Values are listed in the natType registry.
   - Additional Information: See https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-nat-type. See {{?RFC3022}} for the definition of NAT. See {{?RFC1631}} for the definition of NAT44. See {{?RFC6144}} for the definition of NAT64. See {{?RFC6146}} for the definition of NAT46. See {{?RFC6296}} for the definition of NAT66. See {{?RFC0791}} for the definition of IPv4. See {{?RFC8200}} for the definition of IPv6.


## selectorAlgorithm

* OLD:
   - Description: This Information Element identifies the packet selection methods (e.g., Filtering, Sampling) that are applied by the Selection Process. Most of these methods have parameters. Further Information Elements are needed to fully specify packet selection with these methods and all their parameters. The methods listed below are defined in {{?RFC5475}}. For their parameters, Information Elements are defined in the information model document. The names of these Information Elements are listed for each method identifier. Further method identifiers may be added to the list below. It might be necessary to define new Information Elements to specify their parameters. The following packet selection methods identifiers are defined here: https://www.iana.org/assignments/psamp-parameters. There is a broad variety of possible parameters that could be used for Property match Filtering (5) but currently there are no agreed parameters specified.
   - Additional Information:
* NEW:
   - Description: This Information Element identifies the packet selection methods (e.g., Filtering, Sampling) that are applied by the Selection Process. Most of these methods have parameters. Further Information Elements are needed to fully specify packet selection with these methods and all their parameters. The methods listed below are defined in {{?RFC5475}}. For their parameters, Information Elements are defined in the information model document. The names of these Information Elements are listed for each method identifier. Further method identifiers may be added to the list. It might be necessary to define new Information Elements to specify their parameters. There is a broad variety of possible parameters that could be used for Property match Filtering (5) but currently there are no agreed parameters specified.
   - Additional Information: See https://www.iana.org/assignments/psamp-parameters

## informationElementDataType

* OLD:
   - Description: A description of the abstract data type of an IPFIX information element.These are taken from the abstract data types defined in section 3.1 of the IPFIX Information Model {{?RFC5102}}; see that section for more information on the types described in the [informationElementDataType] subregistry. These types are registered in the IANA IPFIX Information Element Data Type subregistry. This subregistry is intended to assign numbers for type names, not to provide a mechanism for adding data types to the IPFIX Protocol, and as such requires a Standards Action {{?RFC8126}} to modify.
   - Additional Information:
* NEW:
   - Description: A description of the abstract data type of an IPFIX information element.These are taken from the abstract data types defined in section 3.1 of the IPFIX Information Model {{?RFC5102}}; see that section for more information on the types described in the [informationElementDataType] subregistry. These types are registered in the IANA IPFIX Information Element Data Type subregistry. This subregistry is intended to assign numbers for type names, not to provide a mechanism for adding data types to the IPFIX Protocol, and as such requires a Standards Action {{?RFC8126}} to modify.
   - Additional Information: See https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-information-element-data-types

## informationElementSemantics

* OLD:
   - Description: A description of the semantics of an IPFIX Information Element. These are taken from the data type semantics defined in section 3.2 of the IPFIX Information Model {{?RFC5102}}; see that section for more information on the types defined in the [IPFIX Information Element Semantics] subregistry. This field may take the values in the semantics registry; the special value 0x00 (default) is used to note that no semantics apply to the field; it cannot be manipulated by a Collecting Process or File Reader that does not understand it a priori. These semantics are registered in the IANA IPFIX Information Element Semantics subregistry. This subregistry is intended to assign numbers for semantics names, not to provide a mechanism for adding semantics to the IPFIX Protocol, and as such requires a Standards Action {{?RFC8126}} to modify.
   - Additional Information:
* NEW:
   - Description: A description of the semantics of an IPFIX Information Element. These are taken from the data type semantics defined in section 3.2 of the IPFIX Information Model {{?RFC5102}}; see that section for more information on the types defined in the [IPFIX Information Element Semantics] subregistry. This field may take the values in the semantics registry; the special value 0x00 (default) is used to note that no semantics apply to the field; it cannot be manipulated by a Collecting Process or File Reader that does not understand it a priori. These semantics are registered in the IANA IPFIX Information Element Semantics subregistry. This subregistry is intended to assign numbers for semantics names, not to provide a mechanism for adding semantics to the IPFIX Protocol, and as such requires a Standards Action {{?RFC8126}} to modify.
   - Additional Information: See https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-information-element-semantic

## informationElementUnits

* OLD:
   - Description: A description of the units of an IPFIX Information Element. These correspond to the units implicitly defined in the Information Element definitions in section 5 of the IPFIX Information Model {{?RFC5102}}; see that section for more information on the types described in the informationElementsUnits subregistry. This field may take the values in Table 3 below; the special value 0x00 (none) is used to note that the field is unitless. These types are registered in the [IANA IPFIX Information Element Units] subregistry.
   - Additional Information:
* NEW:
   - Description: A description of the units of an IPFIX Information Element. These correspond to the units implicitly defined in the Information Element definitions in section 5 of the IPFIX Information Model {{?RFC5102}}; see that section for more information on the types described in the informationElementsUnits subregistry. This field may take the values in Table 3 below; the special value 0x00 (none) is used to note that the field is unitless. These types are registered in the [IANA IPFIX Information Element Units] subregistry.
   - Additional Information: See https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-information-element-units


## portRangeStart

* OLD:
   - Description: The port number identifying the start of a range of ports. A value of zero indicates that the range start is not specified, ie the range is defined in some other way. Additional information on defined TCP port numbers can be found at https://www.iana.org/assignments/service-names-port-numbers.
   - Additional Information:
* NEW:
   - Description: The port number identifying the start of a range of ports. A value of zero indicates that the range start is not specified, i.e., the range is defined in some other way.
   - Additional Information: Additional information on defined TCP port numbers can be found at https://www.iana.org/assignments/service-names-port-numbers.

## portRangeEnd

* OLD:
   - Description: The port number identifying the end of a range of ports. A value of zero indicates that the range end is not specified, ie the range is defined in some other way. Additional information on defined TCP port numbers can be found at https://www.iana.org/assignments/service-names-port-numbers.
   - Additional Information:
* NEW:
   - Description: The port number identifying the end of a range of ports. A value of zero indicates that the range end is not specified, i.e., the range is defined in some other way.
   - Additional Information: Additional information on defined TCP port numbers can be found at https://www.iana.org/assignments/service-names-port-numbers.

## ingressInterfaceType

* OLD:
   - Description: The type of interface where packets of this Flow are being received. The value matches the value of managed object 'ifType' as defined in https://www.iana.org/assignments/ianaiftype-mib.
   - Additional Information: https://www.iana.org/assignments/ianaiftype-mib
* NEW:
   - Description: The type of interface where packets of this Flow are being received. The value matches the value of managed object 'ifType'.
   - Additional Information: See https://www.iana.org/assignments/ianaiftype-mib

## egressInterfaceType

* OLD:
   - Description: The type of interface where packets of this Flow are being sent. The value matches the value of managed object 'ifType' as defined in https://www.iana.org/assignments/ianaiftype-mib.
   - Additional Information: https://www.iana.org/assignments/ianaiftype-mib
* NEW:
   - Description: The type of interface where packets of this Flow are being sent. The value matches the value of managed object 'ifType'.
   - Additional Information: See https://www.iana.org/assignments/ianaiftype-mib


## valueDistributionMethod

* OLD:
   - Description: A description of the method used to distribute the counters from Contributing Flows into the Aggregated Flow records described by an associated scope, generally a Template. The method is deemed to apply to all the non-key Information Elements in the referenced scope for which value distribution is a valid operation; if the originalFlowsInitiated and/or originalFlowsCompleted Information Elements appear in the Template, they are not subject to this distribution method, as they each infer their own distribution method. The valueDistributionMethod registry is intended to list a complete set of possible value distribution methods. See https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-value-distribution-method.
   - Additional Information:
* NEW:
   - Description: A description of the method used to distribute the counters from Contributing Flows into the Aggregated Flow records described by an associated scope, generally a Template. The method is deemed to apply to all the non-key Information Elements in the referenced scope for which value distribution is a valid operation; if the originalFlowsInitiated and/or originalFlowsCompleted Information Elements appear in the Template, they are not subject to this distribution method, as they each infer their own distribution method. The valueDistributionMethod registry is intended to list a complete set of possible value distribution methods.
   - Additional Information: See https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-value-distribution-method.

## flowSelectorAlgorithm

* OLD:
   - Description: This Information Element identifies the Intermediate Flow Selection Process technique (e.g., Filtering, Sampling) that is applied by the Intermediate Flow Selection Process. Most of these techniques have parameters. Its configuration parameter(s) MUST be clearly specified. Further Information Elements are needed to fully specify packet selection with these methods and all their parameters. Further method identifiers may be added to the flowSelectorAlgorithm registry. It might be necessary to define new Information Elements to specify their parameters. Please note that the purpose of the flow selection techniques described in this document is the improvement of measurement functions as defined in the Scope (Section 1). The Intermediate Flow Selection Process Techniques identifiers are defined at https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-flowselectoralgorithm.
   - Additional Information:
* NEW:
   - Description: This Information Element identifies the Intermediate Flow Selection Process technique (e.g., Filtering, Sampling) that is applied by the Intermediate Flow Selection Process. Most of these techniques have parameters. Its configuration parameter(s) MUST be clearly specified. Further Information Elements are needed to fully specify packet selection with these methods and all their parameters. Further method identifiers may be added to the flowSelectorAlgorithm registry. It might be necessary to define new Information Elements to specify their parameters.
   - Additional Information: See https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-flowselectoralgorithm.

## dataLinkFrameType

* OLD:
   - Description: This Information Element specifies the type of the selected data link frame. Data link types are defined in the dataLinkFrameType registry. See https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-data-link-frame-type. Further values may be assigned by IANA. Note that the assigned values are bits so that multiple observations can be OR'd together. The data link layer is defined in [ISO/IEC.7498-1:1994].
   - Additional Information: [IEEE802.3][IEEE802.11][ISO/IEC.7498-1:1994]
* NEW:
   - Description: This Information Element specifies the type of the selected data link frame. Data link types are defined in the dataLinkFrameType registry. Further values may be assigned by IANA. Note that the assigned values are bits so that multiple observations can be OR'd together. The data link layer is defined in [ISO/IEC.7498-1:1994].
   - Additional Information: See https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-data-link-frame-type. [IEEE802.3][IEEE802.11][ISO/IEC.7498-1:1994]

## mibCaptureTimeSemantics

* OLD:
   - Description: Indicates when in the lifetime of the Flow the MIB value was retrieved from the MIB for a mibObjectIdentifier. This is used to indicate if the value exported was collected from the MIB closer to Flow creation or Flow export time and refers to the Timestamp fields included in the same Data Record. This field SHOULD be used when exporting a mibObjectValue that specifies counters or statistics. If the MIB value was sampled by SNMP prior to the IPFIX Metering Process or Exporting Process retrieving the value (i.e., the data is already stale) and it is important to know the exact sampling time, then an additional observationTime* element should be paired with the OID using IPFIX Structured Data {{?RFC6313}}. Similarly, if different MIB capture times apply to different mibObjectValue elements within the Data Record, then individual mibCaptureTimeSemantics Information Elements should be paired with each OID using IPFIX Structured Data. Values are listed in the mibCaptureTimeSemantics registry. See https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-mib-capture-time-semantics.
   - Additional Information:
* NEW:
   - Description: Indicates when in the lifetime of the Flow the MIB value was retrieved from the MIB for a mibObjectIdentifier. This is used to indicate if the value exported was collected from the MIB closer to Flow creation or Flow export time and refers to the Timestamp fields included in the same Data Record. This field SHOULD be used when exporting a mibObjectValue that specifies counters or statistics. If the MIB value was sampled by SNMP prior to the IPFIX Metering Process or Exporting Process retrieving the value (i.e., the data is already stale) and it is important to know the exact sampling time, then an additional observationTime* element should be paired with the OID using IPFIX Structured Data {{?RFC6313}}. Similarly, if different MIB capture times apply to different mibObjectValue elements within the Data Record, then individual mibCaptureTimeSemantics Information Elements should be paired with each OID using IPFIX Structured Data. Values are listed in the mibCaptureTimeSemantics registry.
   - Additional Information: See https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-mib-capture-time-semantics

## natQuotaExceededEvent

* OLD:
   - Description: This Information Element identifies the type of a NAT Quota Exceeded event. Values for this Information Element are listed in the "NAT Quota Exceeded Event Type" registry, see https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-nat-quota-exceeded-event.
   - Additional Information: See {{?RFC0791}} for the definition of the IPv4 source address field. See {{?RFC3022}} for the definition of NAT. See {{?RFC3234}} for the definition of middleboxes.
* NEW:
   - Description: This Information Element identifies the type of a NAT Quota Exceeded event. Values for this Information Element are listed in the "NAT Quota Exceeded Event Type" registry.
   - Additional Information: See https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-nat-quota-exceeded-event. See {{?RFC0791}} for the definition of the IPv4 source address field. See {{?RFC3022}} for the definition of NAT. See {{?RFC3234}} for the definition of middleboxes.

## natThresholdEvent

* OLD:
   - Description: This Information Element identifies a type of a NAT Threshold event. Values for this Information Element are listed in the "NAT Threshold Event Type" registry, see https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-nat-threshold-event.
   - Additional Information: See {{?RFC0791}} for the definition of the IPv4 source address field. See {{?RFC3022}} for the definition of NAT. See {{?RFC3234}} for the definition of middleboxes.
* NEW:
   - Description: This Information Element identifies a type of a NAT Threshold event. Values for this Information Element are listed in the "NAT Threshold Event Type" registry.
   - Additional Information: See https://www.iana.org/assignments/ipfix/ipfix.xhtml#ipfix-nat-threshold-event. See {{?RFC0791}} for the definition of the IPv4 source address field. See {{?RFC3022}} for the definition of NAT. See {{?RFC3234}} for the definition of middleboxes.


# Security Considerations

IPFIX security considerations are discussed in {{Section 8 of !RFC7012}}.


# IANA Considerations

Requested IANA actions are described in the main document. These actions are not repeated here.


--- back

# Acknowledgments
{:numbered="false"}

TODO acknowledge.

