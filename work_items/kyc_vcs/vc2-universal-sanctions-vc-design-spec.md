# Verifiable Credentials #2

## Universal Sanctions Verifiable Credential Design Specifications

### Considerations and Assumptions: 
1. This initial Universal Sanctions Credential is focused on individuals and does not include checks against sanctioned entities. Additional Sanctions VC design specifications will be developed at a later stage for entities or vessels.

2. This Universal Sanctions Credential does not include the results of checks against lists of Politically Exposed Person (PEPs), even though PEP checks may be performed at the same time as Sanctions checks. PEPs requirements are being considered as part of the KYC Credential design.

3. This Universal Sanctions Credential will be based on an **Open Standard for Sanctions Screening** which is currently under development with the expectation that anyone issuing this credential has controls that align to the standard. The Open Standard will include best practices for screening frequency, the scope of global sanctions lists included, data quality and cleansing, matching fuzzy logic, and acceptable match rates.

4. Sanctions check (and therefore the corresponding VCs) frequency depends on the transacting companies’ risk profile and can be daily, weekly, or monthly.  The lists themselves are updated ad hoc by regulatory agencies. However, a recent OFAC finding of violation cited a US financial institution for processing transactions for two customers who were newly designated individuals conducting transactions that occurred on the same day the individuals were added to the list.  While real-time or daily screening frequency may be a global best practice to ensure that updates to sanctions lists are reflected timely, not all Issuers will have the resources and automated systems to facilitate sanctions checks at this frequency. To manage variability in resources and risk, authenticator assurance levels should reflect the **Open Standard for Sanctions Screening**.

5. Inherent in the ecosystem for decentralized identity is the preservation of privacy and user control. Sanctions credentials offer us an early path to practical use cases for selective disclosure and zero-knowledge proof (ZKP) privacy techniques. In the USA all companies are subject to OFAC regulations and cannot “do business” with sanctioned individuals or entities. This means that sanctions credentials have a wide variety of practical use cases for both financial and non-financial online interactions. Companies conducting these non-financial interactions are likely to benefit from the proactive knowledge that the user is not on the relevant sanctions lists, but lack the resources to conduct proactive sanctions screening themselves.

6. Including the hundreds of global sanctions screening lists introduces complexity and variability that may lead to too many versions of the VC and therefore limits the acceptance of a Universal Sanctions Credential. Instead, Issuers should leverage the **Open Standard for Sanctions Screening**, which will include common sanctions lists focused on countries with the most strict sanctions enforcement controls, including the USA, Europe, UK, Canada, and Australia. 

    *The Sanctions lists selected for the Open Standard are intended to provide broad global coverage and usage. An Issuer can choose to screen against additional or local lists per their internal controls or regulatory obligations. However, it is important to note that minimizing the lists screened against, including setting minimal standards for list data quality will increase automation and reduce manual review to clear potential matches.*

7. For certain financial transactions, Sanctions Credentials may be presented together with a KYC Credential before transacting. Therefore, Issuers may choose to issue more than one credential when they are performing multiple compliance checks for a user at the same time. We anticipate that there is also a valid use case for sanctions credentials alone, without KYC. For unregulated transactions or activity a sanctions credential may be presented first and the additional credential requirements requested at a later date or never. 

8. Finally, it is yet unclear if individuals will accept a “Matched” sanctions credential, given they have control over the VCs they accept. Therefore, in practice a “clear” or “unmatched” sanctions result is what companies will use to address sanctions risk. Any user who cannot produce this credential may need to complete traditional sanctions checks outside of the decentralized identity ecosystem or may be unable to transact with certain institutions.

### Standard Vocabulary for Sanctions Credentials:
The design specification for a Universal Sanctions Credential is intended to limit the disclosure of personally identifiable information (PII), except where required by financial regulations. Additional data fields (than those included below) may be collected and used by the Issuer to clear potential sanctions matches. However, they should not be disclosed in the credential itself. This list below strikes the right balance of minimizing the disclosure of personal information while collecting sufficient information to reduce match false positives and link the result to an individual. 

The minimal data fields for the Universal Sanctions Credential include:

* Family Name (last name)
* Given Name (first name)
* Additional Names (including middle name, aka or alias)
* Birth Date (YYYY/MM/DD)
* Nationality
* IP Address/Geolocation - we anticipate that IP Geolocation will be a standard data field for all identity related credential formats

These fields have been included to minimize false positives and to provide sufficient information for the Verifier to associate the credential to a unique individual. *However, please note that more data points included in the credential can be used to minimize false positives.* Selective disclosure or ZKP presentation can also be utilized to limit the sharing of these data fields when it is not required by the Verifier (who may not be subject to financial regulations for certain types of transactions).


| The Universal Sanctions Credential can be presented using Selective Disclosure or Zero Knowledge Proofs (ZKPs) to further reduce the disclosure of the personal information contained within the credential. This presentation format is likely to be used when the transaction is non-financial or customer recordkeeping is not required. Therefore, we anticipate a wide range of uses for Selective Disclosure and ZKP presentation with the Universal Sanctions Credential. |
|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|



