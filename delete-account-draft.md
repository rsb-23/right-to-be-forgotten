# delete-account Well-Known URI

> LAST MODIFIED : 03<sup>rd</sup> October 2024

## Abstract

This specification defines a well-known URL that sites can use to make their `delete account` page discoverable by tools. This simple affordance provides a way for software to help the user find the way to delete their account.

## Introduction

Client-side password management software helps improve both the security and usability of websites which require authentication. It improves security by reducing cross-site password reuse, and enhances usability by providing autofill functionality.

Sites currently lack a way to programmatically advertise/access where a user can delete their account. By proposing a well-known URL for deleting account, this specification enables password managers to help users to quickly delete their account on sites which support it.

## Specification

A delete account url of an [origin] is a URL that points to a resource that clients can use to discover where a user should go to delete their account on [origin].

Given an origin, clients generate a delete account url by running these steps:

1. If origin is not a potentially trustworthy origin, return failure.
1. Let url be a new URL with values set as follows:
   | | |
   | ------ | ----------------------------- |
   | scheme | origin’s [scheme] |
   | host | origin’s [host] |
   | port | origin’s [port] |
   | path | ../.well-known/delete-account |

1. Return url.

> The delete account url for origin https://example.com/ is https://example.com/.well-known/delete-account.

## IANA considerations

This document defines the “.well-known” URI delete-account. This registration will be submitted to the IESG for review, approval, and registration with IANA using the template defined in [WELL-KNOWN] as follows:

|                           |                                         |
| ------------------------- | --------------------------------------- |
| URI suffix                | /delete-account                         |
| Change controller         | Rishabh B. (https://github.com/rsb-23/) |
| Specification document(s) | Specification. [🔗](#specification)     |
| Related information:      | --                                      |

## Use Cases

## Security Considerations

The resource value should not be treated as reliable because bad actors can easily spoof the resource and redirect to malicious website.

[origin]: https://url.spec.whatwg.org/#concept-url-origin
[scheme]: https://html.spec.whatwg.org/multipage/origin.html#concept-origin-scheme
[host]: https://html.spec.whatwg.org/multipage/origin.html#concept-origin-host
[port]: https://html.spec.whatwg.org/multipage/origin.html#concept-origin-port
[well-known]: https://datatracker.ietf.org/doc/html/rfc8615
