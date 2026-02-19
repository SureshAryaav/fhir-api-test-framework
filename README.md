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
