# CBOR Identity Data in QR-Code

**Tag**: 169 (identity-data)

**Data Item**: JSON Object

**Semantics**: Unique Identity Data of a Citizen in QR-Code

**Point of contact**: Resham Chugani (resham@mosip.io)

# 1.Introduction

This document specifies a generic data structure and encoding mechanisms for storing Unique Identity Data of a Citizen registered using any ID platforms. It also specifies a transport encoding mechanism in a machine-readable optical format (QR).

# 2.Rationale

Once a citizen is registered in an identity system, their data serves as the foundation for identification, granting them access to social benefits and government services. The level of assurance in this identification process varies depending on the authentication method employed. Low assurance is achieved through the use of basic identifiers like ID numbers, demographic data, passwords, or PINs. Conversely, higher assurance levels are attained through methods such as one-time passwords (OTP) or biometrics.

Among these methods, biometric based authentication, such as facial authentication, offers the highest level of assurance as it directly verifies the presence of the citizen. While this is effective for online systems where verification is conducted on a server, offline authentication presents challenges in maintaining a similarly high level of assurance.

For instance, in scenarios involving cross-border verification, remote areas often face significant internet connectivity issues. Even when internet access is available, server reliability may be inconsistent. In such circumstances, scanning a QR code containing a citizen's facial photograph and identity information, alongside assurance that the data is country-signed, provides an additional layer of security and affirmation for the countries involved.

To tackle the aforementioned challenge and include a face photograph within the QR code, we propose a solution that involves embedding a low-resolution grayscale image of the citizen along with a minimal demographic dataset within the QR code. This QR code would be digitally signed by the ID system and then printed on a physical card. Subsequently, the signed data within the QR code can be utilized for facial authentication. However, it's essential to recognize that QR codes have limitations regarding size. To address this, we suggest leveraging CBOR Web Token (CWT) to generate a smaller signature and more condensed data.

# 3.Semantics

Claim 169 represents a JSON Object that includes a range of ID attributes defined by the issuing identity system as key-value pairs. Below, you can find an illustration of the ID JSON structure contained within Claim 169, where:
### 3.1 JSON Struchture Overview

| Attribute | Type  | Attribute Name       | Description                                                                                                      |
|-----------|-------|----------------------|------------------------------------------------------------------------------------------------------------------|
| 1         | tstr  | ID                   | Unique ID to indicate the PII data                                                                               |
| 2         | tstr  | Version              |                                                                                                                  |
| 3         | tstr  | Language             |                                                                                                                  |
| 4         | tstr  | Issuing Authority    |                                                                                                                  |
| 5         | tstr  | First Name           |                                                                                                                  |
| 6         | tstr  | Middle Name          |                                                                                                                  |
| 7         | tstr  | Last Name            |                                                                                                                  |
| 8         | tstr  | Full Name            |                                                                                                                  |
| 9         | tstr  | Gender               |                                                                                                                  |
| 10        | tstr  | Date of Birth        |                                                                                                                  |
| 11        | tstr  | Address              | Address of the citizen with address line separator character `\n`                                                |
| 12        | [int] | Best Quality Fingers |                                                                                                                  |
| 13        | tstr  | Binary Image         | Binary image data representing the citizen's photograph                                                          |
| 14        | tstr  | Email ID             |                                                                                                                  |
| 15        | tstr  | Phone Number         |                                                                                                                  |
| 16        | tstr  | Martial Status       |                                                                                                                  |
| 17        | tstr  | Nationality          |                                                                                                                  |
| 18        | tstr  | Guardian             | Entity playing the role of a guardian of the citizen such as mother, father, spouse, sister, legal guardian etc. |
| 19        | tstr  | Additional attribute | Reserved for future attributes                                                                                   |
| 20        | tstr  | Additional attribute | Reserved for future attributes                                                                                   |
| 21        | tstr  | Additional attribute | Reserved for future attributes                                                                                   |
| 22        | tstr  | Additional attribute | Reserved for future attributes                                                                                   |
| 23        | tstr  | Additional attribute | Reserved for future attributes                                                                                   |
| 24        | tstr  | Additional attribute | Reserved for future attributes                                                                                   |
| 24        | tstr  | Additional attribute | Reserved for future attributes                                                                                   |
| 26        | tstr  | Additional attribute | Reserved for future attributes                                                                                   |
| 27        | tstr  | Additional attribute | Reserved for future attributes                                                                                   |
| 28        | tstr  | Additional attribute | Reserved for future attributes                                                                                   |
| 29        | tstr  | Additional attribute | Reserved for future attributes                                                                                   |
| 30        | tstr  | Additional attribute | Reserved for future attributes                                                                                   |
| 31        | tstr  | Additional attribute | Reserved for future attributes                                                                                   |
| 32        | tstr  | Additional attribute | Reserved for future attributes                                                                                   |
| 33        | tstr  | Additional attribute | Reserved for future attributes                                                                                   |
| 34        | tstr  | Additional attribute | Reserved for future attributes                                                                                   |
| 35        | tstr  | Additional attribute | Reserved for future attributes                                                                                   |
| 36        | tstr  | Additional attribute | Reserved for future attributes                                                                                   |
| 37        | tstr  | Additional attribute | Reserved for future attributes                                                                                   |
| 38        | tstr  | Additional attribute | Reserved for future attributes                                                                                   |
| 39        | tstr  | Additional attribute | Reserved for future attributes                                                                                   |
| 40        | tstr  | Additional attribute | Reserved for future attributes                                                                                   |
| 41        | tstr  | Additional attribute | Reserved for future attributes                                                                                   |
| 42        | tstr  | Additional attribute | Reserved for future attributes                                                                                   |
| 43        | tstr  | Additional attribute | Reserved for future attributes                                                                                   |
| 44        | tstr  | Additional attribute | Reserved for future attributes                                                                                   |
| 45        | tstr  | Additional attribute | Reserved for future attributes                                                                                   |
| 46        | tstr  | Additional attribute | Reserved for future attributes                                                                                   |
| 47        | tstr  | Additional attribute | Reserved for future attributes                                                                                   |
| 48        | tstr  | Additional attribute | Reserved for future attributes                                                                                   |
| 49        | tstr  | Additional attribute | Reserved for future attributes                                                                                   |
| 50        | tstr  | Additional attribute | Reserved for future attributes                                                                                   |


