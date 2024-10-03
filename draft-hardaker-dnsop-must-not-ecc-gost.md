---
title: "Remove ECC-GOST from active use within DNSSEC"
abbrev: MUST NOT DNSSEC with ECC-GOST
docname: draft-hardaker-dnsop-must-not-ecc-gost-00
category: std
ipr: trust200902

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
  RFC4033:
  RFC4034:
  RFC4035:
  RFC5933:
  RFC8080:
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

informative:
  RFC8499:


--- abstract

This document retires the use of ECC-GOST within DNSSEC.

--- middle

# Introduction

The security of the ECC-GOST algorithm {{RFC5933}} has been slowly
diminishing over time as various forms of attacks have weakened its
cryptographic underpinning.  Thus, the use of ECC-GOST is no longer
needed and is not recommend for use in DNSSEC {{RFC4033}} {{RFC4034}}
{{RFC4035}}.

This document retires the use of ECC-GOST within DNSSEC.

## Requirements notation

   The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT",
   "SHOULD", "SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED", "MAY",
   and "OPTIONAL" in this document are to be interpreted as described
   in BCP 14 {{RFC2119}} {{?RFC8174}} when, and only when, they appear
   in all capitals, as shown here.

# Deprecating ECC-GOST algorithms in DNSSEC

The ECC-GOST {{RFC5933}} algorithm MUST NOT be used when creating DS
records.  Validating resolvers MUST treat DS records as insecure.  If
no other DS records of accepted cryptographic algorithms are
available, the DNS records below the delegation point MUST be treated
as insecure.

The ECC-GOST {{RFC5933}} algorithm MUST NOT be used when creating
DNSKEY and RRSIG records.  Validating resolvers MUST treat RRSIG
records created from DNSKEY records using these algorithms as
insecure.  If no other RRSIG records of accepted cryptographic
algorithms are available, the validating resolver MUST consider the
associated resource records as Bogus.


# Security Considerations

This document increases the security of the DNSSEC ecosystem by
deprecating algorithms that make use of older algorithms with ECC-GOST
derived uses.

# Operational Considerations

Zone owners currently making use of ECC-GOST based algorithms should
immediate switch to algorithms with stronger cryptographic strengths,
such as those listed in the introduction.  DNS registries {{?RFC8499}}
should prohibit their clients to upload and publish ECC-GOST based DS
records.

# IANA Considerations

IANA is requested to set the "DNSSEC Validation" of the "Digest
Algorithms" registry {{DS-IANA}} for ECC-GOST (3) to MUST NOT.

IANA is requested to set the "Recommended for DNSSEC Validation"
column of the DNS Security Algorithm Numbers registry {{DNSKEY-IANA}}
for ECC-GOST (23) to MUST NOT:

--- back

# Acknowledgments

The authors appreciate the comments and suggestions from the following
IETF participants in helping produce this document: Mark Andrews, Mark
Andrews, Paul Wouters and the many members of the DNSOP working group
that discussed this draft.

# Current algorithm usage levels

The DNSSEC scanning project by Viktor Dukhovni and Wes Hardaker
highlights the current deployment of various algorithms on the
https://stats.dnssec-tools.org/ website.

[RFC Editor: please delete this section upon publication]

# Github Version of this document

While this document is under development, it can be viewed, tracked,
fill here:

https://github.com/hardaker/draft-hardaker-dnsop-must-not-sha1

