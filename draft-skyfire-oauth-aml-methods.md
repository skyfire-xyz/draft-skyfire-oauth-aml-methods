---
title: "Anti-Money Laundering Methods Values"
#abbrev: ""
category: std

docname: draft-skyfire-oauth-aml-methods-latest
submissiontype: IETF  # also: "independent", "editorial", "IAB", or "IRTF"
#number:
date:
consensus: true
v: 3
area: "Security"
workgroup: "Web Authorization Protocol"
keyword:
 - agent
 - agentic
 - payment
 - commerce
 - compliance
 - regulation
 - Anti-Money Laundering
 - AML
 - Countering the Financing of Terrorism
 - CFT
venue:
  github: "skyfire-xyz/draft-skyfire-oauth-aml-methods"
  group: "Web Authorization Protocol"
  type: "Working Group"
  mail: "oauth@ietf.org"
  arch: "https://mailarchive.ietf.org/arch/browse/oauth/"
  latest: "https://skyfire-xyz.github.io/draft-skyfire-oauth-aml-methods/draft-skyfire-oauth-aml-methods.html"

author:
-
  name: Ankit Agarwal
  organization: Skyfire Systems Inc.
  email: ankit_agarwal@yahoo.com
  uri: https://skyfire.xyz
-
  ins: M. Jones
  name: Michael B. Jones
  organization: Self-Issued Consulting
  email: michael_b_jones@hotmail.com
  uri: https://self-issued.info/
-
  name: Nash Ali
  organization: Experian
  email: nash.ali@experian.com

normative:
  RFC7519:
  OFAC:
    target: https://ofac.treasury.gov/faqs/topic/1596
    title: "Starting an OFAC Compliance Program"
    date: January 30, 2015
    author:
      - org: Office of Foreign Assets Control, U.S. Department of the Treasury
  Sanctions:
    target: https://www.swift.com/risk-and-compliance/sanctions/why-sanctions-screening-critical-financial-institutions
    title: "Why sanctions screening is critical for financial institutions"
    author:
      - org: Swift
    date: false
  Watchlist:
    target: https://withpersona.com/blog/what-is-watchlist-screening/
    title: "What is watchlist screening? A complete guide"
    date: January 12, 2026
    author:
      - org: persona
  PEPs:
    target: https://www.moodys.com/web/en/us/kyc/solutions/screen-monitor/peps.html
    title: "Identifying Politically Exposed Persons (PEPs) and their associates"
    author:
      - org: Moody's
    date: false
  AdverseMedia:
    target: https://legal.thomsonreuters.com/blog/overview-adverse-media-screening/
    title: "Adverse media screening: An overview"
    date: May 8, 2025
    author:
      - org: Thomson Reuters

informative:
  RFC5226:
  I-D.skyfire-oauth-kyapay-token:
  OpenID.Core:
    target: https://openid.net/specs/openid-connect-core-1_0.html
    title: "OpenID Connect Core 1.0 incorporating errata set 2"
    date: 2023-12-15
    author:
      - name: Nat Sakimura
      - name: John Bradley
      - name: Michael B. Jones
      - name: Breno de Medeiros
      - name: Chuck Mortimore
  IANA.JWT.Claims:
    author:
    - org: IANA
    target: https://www.iana.org/assignments/jwt
    title: JSON Web Token Claims
    date: false
  IANA.AMR:
    author:
    - org: IANA
    target: https://www.iana.org/assignments/authentication-method-reference-values
    title: Authentication Method Reference Values
    date: false

...

--- abstract

Financial regulations require application of Anti-Money Laundering (AML) and
Countering the Financing of Terrorism (CFT) methods in many jurisdictions worldwide.
This specification defines a claim and values for declaring what AML/CFT
methods were employed.

--- middle

# Introduction

Compliance to Anti-Money Laundering (AML) and
Countering the Financing of Terrorism (CFT) regulations
is required in many jurisdictions worldwide.
This specification defines the Anti-Money Laundering Methods (aml) claim
and values for it for declaring what Anti-Money Laundering (AML) and
Countering the Financing of Terrorism (CFT) methods were employed.
It also creates a registry for Anti-Money Laundering Methods Values
and initializes the registry with the values defined in this specification.

While this claim and values are general purpose
and can be used in any JSON Web Token (JWT) {{RFC7519}},
one use case for them is use in KYAPay tokens {{I-D.skyfire-oauth-kyapay-token}}.


# Conventions and Definitions

{::boilerplate bcp14-tagged}


# Anti-Money Laundering Methods {#aml}

This section defines the "aml" (Anti-Money Laundering Methods) claim and
values used with it to indicate that particular
Anti-Money Laundering/Countering the Financing of Terrorism
methods were used.
In many ways, this parallels the "amr" (Authentication Methods References) claim
defined in {{OpenID.Core}}.
Like "amr", "aml" is a JWT claim whose value is
an array that lists a set of methods that were used,
in this case, as anti-money laundering methods,
rather than authentication method references.

## "aml" (Anti-Money Laundering Methods) Claim {#amlClaim}

The "aml" (Anti-Money Laundering Methods) claim is a
JSON array of case-sensitive strings that are identifiers for
anti-money laundering methods used.
For instance, values might indicate that both
sanctions screening and watchlist screening methods were used.
Values used in the "aml" claim SHOULD be from those registered in the
IANA "Anti-Money Laundering Methods" registry
established by {{amlRegistry}};
parties using this claim will need to agree upon the meanings of
any unregistered values used, which may be context specific.

## Anti-Money Laundering Method Values {#amlValues}

