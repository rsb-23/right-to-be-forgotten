# Specification for /.well-known/delete-account URI

## 1. Introduction

This document specifies the /.well-known/delete-account URI, a well-known URI designed to provide users with direct access to account deletion functionality. This specification aims to improve user experience and reduce the implementation of dark patterns that make account deletion unnecessarily complicated.

## 2. Purpose

The purpose of this specification is to:

- Define the /.well-known/delete-account URI
- Establish implementation guidelines for service providers
- Outline expected behavior for clients
- Promote user rights and control over their accounts

## 3. URI Specification

### 3.1 Structure

The well-known URI for account deletion follows this structure:

```
https://<domain>/.well-known/delete-account
```

Where `<domain>` is the domain name of the website or service.

### 3.2 Requirements

- The path segment "/.well-known/" MUST be used.
- The identifier "delete-account" MUST be used exactly as specified.
- The URI MUST be case-insensitive.

### 3.3 IANA considerations

This document defines the “.well-known” URI delete-account. This registration will be submitted to the IESG for review, approval, and registration with IANA using the template defined in [WELL-KNOWN] as follows:

|                           |                                         |
| ------------------------- | --------------------------------------- |
| URI suffix                | /delete-account                         |
| Change controller         | Rishabh B. (https://github.com/rsb-23/) |
| Specification document(s) | Specification. [🔗](#uri-specification) |
| Related information:      | None                                    |

## 4. Implementation Guidelines

### 4.1 For Service Providers

1. The /.well-known/delete-account URI MUST redirect to the account deletion page or process.
2. The redirect SHOULD be a direct link to initiate the account deletion process.
3. If additional verification is required, it SHOULD be handled on the destination page.
4. The destination MUST NOT be a general account settings page unless the delete option is immediately visible.
5. The account deletion process SHOULD be straightforward and free of unnecessary obstacles.

### 4.2 For Clients

1. Clients MAY use this URI to provide users with a direct link to delete their account.
2. Clients SHOULD handle 404 responses gracefully, as not all services will implement this URI.
3. Clients MAY inform users if a service does not support this well-known URI.

Given an [origin], clients generate a delete account url by running these steps:

1. If origin is not a potentially trustworthy origin, return failure.
1. Let url be a new URL with values set as follows:
   | | |
   | ------ | ----------------------------- |
   | scheme | origin’s [scheme] |
   | host | origin’s [host] |
   | port | origin’s [port] |
   | path | ../.well-known/delete-account |

1. Return url.

> The delete account url for origin https://example.com/ will be https://example.com/.well-known/delete-account.

## 5. User Experience Considerations

### 5.1 Accessibility

- The account deletion page SHOULD be accessible and usable by each user.
- Clear instructions SHOULD be provided in plain language.

### 5.2 Confirmation

- A confirmation step MAY be included to prevent accidental deletions.
- Any confirmation step SHOULD be simple and direct.

### 5.3 Data Handling

- Clear information SHOULD be provided about what data will be deleted or retained.
- Options for data export MAY be offered before deletion, where applicable.

## 6. Security Considerations

- Implementation MUST ensure that only authenticated and authorized users can delete their own accounts.
- HTTPS MUST be used to protect the user's privacy and security.
- Services SHOULD implement appropriate measures to prevent unauthorized bulk account deletions.

## 7. Rationale

The /.well-known/delete-account URI aims to:

- Empower users to easily exercise their right to delete their accounts
- Simplify the account deletion process for users
- Discourage dark patterns in account management
- Standardize the location of account deletion functionality across services
- Enable password managers and similar tools to incorporate account deletion features, enhancing user control over their digital presence

## 8. Examples

Correct implementation:

```
https://example.com/.well-known/delete-account
-> Redirects to https://example.com/accounts/delete
```

Incorrect implementation:

```
https://example.com/.well-known/delete-account
-> Redirects to https://example.com/account-settings
```

## 9. References

- [RFC 8615][well-known]: Well-Known Uniform Resource Identifiers (URIs)
- [Article 17 of GDPR][gdpr]: Right to erasure ('right to be forgotten')

## 10. Revision History

- Version 0.1: Initial specification (Date: 25<sup>th</sup> September 2024)

[origin]: https://url.spec.whatwg.org/#concept-url-origin
[scheme]: https://html.spec.whatwg.org/multipage/origin.html#concept-origin-scheme
[host]: https://html.spec.whatwg.org/multipage/origin.html#concept-origin-host
[port]: https://html.spec.whatwg.org/multipage/origin.html#concept-origin-port
[gdpr]: https://gdpr-info.eu/art-17-gdpr
[well-known]: https://datatracker.ietf.org/doc/html/rfc8615
