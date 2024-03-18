# European Blockchain Service Infrastructure (EBSI)

EQAR is enabling the use of DEQAR data on external quality assurance within the EBSI ecosystem. This allows recognised European higher education institutions to easily confirm their accreditation status and thus facilitates adoption of EBSI digital diplomas.

The EU is developing a technical architecture for digitally-issued education diplomas as part of the [European Blockchain Service Infrastructure (EBSI)](https://ec.europa.eu/digital-building-blocks/wikis/display/ebsi). The EBSI Diplomas Use Case addresses the same needs as the [European Digital Credentials for Learning](europass.md), based on a different underlying technical platform. Yet, both initiatives are compatible and based on the same higher-level data models and standards.

EQAR has worked to enable the use of DEQAR data on external quality assurance and accreditation as part of the EBSI Early Adopters Programme, in close dialogue with the EBSI architects and the convenors of the Diplomas Use Case. Currently, two types of Verifiable Credentials (VC) can be issued:

 1. **EBSI Verifiable Accreditations** can be issued for external quality assurance results with an official status in a national system (“part of obligatory EQA system”).

    The higher education institution must have an EBSI DID. Currently, EBSI DIDs need to be communicated to EQAR and recorded manually.

    If your institution has an EBSI DID and wishes to use EBSI Verifiabl Accreditations issued through DEQAR, please send your DID to <deqar@eqar.eu>.

 2. **DEQAR format VCs** are based on the plain W3C Recommendation and an own data model, closely following EBSI standards but without EBSI-specific or EU-specific elements or data types. The higher education institution is identified by its DEQAR URI in this case.

    These VCs can be issued for all reports in DEQAR and are issued by EQAR under `did:web:data.deqar.eu`.

