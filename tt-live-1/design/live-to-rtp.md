# TT-Live to TTML in RTP and back

The TTML Live Module specifies how to deal with sequences of TTML documents and
resolve the timing of each document based on the set of documents received so
far. The idea is that the documents can be carried from A to B over any
mechanism that is adequately well specified. For example WebSocket or the file
system would both work.

The IETF payload specification for TTML in RTP [1] defines the RTP packet
format for wrapping TTML documents, with the idea that they can be streamed
live over UDP.

[1] https://datatracker.ietf.org/doc/draft-ietf-payload-rtp-ttml/

The question arises, can a TTML document using the Live extensions be carried
over RTP, and how does the document time resolution algorithms interact with
each other?

## Key features

### TTML over RTP key features

* The packet has a timestamp, the _RTP timestamp_.
* The packet has a _sequence number_ which is used for identifying packet loss
and goes up by 1 for each packet.
* The payload becomes active at the RTP timestamp.
* The TTML document's `ttp:timeBase` _MUST_ be `media`.
* All times within the TTML document are relative to the RTP timestamp.
* Exactly zero or one document is active at any time.
* If a document begins before the end time of an active document, that
active document becomes inactive and the new document becomes active,
at the RTP timestamp of the new document.
* Any identifying data about the RTP stream is external to the stream, for example
in some other manifest file.

### TT-Live key features

* Each document has a _sequence number_ and a _sequence identifier_.
* Within a sequence every document has the same sequence identifier.
* Sequence numbers go up as new documents are issued, but not necessarily by 1
for each subsequent document.
* Each document becomes active at its _document resolved begin time_.
* The document resolved begin time is the later of the _document availability time_,
the _earliest computed begin time_ and any externally specified document activation
begin time.
* Each document becomes inactive at its _document resolved end time_.
* The document resolved end time is the earlier of the 
_earliest document resolved begin time_ of all available documents in the sequence
with a greater sequence number, the document resolved begin time plus the `dur` on
the `body`, if present, the _latest computed end time_ and any externally specified
document deactivation time.

## Creating a TT-Live document from a TTML document in an RTP packet

The _document availability time_ is the RTP timestamp.
The RTP timestamp can be mapped to the TT-Live `sequenceNumber`.
If there is already a `sequenceNumber` present, *What do do?!* (remove it?)
The TT-Live `sequenceIdentifier` must be derived from some out-of-band protocol.
The media time needs to be incremented by the media time equivalent to the
RTP timestamp. This can be done by adding the offset to the `body` element's `begin`
attribute, if present, or by creating that attribute with the media time offset as
its value.

## Creating an RTP packet from a TT-Live document

The RTP packet timestamp is the equivalent to the document resolved begin time.
The `sequenceNumber` can be removed or left in place.
The times in the document have to be adjusted to subtract the document resolved begin time.
They also have to be expressed in `media` timebase and the `ttp:timeBase` must be
set to `media` if not already. If a clock timebase is used, the equivalent RTP timestamp
for the clock time in the document must be computed.
If any of the document content is earlier than the document resolved begin time, it must be removed.
Create the RTP packet with the TTML document as the payload.

