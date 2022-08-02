# VC #1 Open Questions
The Verifiable Credentials Document #1 outlined the acceptance criteria for a regulated financial institution to accept a KYC Verifiable Credential. This was the first draft of a framework that we hope will be adopted by the broader community and used to issue and accept Verifiable Credentials for use in online financial transactions.

However, this is only a first draft and there remain many questions, additional considerations and decisions to be made with the help of the broader community of participants willing to issue and accept these credentials. Below are a list of some of these questions and considerations:

1. Who should issue the KYC credential? There are schools of thought that the credential should be issued directly from the source which would reduce the opportunities for manipulation through third parties. However, the sources (except when the source is a government agency) are usually identity vendors who are relatively unknown to consumers. So is it better to have the vendor issue a credential directly to the user or for the PFI to wrap credentials from their vendors and then issue the credential to users?

2. Furthermore, what are the financial incentives for issuing a credential and how does this align with existing identity verification vendors business models (which are usually B2B)?

3. The matter of biometrics has not been included in the spec. How do we account for controls like liveness and selfie checks to determine that the person presenting the ID is also the owner of the identity? Also, how do we replicate these checks every time the credential is presented? Do we need to?

4. How do we determine the quality of a KYC credential? Some thoughts are to expand on the NIST Digital Identity Guidelines for Identity Proofing (NIST SP 800-63).

5. There are other data points beyond KYC such as email address, IP address and phone number that provide valuable information to verify the identity of the customer and determine fraud risk. Companies usually collect this information when onboarding a customer online. How do we incorporate this information into a KYC VC or should this be a separate credential?

6. How can we address changes in the Purpose of Account attribute? Unlike many of these data elements, the purpose of an account may change given the type of transaction or account relationship. Would it be better to change this field to “Source of Wealth” which is likely to be more static? Will this attribute still meet regulatory requirements for the purpose of account? Or should we have both?

7. We are recommending that initially we separate out the Identity and Address Verification Evidence from the KYC Verifiable Credential for several reasons such as simplicity, selective disclosure and segregating data which requires updating from static data. However, there are ways to combine this information into a single credential and still minimize the information shared with PFIs. So the question is does it make sense to separate the KYC attributes from address verification into separate credentials or to combine them into one credential?

8. Taking this one step further, should we separate different aspects of the onboarding process into separate credentials? For example, KYC which is usually the basic PII information, from the identity document, and further from CDD and EDD fields which can include other non-static information.

9. Occupation information is typically collected during the enhanced due diligence process, but is also a requirement in certain regulated jurisdictions. This information can be highly subjective and is not easy to verify. Instead, an employment credential may be preferable to including employment information in the KYC VC.

10. Even for non documentary verification (when there is no document expiration date), we can set standard expiry dates within the credential. For example,  compliance standards dictate that KYC should be refreshed every 1-3 years based on risk.

11. For the document evidence, we may want to consider all possible sources for document verification even if they are atypical such as: social security card, utility bill, or birth certificate for example.

12. Companies also store a copy of the photo ID and/or the personal data from the ID, through OCR technology, at field level. This typically includes: Full name, Date of Birth, ID Type, ID Number, ID Country and address (if applicable). Therefore, we may want to consider including the personal information on the identity document within the verifiable credential evidence and to allow the company to compare this information to the KYC data.

13. Regulatory requirements and compliance controls may require the collection and storage of the statement, therefore it is important to consider how to comply with this requirement with verifiable credentials. For example, can or should we embed an image of the statement in the credential?
