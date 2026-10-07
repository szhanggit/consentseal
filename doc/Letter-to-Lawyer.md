**SELAH HEAD SPA**
[Street address]
[City], Ontario [Postal code]
[Phone] · [Email]

[Date]

**PRIVILEGED AND CONFIDENTIAL — REQUEST FOR LEGAL ADVICE**

[Lawyer name]
[Law firm]
[Address]

**Re: Electronic client intake, consent and signature records — request for opinion and fee estimate**

Dear [Lawyer name],

SELAH HEAD SPA (the "Clinic") provides treatments in Ontario. Many clients pay through extended health benefit plans (for example Sun Life, Manulife, Canada Life). These insurers expect the Clinic to keep, for each client, a signed health history (intake) form and a signed consent to treatment form, and they may review these records when auditing claims.

We are building a system, called ConsentSeal, to replace our paper forms with an electronic process. Before we store any real client information, we are asking for your advice on the questions below. We would also appreciate an estimate of your fees and timeline.

## 1. The current paper forms

- **Health History Form:**
  - contact details, date of birth, occupation;
  - medical conditions (cardiovascular, respiratory, infections, diabetes, cancer, pregnancy and others);
  - medications, family physician, implants, surgeries and injuries;
  - reason for the visit.

  It states that information is kept confidential and that the client's written permission is required to release it. It has no signature line.
- **Consent to Osteopathic Treatment:**
  - a description of the risks of treatment;
  - four statements beginning "I acknowledge I have discussed…" and four beginning "I understand that…";
  - the name of the practitioner and the treatment areas;
  - a statement that the consent applies to present and future care;
  - a signature line ("Patient signature (or Legal Guardian)") and a date.

  The original document contains spelling errors, including "OSTEOAPTHIC" in the title and "sourness" where "soreness" may be intended.

Copies of both forms are enclosed.

## 2. The proposed electronic process

1. **The client fills in the health history form** online before the visit. They identify themselves with their phone number and email address; there are no accounts or passwords. Their answers are saved as a draft.
2. **At the Clinic, the client signs in person** on a Clinic tablet:
   - they review their completed form;
   - they read the full consent text (they must scroll to the end before continuing);
   - they tick each of the 8 acknowledgement/understanding statements;
   - they tick a ninth box: "I agree to sign this document electronically";
   - they select treatment areas and enter the practitioner's name;
   - they sign by hand with a finger or stylus.
3. **A named staff member acts as witness.** They check the client's identification in person, record the ID type (driver's licence, health card or passport; never the number), and confirm with a personal PIN.
4. **At the moment of signing, the system creates PDFs of the original forms, filled in and signed:**
   - The consent form shows the signature and date.
   - The health history form gets an added page, clearly labelled as electronically generated. It contains an attestation ("I confirm that the health history on the previous page is complete and accurate"), the signature, name, date and a record number.
5. **The PDFs are sealed:**
   - a SHA-256 fingerprint is recorded;
   - an RFC 3161 trusted timestamp is obtained from a third-party timestamping authority (only the fingerprint is sent);
   - the files are stored in write-once storage (Amazon S3 Object Lock, compliance mode) in the AWS Canada (Central) region, where they cannot be changed or deleted during the retention period;
   - a tamper-evident, hash-chained log records each step: viewed, confirmed, agreed to sign electronically, signed, witnessed, sealed, and later downloads and verifications.
6. **Updates:** if a client's health information changes, or the consent wording changes, the client signs a new version in the same way. Earlier versions are kept.
7. **Clients below a set age** (currently 18, configurable) cannot sign electronically and are directed to a paper process.
8. **Invitations to fill in the form** may be sent by email or SMS to clients the Clinic has registered. They contain only the client's first name and a link.
9. **Data storage:** all data is stored in Canada and encrypted. Access is limited to named staff accounts and is logged.

## 3. Questions

### A. Which laws apply
1. Is the Clinic a "health information custodian" under the *Personal Health Information Protection Act, 2004* (PHIPA)? Or does the *Personal Information Protection and Electronic Documents Act* (PIPEDA) apply instead, or as well? Does the answer depend on whether the practitioners are members of a regulated health profession (for example registered massage therapists) or unregulated (for example non-physician osteopathic practitioners)?
2. Given the answer to question 1, does the *Health Care Consent Act, 1996* apply to these treatments? What does that mean for the consent process?

### B. Electronic signature and evidence
3. Does the process in section 2 produce a valid signature under the *Electronic Commerce Act, 2000* (Ontario)? Is it suitable as evidence under the *Evidence Act* (Ontario), including the provisions on electronic records?
4. Is the ninth checkbox, "I agree to sign this document electronically", needed? Is the wording adequate? Please propose wording if not.
5. Are there steps we should add or change to strengthen the evidence? For example, how identity is verified, what is recorded, or how the witness confirms.
6. May the Clinic ask to see a client's **Ontario health card** as identification? We understand there may be restrictions on who can require it.

### C. Content of the forms
7. Please review the consent text. Is it adequate for informed consent to these treatments? Should the spelling errors be corrected, or should the text be kept exactly as the original?
8. Is the attestation page added to the health history form appropriate? Is the wording adequate?
9. The health history form says written permission is required to release information. Do we need a separate written authorisation from each client before providing their forms to their insurer for a claim or an audit? If so, can it be part of this electronic process, and what should it say?
10. The consent states it applies to "all my present and future care". How long can the Clinic rely on it? When should a client be asked to sign again?

### D. Minors and substitute decision-makers
11. What age threshold or capacity assessment should apply? How should consent be obtained for clients who cannot consent themselves? Can a parent, guardian or substitute decision-maker sign electronically in a later version of the system, and what would that require?

### E. Retention and storage
12. How long must the Clinic keep these records, and from when (for example from the last visit, or from age 18 for minors)? We will set the write-once retention period to this value. Please note that once set, it cannot be shortened.
13. Write-once storage means a sealed record cannot be corrected or deleted. How does this fit with clients' rights to access and correct their information, and with any obligation to dispose of records after the retention period? Is recording corrections as a new signed version sufficient?
14. Is storage with Amazon Web Services in its Canada (Central) region acceptable? Do we need agreements with AWS or other service providers (email, SMS, timestamping authority)?

### F. Privacy and security
15. What privacy policies, notices and consent statements should clients see when they fill in the form online?
16. What are the Clinic's obligations if there is a privacy breach (notifying clients, the Information and Privacy Commissioner, or others)? What should our breach-response procedure include?
17. Are our safeguards adequate? These are: encryption, named staff accounts, access logging, no health data in logs, and data in Canada.

### G. Communications
18. Do invitation emails and SMS messages to clients fall under Canada's anti-spam legislation (CASL)? If so, what consent and content (for example an unsubscribe option) are required?

### H. Other
19. Is there anything else in this process that creates legal risk for the Clinic, or that we should change before using it with real clients?

## 4. What we are asking for

- A written opinion on the questions above. Where useful, please give recommended wording for:
  - the consent text;
  - the e-signature agreement;
  - the attestation;
  - the client authorisation to release records to insurers;
  - the privacy notice.
- The retention period to configure.
- A confirmation of the age threshold or an alternative rule.
- An estimate of fees and the expected timeline.

We are happy to demonstrate the process and provide a sample of a sealed form filled in with fictitious data. No real client information has been stored in the system.

Please contact [contact name] at [phone] or [email].

Sincerely,

[Name]
[Title]
SELAH HEAD SPA

Enclosures:
1. Health History Form (current paper version)
2. Consent to Osteopathic Treatment (current paper version)
3. Process summary (optional: excerpt of the system design)
