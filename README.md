# fhir-api-test-framework
**Structure to build:**
```
fhir-api-test-framework/
├── src/
│   ├── test/java/
│   │   ├── api/
│   │   │   ├── PatientApiTests.java
│   │   │   ├── ObservationApiTests.java
│   │   │   ├── EncounterApiTests.java
│   │   │   └── MedicationRequestApiTests.java
│   │   ├── validation/
│   │   │   ├── FHIRResourceValidator.java
│   │   │   └── HIPAAFieldValidator.java
│   │   └── utils/
│   │       ├── FHIRClient.java
│   │       └── TestDataBuilder.java
│   └── resources/
│       ├── testdata/
│       │   └── patient_test_data.json
│       └── config/
│           ├── dev.properties
│           └── staging.properties
├── pom.xml
├── README.md
└── .github/workflows/ci.yml


// PatientApiTests.java — show this in interviews
public class PatientApiTests extends BaseTest {

    @Test(description = "Validate FHIR Patient resource mandatory fields")
    public void testPatientMandatoryFields() {
        Response response = FHIRClient.getPatient("592442");
        
        assertThat(response.statusCode()).isEqualTo(200);
        assertThat(response.jsonPath().getString("resourceType")).isEqualTo("Patient");
        assertThat(response.jsonPath().getString("id")).isNotEmpty();
        // HIPAA validation — SSN should never appear in response
        assertThat(response.asString()).doesNotContain("ssn");
        assertThat(response.asString()).doesNotContain("socialSecurityNumber");
    }

    @Test(description = "Validate Patient search returns Bundle resource type")
    public void testPatientSearchReturnsBundleWithResults() {
        Response response = FHIRClient.searchPatients("family", "Smith");
        
        assertThat(response.jsonPath().getString("resourceType")).isEqualTo("Bundle");
        assertThat(response.jsonPath().getInt("total")).isGreaterThan(0);
    }
}
```

**README must include:**
- Why you built it (real problem context)
- Architecture diagram (draw a simple one using draw.io, export as PNG)
- How to run it
- What FHIR resources are covered
- Sample test report screenshot

**Commit strategy — this is crucial:**
Don't push everything at once. Spread commits over 6-8 weeks. Interviewers look at commit frequency.
```
Week 1: Initial framework setup, base HTTP client
Week 2: Patient resource tests
Week 3: Observation resource tests  
Week 4: HIPAA validation utilities
Week 5: CI/CD pipeline with GitHub Actions
Week 6: README + documentation + test report
