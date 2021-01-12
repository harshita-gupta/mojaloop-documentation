# POST Participants \(batch\)

Design for the creation of a Participant by a DFSP via a batch request.

## Notes

* Operation only supports requests which contain:
  * All Participant's FSPs match the FSPIOP-Source
  * All Participant's will be of the same Currency as per the [Mojaloop  Specification](https://github.com/harshita-gupta/mojaloop-documentation/tree/43c018dbcbca7411f4e85477187b079b35ab0ff8/mojaloop-technical-overview/account-lookup-service/%7B%7B%20book.importedVars.mojaloop.spec.uri.doc%20%7D%7D)
* Duplicate POST Requests with matching TYPE and optional CURRENCY will be considered an **update** operation. The existing record must be completely **replaced** in its entirety. 

## Sequence Diagram