The standard practice for issuing Universal Sanctions Credentials will utilize revocation. Re-screening frequency for this credential is expected to be variable but frequent (i.e. daily, weekly, or monthly). Therefore, the Issuer will revoke the old credential and issue a new credential every time the user is re-screened against sanctions lists. This ensures that updates to global sanctions lists are reflected in the most recent credential issuance and that the previous credential can no longer be presented.

The vocabulary for these inputs mirrors the [KYC VC](https://github.com/TBD54566975/credentials-working-group/blob/main/work_items/kyc-vcs/requirements-to-accept-a-kyc-vc.md) so that there is consistency in terms and usage.



| Vocabulary | Field Description | 
| -------- | -------- | 
| CredentialType     | Universal Sanctions Credential    | 
| SubType    | Individual    | 
| Sanctions Result     | match, no-match, undetermined (note that an undetermined or no-match result is unlikely to be accepted by the user)     | 
| Family Name     | Refer to Person Schema. In the USA, the Family Name is the Last Name of a Person 
| Given Name     | Refer to Person Schema. In the USA, the Given Name is the First Name of a Person    | 
| Additional Name     | Refer to Person Schema. This can be used to include Middle Name, AKA or Alias or left blank or n/a     | 
| Date of Birth (DOB)     | BirthDate using the Universal Date Format (ISO 8601): YYYY/MM/DD    | 
| Sanctions Description    | Includes any details about the match including the full name and alias’ of the matched individual. The description contents and format will depend on the list. There may also be multiple matches.Consider aligning with existing data formats such as Swift MT103.  This field will be n/a (if the result is “no match” or “undetermined”)    | 
| Effective Date & Time     | YYYY/MM/DD, HH/MM/SS - this should be the most recent date and time the sanctions check was performed    | 
| Expiration Date & Time     | YYYY,MM,DD, HH/MM/SS - We think it is unlikely that this field will be populated by the Issuer, as sanctions credentials can be revoked and reissued. However expiration is a standard VC field.     | 
| Verifier Name     | Name or ideally the DID reference of the sanctions vendor who performs the check      | 
| IP Geolocation    | Consider whether this should be an address, location or both. The credential could be enriched with geolocation data from third parties if they are used by the Issuer.  Note that the accuracy of IP geolocation data varies significantly and is also dependent on whether the user is masking their IP.    | 

**Person Schema Reference:** https://schema.org/Person

If the Sanctions result is “no match” or “undetermined” then the **Sanctions Description** field will be n/a or blank.

### Example #1 (ZKP presentation):
As you can see in the result when the user selects ZKP Presentation, only the sanctions result information is shared with the verifier, and the underlying personal data is not disclosed. 

_// specify the “Sanctions Check”_
```jsonld=
{
    “type”: “VerifiableCredential”
    “issuer”: “did:example:BlockInc”,
    “issanceDate” "2010-01-01T00:00:00Z",
    “credentialSubject”: { 
    “id”: “did:example:1a2b3c4d5e6f7g”,
     ...
    },
    “proof”: {...}
}
```

_// specify the contents of the “VerifiableCredential”_

```jsonld=
{
    “credentialType”: “Universal Sanctions Credential”,
    “subType”: “Individual”,
    “sanctionsResult”: “no match”,
    “effectiveDate”: “2022/08/19, 11:03:00”,
    “verifierName”: “did:example:SanctionsVendor”
}
```

*Refer to the [KYC VC](https://github.com/TBD54566975/credentials-working-group/blob/main/work_items/kyc-vcs/requirements-to-accept-a-kyc-vc.md) for specifications to resolve the Issuer or Verifier DID.*

### Example #2 (normal presentation):

_// specify the “Sanctions Check”_

```jsonld=
{
    “type”: “VerifiableCredential”
    “issuer”: “did:example:BlockInc”,
    “issanceDate” "2010-01-01T00:00:00Z",
    “credentialSubject”: { 
    “id”: “did:example:1a2b3c4d5e6f7g”,
    ...
    },
    “proof”: {...}
}
```

_// specify the contents of the “VerifiableCredential”_

```jsonld=
{
    “credentialType”: “Universal Sanctions Credential”,
    “subType”: “Individual”,
    “sanctionsResult”: “match”,
    “familyName”: “Ali”,
    “givenName”: “Ahmed”,
    “additionalName”: “Mohammed”,
    “birthDate”: “1965/04/25”,
    “sanctionsDescription”: “Ahmed Mohammed Hamed Ali, SDN, SDGT, Citizenship Egypt, Date of Birth	1965	Remarks n/a, Place of Birth Egypt, aka ABDUREHMAN Ahmed Mohamme, aka AHMED Ahmed”,
    “effectiveDate”: “2022/07/22, 15:45:03”,
    “expirationDate”: “2022/07/29, 15:45:03”,
    “verifierName”: “did:example:SanctionsVendor”,
    “ipGeolocation”: “Alexandria, Egypt”
}
```
