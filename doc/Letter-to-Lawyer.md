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
2. **Staff prepare the consent details** when the appointment is booked: the practitioner, the treatment areas, and the "present and future care with" entry. The client sees them but cannot edit them.
3. **The client signs both forms by hand** (finger or stylus) in one of two ways. The signature step appears only when the health history is complete and the consent details have been prepared. Before signing, in both cases, the client:
   - reviews their completed form;
   - reads the full consent text (they must scroll to the end before continuing);
   - ticks each of the 8 acknowledgement/understanding statements;
   - ticks a ninth box: "I agree to sign this document electronically";
   - confirms the prepared consent details.

   The two ways are:
   - **(a) In the Clinic, on a Clinic tablet.** A named staff member acts as witness. They check the client's identification in person, record the ID type (driver's licence, health card or passport; never the number), and confirm with a personal PIN.
   - **(b) Remotely, on the client's own phone or computer.** The only identity check at that moment is that the phone number and email address match the Clinic's records. No one-time code is sent and no ID is checked. The IP address and device are recorded. At the client's first visit afterwards, a staff member checks photo ID in person and records that check (ID type and the staff member's PIN). The sealed documents are not changed.
4. **Before treatment, the practitioner records the discussion.** They confirm with their personal PIN that they discussed with the client the four topics the consent refers to: the condition, the nature of the treatment, its risks and benefits, and the alternatives. This matters especially for remote signing, where the client may sign the consent ("I acknowledge I have discussed the following with my healthcare provider") before meeting the practitioner.
5. **At the moment of signing, the system creates PDFs of the original forms, filled in and signed:**
   - The consent form shows the signature and date.
   - The health history form gets an added page, clearly labelled as electronically generated. It contains an attestation ("I confirm that the health history on the previous page is complete and accurate"), the signature, name, date and a record number.
6. **The PDFs are sealed:**
   - a SHA-256 fingerprint is recorded;
   - an RFC 3161 trusted timestamp is obtained from a third-party timestamping authority (only the fingerprint is sent);
   - the files are stored in write-once storage (Amazon S3 Object Lock, compliance mode) in the AWS Canada (Central) region, where they cannot be changed or deleted during the retention period;
   - a tamper-evident, hash-chained log records each step: viewed, confirmed, agreed to sign electronically, signed (in Clinic or remotely), witnessed or later ID-checked, the practitioner's discussion record, sealed, and later downloads and verifications.

   Each record states whether it was signed in the Clinic or remotely.
7. **Updates:** if a client's health information, the planned treatment or the consent wording changes, staff start an update and the client signs a new version, in the Clinic or remotely. Earlier versions are kept.
8. **Clients below a set age** (currently 18, configurable) cannot sign electronically and are directed to a paper process.
9. **Messages** may be sent by email or SMS to clients the Clinic has registered: invitations to fill in the form, and notices that forms are ready to sign or need updating. They contain only the client's first name and a link.
10. **Data storage:** all data is stored in Canada and encrypted. Access is limited to named staff accounts and is logged.

## 3. Questions

### A. Which laws apply
1. Is the Clinic a "health information custodian" under the *Personal Health Information Protection Act, 2004* (PHIPA)? Or does the *Personal Information Protection and Electronic Documents Act* (PIPEDA) apply instead, or as well? Does the answer depend on whether the practitioners are members of a regulated health profession (for example registered massage therapists) or unregulated (for example non-physician osteopathic practitioners)?
2. Given the answer to question 1, does the *Health Care Consent Act, 1996* apply to these treatments? What does that mean for the consent process?

### B. Electronic signature and evidence
3. Does the process in section 2 produce a valid signature under the *Electronic Commerce Act, 2000* (Ontario)? Is it suitable as evidence under the *Evidence Act* (Ontario), including the provisions on electronic records? Please answer separately for signing **in the Clinic** (3a) and **remotely** (3b).
4. **Remote signing identity.** For remote signing, the only identity check is a match of phone number and email address, followed by an in-person ID check at the next visit. Is that sufficient? If someone else signed in a client's name, what would the Clinic's exposure be? Should we add a one-time code sent to the client's phone, or another measure?
5. Is the ninth checkbox, "I agree to sign this document electronically", needed? Is the wording adequate? Please propose wording if not.
6. Are there steps we should add or change to strengthen the evidence? For example, how identity is verified, what is recorded, or how the witness confirms.
7. May the Clinic ask to see a client's **Ontario health card** as identification? We understand there may be restrictions on who can require it.

### C. Content of the forms
8. Please review the consent text. Is it adequate for informed consent to these treatments? Should the spelling errors be corrected, or should the text be kept exactly as the original?
9. **"I acknowledge I have discussed…" with remote signing.** A client who signs remotely may sign this statement before meeting the practitioner. The practitioner then records the discussion before treatment (section 2, step 4). Is that acceptable? Or should the consent wording change for remote signing (for example "I will discuss" or "I have been given the opportunity to discuss"), or should the consent only be signed after the discussion?
10. Staff, not the client, fill in the practitioner and treatment areas, and the client confirms them by signing. Is that acceptable?
11. Is the attestation page added to the health history form appropriate? Is the wording adequate?
12. The health history form says written permission is required to release information. Do we need a separate written authorisation from each client before providing their forms to their insurer for a claim or an audit? If so, can it be part of this electronic process, and what should it say?
13. The consent states it applies to "all my present and future care". How long can the Clinic rely on it? When should a client be asked to sign again?

### D. Minors and substitute decision-makers
14. What age threshold or capacity assessment should apply? How should consent be obtained for clients who cannot consent themselves? Can a parent, guardian or substitute decision-maker sign electronically in a later version of the system, and what would that require?

### E. Retention and storage
15. How long must the Clinic keep these records, and from when (for example from the last visit, or from age 18 for minors)? We will set the write-once retention period to this value. Please note that once set, it cannot be shortened.
16. Write-once storage means a sealed record cannot be corrected or deleted. How does this fit with clients' rights to access and correct their information, and with any obligation to dispose of records after the retention period? Is recording corrections as a new signed version sufficient?
17. Is storage with Amazon Web Services in its Canada (Central) region acceptable? Do we need agreements with AWS or other service providers (email, SMS, timestamping authority)?

### F. Privacy and security
18. What privacy policies, notices and consent statements should clients see when they fill in the form online?
19. What are the Clinic's obligations if there is a privacy breach (notifying clients, the Information and Privacy Commissioner, or others)? What should our breach-response procedure include?
20. Are our safeguards adequate? These are: encryption, named staff accounts, access logging, no health data in logs, and data in Canada.

### G. Communications
21. Do our emails and SMS messages to clients (invitations, "ready to sign" and update notices) fall under Canada's anti-spam legislation (CASL)? If so, what consent and content (for example an unsubscribe option) are required?

### H. Other
22. Is there anything else in this process that creates legal risk for the Clinic, or that we should change before using it with real clients?

## 4. What we are asking for

- A written opinion on the questions above. Where useful, please give recommended wording for:
  - the consent text;
  - the e-signature agreement;
  - the attestation;
  - the client authorisation to release records to insurers;
  - the privacy notice.
- The retention period to configure.
- A confirmation of the age threshold or an alternative rule.
- A clear answer on whether remote signing, as described, may be used, and under what conditions.
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
