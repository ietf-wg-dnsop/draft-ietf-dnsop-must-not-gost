---
title: "Deprecate usage of ECC-GOST within DNSSEC"
abbrev: MUST NOT DNSSEC with ECC-GOST
docname: draft-ietf-dnsop-must-not-ecc-gost-07
category: std
ipr: trust200902
stream: IETF


stand_alone: yes
pi: [toc, sortrefs, symrefs, docmapping]

author:
  -
    ins: W. Hardaker
    name: Wes Hardaker
    org: USC/ISI
    email: ietf@hardakers.net
  -
    ins: W. Kumari
    name: Warren Kumari
    org: Google
    email: warren@kumari.net

normative:
  RFC2119:
  RFC5933:
  RFC9364:

  DNSKEY-IANA:
    author:
      name: IANA
    target: "https://www.iana.org/assignments/dns-sec-alg-numbers/dns-sec-alg-numbers.xhtml"
    title: Domain Name System Security (DNSSEC) Algorithm Numbers
  DS-IANA:
    author:
      name: IANA
    target: "http://www.iana.org/assignments/ds-rr-types"
    title: Delegation Signer (DS) Resource Record (RR) Type Digest Algorithms

  draft-ietf-dnsop-rfc8624-bis:
    author: 
      name: Hardaker, W.
      name: Kumari, W.
    target: https://datatracker.ietf.org/doc/html/draft-ietf-dnsop-rfc8624-bis
    title: DNS Security Algorithm Numbers
    

informative:
  RFC9558:


--- abstract

This document retires the use of GOST R 34.10-2001 (mnemonic
"ECC-GOST") within DNSSEC.

RFC5933 (now historic) defined the use of GOST R 34.10-2001 and GOST R 34.11-94
algorithms with DNS Security Extensions (DNSSEC). This document updates RFC5933
by deprecating the use of ECC-GOST.

--- middle

# Introduction

The use of the GOST R 34.10-2001 and GOST R 34.11-94 algorithms with
the DNS Security Extensions (DNSSEC) [RFC9364] was documented in
{{RFC5933}}. These two algorithms were deprecated by the Orders of the
Federal Agency for Technical Regulation and Metrology of Russia
(Rosstandart) in August 2012, and were superseded by GOST 34.10-2012
and GOST 34.11-2012 respectively. The use of these newer two
algorithms in DNSSEC is documented in {{RFC9558}} and their associated
requirement levels are not changed by this document.

Thus, the use of GOST R 34.10-2001 (mnemonic GOST-ECC) and GOST R 34.11-94
is no longer recommended for use in DNSSEC {{RFC9364}}.


## Requirements notation

   The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT",
   "SHOULD", "SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED", "MAY",
   and "OPTIONAL" in this document are to be interpreted as described
   in BCP 14 {{RFC2119}} {{?RFC8174}} when, and only when, they appear
   in all capitals, as shown here.

# Deprecating ECC-GOST algorithms in DNSSEC

The GOST R 34.11-94 {{RFC5933}} algorithm MUST NOT be used when
creating DS records.  Validating resolvers MUST treat GOST R 34.11-94
DS records as insecure.  If no other DS records of accepted
cryptographic algorithms are available, the DNS records below the
delegation point MUST be treated as insecure.

The ECC-GOST {{RFC5933}} algorithm MUST NOT be used when creating
DNSKEY and RRSIG records.  Validating resolvers MUST treat
RRSIG records created from DNSKEY records using these algorithms as an
unsupported algorithm. If no other RRSIG records of accepted cryptographic
algorithms are available, the validating resolver MUST consider the
associated resource records as insecure.

# Security Considerations

This document potentially increases the security of the DNSSEC ecosystem by
deprecating algorithms that are no longer recommended for use.

# Operational Considerations

This document removes support for ECC-GOST. Zone operators currently making use
of ECC-GOST based algorithms should switch to algorithms that remain supported.
DNS registries should prohibit their clients from uploading and publishing
ECC-GOST based DS records to ensure that they are using algorithms which are
supported by DNSSEC validators, and so can be DNSSEC validated.

# IANA Considerations

[Note to IANA, to be removed by the RFC Editor: the registry fields
listed above will be created by draft-ietf-dnsop-rfc8624-bis.]

IANA is requested to set the "Use for DNSSEC Signing", "Use for DNSSEC
Validation", "Implement for DNSSEC Signing", and "Implement for DNSSEC
Validation" columns of the DNS Security Algorithm Numbers registry
{{DNSKEY-IANA}} {{draft-ietf-dnsop-rfc8624-bis}} for ECC-GOST (12) 
to MUST NOT.  Note that previously
the "Use for DNSSEC Signing" and "Implement for DNSSEC Delegation"
columns were already MUST NOT.

IANA is requested to set the "Use for DNSSEC Delegation", "Use for DNSSEC
Validation", "Implement for DNSSEC Delegation", and "Implement for DNSSEC
Validation" columns of the "Digest Algorithms" registry {{DS-IANA}}
for GOST R 34.11-94 (3) to MUST NOT.  Note that previously
the "Use for DNSSEC Signing" and "Implement for DNSSEC Delegation"
columns were already MUST NOT.

--- back

# Acknowledgments

The authors appreciate the comments and suggestions from the following IETF
participants in helping produce this document: Mark Andrews, Steve Crocker,
Brian Dickson, Thomas Graf, Russ Housely, Shumon Huque, Paul Hoffman, S Moonesamy, Peter
Dickson, Peter Thomassen, Stefan Ubbink, Paul Wouters, Tim Wicinski,  and the
many members of the DNSOP working group that discussed this draft.

# Current algorithm usage levels

The DNSSEC scanning project by Viktor Dukhovni and Wes Hardaker
highlights the current deployment of various algorithms on the
https://stats.dnssec-tools.org/ website.

<RFC Editor: please delete this section upon publication>

# Github Version of this document

While this document is under development, it can be viewed, tracked,
fill here:

https://github.com/hardaker/draft-hardaker-dnsop-must-not-gost

<RFC Editor: please delete this section upon publication>