The following Anti-Money Laundering Method values
are defined by this specification.

### "ofac" (OFAC Compliance) Method {#ofacMethod}

ofac:
: OFAC Compliance, as described in {{OFAC}}

### "sanc" (Sanctions Screening) Method {#sancMethod}

sanc:
: Sanctions Screening, as described in {{Sanctions}}

### "watch" (Watchlist Screening) Method {#watchMethod}

watch:
: Watchlist Screening, as described in {{Watchlist}}

### "pep" (Politically Exposed Persons Screening) Method {#pepMethod}

pep:
: Politically Exposed Persons Screening, as described in {{PEPs}}

### "adv" (Adverse Media Screening) Method {#advMethod}

adv:
: Adverse Media Screening, as described in {{AdverseMedia}}


# Security Considerations

The security considerations defined in
JSON Web Token (JWT) {{RFC7519}}
apply to this specification.


# Privacy Considerations

The privacy considerations defined in
JSON Web Token (JWT) {{RFC7519}}
apply to this specification.


# IANA Considerations

## JSON Web Token Claims Registration

This specification registers the following Claim in the
IANA "JSON Web Token Claims" {{IANA.JWT.Claims}}
established by {{RFC7519}}.

### "aml" Claim

* Claim Name: aml
* Claim Description: Anti-Money Laundering Methods
* Change Controller: Michael B. Jones - michael_b_jones@hotmail.com
* Reference: {{amlClaim}} of this specification

## Anti-Money Laundering Methods Registry {#amlRegistry}

This specification establishes the IANA "Anti-Money Laundering Methods" registry
for `aml` claim array element values.
The registry records the Anti-Money Laundering Method value
and a reference to the specification that defines it.
This specification registers the Anti-Money Laundering Method values
defined in {{amlValues}}.

Values are registered on an Expert Review
{{RFC5226}} basis after a three-week review period on the &lt;jwt-reg-review@ietf.org&gt; mailing
list, on the advice of one or more Designated Experts.
To increase potential interoperability, the Designated Experts are requested to encourage
registrants to provide the location of a publicly accessible specification
defining the values being registered,
so that their intended usage can be more easily  understood.

Registration requests sent to the mailing list for review should use
an appropriate subject
(e.g., "Request to register Anti-Money Laundering Method value: example").

Within the review period, the Designated Experts will either approve or
deny the registration request, communicating this decision to the review list and IANA.
Denials should include an explanation and, if applicable, suggestions as to how to make
the request successful.
Registration requests that are undetermined for
a period longer than 21 days can be brought to the IESG's attention
(using the <iesg@ietf.org> mailing list) for resolution.

IANA must only accept registry updates from the Designated Experts and should direct
all requests for registration to the review mailing list.

It is suggested that the same Designated Experts evaluate these
registration requests as those who evaluate registration requests
for the IANA "Authentication Method Reference Values" registry {{IANA.AMR}}.

Criteria that should be applied by the Designated Experts include
determining whether the proposed registration duplicates existing functionality;
whether it is likely to be of general applicability
or whether it is useful only for a single application;
whether the value is actually being used;
and whether the registration description is clear.

### Registration Template

Anti-Money Laundering Method Name:
: The name requested (e.g., "sanc") for the authentication method
  or family of closely related authentication methods.
  Because a core goal of this specification is for the resulting
  representations to be compact, it is RECOMMENDED that the name be short
  -- that is, not to exceed 8 characters without a compelling reason to do so.
  To facilitate interoperability, the name must use only
  printable ASCII characters excluding double quote ('"') and backslash ('\\')
  (the Unicode characters with code points U+0021, U+0023 through U+005B, and
  U+005D through U+007E).
  This name is case sensitive.
  Names may not match other registered names in a case-insensitive manner
  unless the Designated Experts state that there is a compelling reason
  to allow an exception.

Anti-Money Laundering Method Description:
: Brief description of the Anti-Money Laundering Method
  (e.g., "Watchlist Screening").

Change Controller:
: For Standards Track RFCs, state "IETF". For others, give the name of the
  responsible party. Other details (e.g., postal address, email address, home page
  URI) may also be included.

Specification Document(s):
: Reference to the document or documents that specify the parameter,
  preferably including URIs that
  can be used to retrieve copies of the documents.
  An indication of the relevant
  sections may also be included but is not required.


### Initial Registry Contents

#### "ofac" Method

* Anti-Money Laundering Method Name: ofac
* Anti-Money Laundering Method Description: OFAC Compliance
* Change Controller: IETF
* Reference: {{ofacMethod}} of this specification

#### "sanc" Method

* Anti-Money Laundering Method Name: sanc
* Anti-Money Laundering Method Description: Sanctions Screening
* Change Controller: IETF
* Reference: {{sancMethod}} of this specification

#### "watch" Method

* Anti-Money Laundering Method Name: watch
* Anti-Money Laundering Method Description: Watchlist Screening
* Change Controller: IETF
* Reference: {{watchMethod}} of this specification

#### "pep" Method

* Anti-Money Laundering Method Name: pep
* Anti-Money Laundering Method Description: Politically Exposed Persons Screening
* Change Controller: IETF
* Reference: {{pepMethod}} of this specification

#### "adv" Method

* Anti-Money Laundering Method Name: adv
* Anti-Money Laundering Method Description: Adverse Media Screening
* Change Controller: IETF
* Reference: {{advMethod}} of this specification


--- back

# Document History
{: numbered="false"}

[[ to be removed by the RFC Editor before publication as an RFC ]]

-00

* Initial draft.