### 3.2 JSON Struchture Example
```CWT
{
   "1":"COUN",
   "6":1665980929,
   "8":{
      "3":"dfd1aa976d8d4575a0fe34b96de2bfad"
   },
   "169":{
        "1": "11110000324013",
        "2": "1.0",
        "3": "EN",
        "4": "DMV",
        "5": "Peter",
        "6": "M",
        "7": "Jhon",
        "8": "Peter M Jhon",
        "9": "Male",
        "10": "1988-01-02",
        "11": "New City, METRO LINE, PA",
        "12": "[1,2]",
        "13": "03CBABDF83D068ACB5DE65B3CDF25E0036F2C546CB90378C587A076E7A759DFD27CA7872B6CDFF339AEAACA61A6023FD1D305A9B4F33CAA248CEDE38B67D7C915C59A51BB4E77D10077A625258873183F82D65F4C482503A5A01F41DEE612C3542E5370987815E592B8EA2020FD3BDDC747897DB10237EAD179E55B441BC6D8BAD07CE535129CF8D559445CC3A29D746FBF1174DE2E7C0F3439BE7DBEA4520CF88825AAE6B1F291A746AB8177C65B2A459DD19BD32C0C3070004B85C1D63034707CC690AB0BA023350C8337FC6894061EB8A714A8F22FE2365E7A904C72DEC9746ABEA1A3296ECACD1A40450794EDCD2B34844E7C19EB7FB1A4AF3B05C3B374BD2941603F72D3F9A62EAB9A2FDAEEEEC8EE6E350F8A1863C0A0AB1B4058D154559A1CD5133EFCF682ABC339960819C9427889D60380B635A7D21D017974BBA57798490F668ADD86DA58125D9C4C1202CA1308F7734E43E8F77CEB0AF968A8F8B88849F9B98B26620399470ED057E7931DED82876DCA896A30D0031A8CBD7B9EDFDF16C15C6853F4F8D9EEC09317C84EDAE4B349FE54D23D8EC7DC9BB9F69FD7B7B23383B64F22E25F",
        "14": "peter@example.com",
        "15": "+1 234-567",
        "16": "US",
}
```

### 4. CBOR Identity Data in QR-Code Claims Registration
This specification registers the `identity-data` claim in the IANA "CBOR Web Token (CWT) Claims" registry [IANA.CWT.Claims], established by [RFC8392].

#### 4.1 Registry Contents
Claim Name: identity-data

Claim Description: Identity Data

JWT Claim Name: identity-data

Claim Key: 169

Claim Value Type(s): <>

Change Controller: MOSIP

Specification Document(s): Section 1

# References

[1] C. Bormann, and P. Hoffman. "Concise Binary Object Representation (CBOR)". [RFC 7049](https://tools.ietf.org/html/rfc7049), October 2013.

[2] Mike Jones, Hannes Tschofenig, Ludwig Seitz  "CBOR Web Token (CWT)". [RFC 8392](https://www.iana.org/go/rfc8392), March 2018.


# Author

Resham Chugani ([resham@mosip.io](mailto:resham@mosip.io))