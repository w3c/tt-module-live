# Changes in TT-Live-WebSocket-W3C vs Tech3370s1

## Major sections

The Conformance Notation page is now §2. Conformance.

The Abstract, Status of this document and Scope sections have been
editorially changed to suit the purpose of the output document. The order of
those sections differs in the W3C document template compared to the EBU one.
The W3C ordering has been adopted because the document must pass W3C publication
rules.

In the Introduction section, the §1.1 "Document Structure" subsection is removed.

The §2.1 "Definition of terms" section is promoted to section 
4 Terms and Definitions and replaces §2 Definitions and Concepts.

§6 Bibliography is renamed A.2 Informative references.

## Normative changes

Throughout the document, any basis on EBU-TT Part 1 is re-based on TTML1.

This includes the terms:
*   "EBU-TT Live Document" becomes "Live Document"
*   "EBU-TT Part 3 Document" becomes "TTML Live Document"
*   "EBU-TT Part 3 sequence" becomes "TTML Live sequence"

### 4 Definition of Terms

See above for changes to defined terms.

### 5 Carriage Specification Details

Sentence describing where WebSocket is specified removed because the reference
to WebSocket points at that location already.

### A references

#### A.1 Normative references

Removed references:
*   EBU Tech3370 (moved to Informatie references)
*   ANDR API (moved to Informative references)
*   JT-NM (moved to Informative references)
*   WAMP(moved to Informative references)

Added References:
*   TTML-Live

#### B.2 Informative references

(these deltas relative to Tech3370 §6 Bibliography)

Removed references:
*   EBU Tech 3264
*   EBU Tech 3350
*   EBU Tech 3360
*   EBU Tech 3380
*   EBU Tech 3390
*   EBU R 133
*   SMPTE-12M-1:2008
*   SMPTE ST 2052-1:2010
*   XML 1.0
*   XML Schema Part 2
*   TLS

Added references:
*   ANDR API (was in Normative references)
*   EBU Tech3370 (was in Normative references)
*   EBU Tech3370s1
*   JT-NM (was in Normative references)
*   WAMP (was in Normative references)

## Informative Changes

Throughout the document, in-document references to sections, defined terms or
references have been turned into navigable links.

Throughout the document, text prefixed "Note" or "NOTE", and footnotes
have been moved into a separate paragraph with `class="note"` which changes its formatting.

### 1 Scope

A statement added that this document fulfils the requirements for defining a
Carriage Mechanism.

### 3 Introduction

Figure 1 modified so that it could be included as an SVG diagram, and to
reference TTML Live instead of EBU-TT Part 3.

### 5 Carriage Specification Details

#### 5.6 Channel routing

The example URIs have been formatted as Examples.
