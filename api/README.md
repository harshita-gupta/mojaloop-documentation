# API Specifications

## Mojaloop API

Documentation: [Mojaloop Specification](https://github.com/harshita-gupta/mojaloop-documentation/tree/43c018dbcbca7411f4e85477187b079b35ab0ff8/api/%7B%7B%20book.importedVars.mojaloop.spec.uri.doc%20%7D%7D)

* [Mojaloop API  Specification](mojaloop-api-specification.md)
* [Swagger](https://github.com/harshita-gupta/mojaloop-documentation/tree/43c018dbcbca7411f4e85477187b079b35ab0ff8/api/%7B%7B%20book.importedVars.mojaloop.spec.uri.api%20%7D%7D)

### Versions

| Version | Info | Release Date |
| :--- | :--- | :--- |
| 1.0 | Initial release | 2018-11-01 |

## Central Ledger API

Documentation: [Central-Ledger Service](../mojaloop-technical-overview/central-ledger/)

* [Central Ledger API  Specification](central-ledger-api-specification.md)
* [Swagger](https://github.com/harshita-gupta/mojaloop-documentation/tree/43c018dbcbca7411f4e85477187b079b35ab0ff8/api/%7B%7B%20book.importedVars.central_ledger.spec.uri.api%20%7D%7D)

### Versions

| Version | Info | Release Date |
| :--- | :--- | :--- |
| 3.8.3.1 | Feature/\#538 FundsIn/Out Position Changes | 2018-12-11 |
| 3.8.3 | Initial release | 2018-11-02 |

## Central Settlements API

Documentation: [Central-Settlements Service](../mojaloop-technical-overview/central-settlements/)

* [Central Settlements API  Specification](central-settlements-api-specification.md)
* [Swagger](https://github.com/harshita-gupta/mojaloop-documentation/tree/43c018dbcbca7411f4e85477187b079b35ab0ff8/api/%7B%7B%20book.importedVars.settlement.spec.uri.api%20%7D%7D)

### Versions

| Version | Info | Release Date |
| :--- | :--- | :--- |
| 1.1 | Implementation driven corrections | 2019-04-03 |
| 1.0 | Initial release | 2018-08-31 |

## ALS Oracle API

Documentation: [Account-Lookup Service](../mojaloop-technical-overview/account-lookup-service/)

* [ALS Oracle API  Specification](mojaloop-api-specification.md#tag-parties)
* [Swagger](https://github.com/harshita-gupta/mojaloop-documentation/tree/43c018dbcbca7411f4e85477187b079b35ab0ff8/api/%7B%7B%20book.importedVars.als.oracle.spec.uri.api%20%7D%7D)

Notes:

* ALS Oracle API is based on the [Mojaloop Specification](https://github.com/harshita-gupta/mojaloop-documentation/tree/43c018dbcbca7411f4e85477187b079b35ab0ff8/api/%7B%7B%20book.importedVars.mojaloop.spec.uri.doc%20%7D%7D) with the following main differences:
  * Operations follow traditional REST API paradigms more strictly.
  * Operations are **synchronous** with an immediate response unlike [Mojaloop Specification](https://github.com/harshita-gupta/mojaloop-documentation/tree/43c018dbcbca7411f4e85477187b079b35ab0ff8/api/%7B%7B%20book.importedVars.mojaloop.spec.uri.doc%20%7D%7D) which provides a responds via **asynchronous callbacks**.
  * `PUT /participants` is to update existing records and not a Callback as per the [Mojaloop Specification](https://github.com/harshita-gupta/mojaloop-documentation/tree/43c018dbcbca7411f4e85477187b079b35ab0ff8/api/%7B%7B%20book.importedVars.mojaloop.spec.uri.doc%20%7D%7D)
  * `GET /participants` response body returns a list of Participants, containing `currency`.
  * `POST /participants` request body includes the `currency` as part of each record. 

### Versions

| Version | Info | Release Date |
| :--- | :--- | :--- |
| 1.2 | Removal of duplicated currency from `POST /participants` payload. | 2019-05-20 |
| 1.1 | `PUT /participants/{Type}/{ID}` returns a `HTTP 204 - No Content on success`. This was previously returned `HTTP 200 - Success`  `POST /participants` now returns a list a `partyList` either containing a `PartyIdInfo` or `ErrorInformation`. This provides a closer alignment to the Mojaloop Specification. | 2019-03-28 |
| 1.0 | Initial release | 2019-03-08 |

