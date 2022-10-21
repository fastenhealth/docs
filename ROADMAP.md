# Roadmap


## Phase 1 - Production Accesss

1. [x] Incorporate 
	- See [legal/Corp.md](./legal/Corp.md)
2. [ ] Register Trademark
	- See [legal/INTELLECTUAL_PROPERTY](legal/INTELLECTUAL_PROPERTY.md)
3. [x] Sign up for AWS Activate (funding/credits)
	- 10k credit with Stripe Atlas
	- [ ] Waiting for confirmation⏳  #task
4. [ ] Open Bank account
		- SVB or other Stripe Atlas reccomended #task
		- Chase/BoA/etc
5. [ ] Move all infrastructure to new AWS account
1. Complete AWS Infrastructure Hardening for Lighthouse
	- See [security/REFERENCES.md](security/REFERENCES.md)
2. Configure Github CI for Lighthouse
3. Release source code
	- [x] Fasten on Premise
	- [ ] Fasten Lighthouse (timeline unknown)
4. User Interviews
5. Sign Healthcare provider attestations for Production access
	- Limit to existing healthcare providers
		- Cerner
		- Epic
		- Cigna
		- HealthIT
		- Logica
		- Medicare BlueButton
		- Athena
		- CareEvolution
		- [PATIENT_PORTAL_AND_SOURCES_TESTING](PATIENT_PORTAL_AND_SOURCES_TESTING.md)
6. Release a production capable version of Fasten
7. Coordinate with Designers to begin work on the Fasten UI


#### Phase 1 - Costs
- [ ] register corp
- [ ] buy website
- [ ] trademarking
- [ ] AWS hosting for Lighthouse
	- Offset by AWS Activate credits
- [ ] Legal review of provider attestations

### Phase 2 - Expanding Healthcare Providers

1. Sign CARIN Trust Framework. 
2. User Interviews 
3. Add support for additional healthcare providers
	1. Support HL7
	2. Support FHIR Release 2 (DSTU) (Version 1)
	3. Support FHIR Release 3 (STU) (Version 3)
	4. Support FHIR Release 4 (Version 4) - DONE
	5. Support FHIR Release 4b (Version 4b)
	6. Support FHIR Release 5 (STU) (Version 5)
4. Integrate additional Provider sources (prioritizing those used by Fasten users)
	1. See [PATIENT_PORTAL_AND_SOURCES_TESTING](PATIENT_PORTAL_AND_SOURCES_TESTING.md)
5. Look for Grants & Sponsors
6. Look for EMR System to Partner with (Funding)
7. Add opt-in "tracking" to Fasten On-Prem
	- no healthcare related data, only which pages are being used, and deployed version information
	- Rollbar/User error tracking is probably unavailable due to PII/PHI data


#### Phase 2 - Costs 
- Legal advice
- AWS hosting for Lighthouse
	- Offset by AWS Activate credits


### Phase 3 - Marketing 
1. Communicate with healthcare newsletters
2. Apply for Grants/Sponsors
3. Production mode for more Healthcare Providers
	1. Start asking for marketing callouts/added to documentation
4. User Interviews
5. Redo landing page

### Phase 4 - Monetization
- Cloud version?
- Charge for connection to the Lighthouse?