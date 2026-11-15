# Week 7 — HealthLens: My Health Journey

*Break the Code · Working product notes · November 15, 2026*

> Educational prototype. All examples below are fictional and synthetic. No real patient information, credentials or access tokens belong in this public repository.

## Task 2 — App purpose

**Working name:** HealthLens — My Health Journey  
**Primary user:** A patient managing an ongoing health concern.  
**Starting use case:** Overactive bladder (OAB).

**Problem:** Relevant information is often organized by record type (lab results, diagnostic reports, prescriptions) rather than by the health concern a patient wants to understand or manage. It can be difficult to see investigations, treatments and changes in symptoms together.

**Purpose statement:** My app helps patients manage an ongoing health concern by bringing together relevant clinical records, treatments and symptom trends in one personalized view.

**Design principle:** Organize the experience around what matters to the patient, rather than around the underlying FHIR resource types. Start with one concern and one screen; expand to other concerns only after validating the initial design.

## Task 3 — Information and FHIR resources

| Information needed | Likely FHIR R4 resource | Details to display |
| --- | --- | --- |
| Patient identity | [Patient](https://hl7.org/fhir/R4/patient.html) | Name and birth date |
| Recorded health concern | [Condition](https://hl7.org/fhir/R4/condition.html) | Name, onset date, clinical and verification status |
| Laboratory results | [Observation](https://hl7.org/fhir/R4/observation.html) | Test name/code (e.g., LOINC where available), result, unit, date, reference range when provided |
| Ultrasound report | [DiagnosticReport](https://hl7.org/fhir/R4/diagnosticreport.html) | Examination date, report status, findings/conclusion or report attachment |
| Prescribed treatment | [MedicationRequest](https://hl7.org/fhir/R4/medicationrequest.html) | Medication name, prescribed dosage, prescription date and recorded status |
| Symptom trends | [Observation](https://hl7.org/fhir/R4/observation.html) or [QuestionnaireResponse](https://hl7.org/fhir/R4/questionnaireresponse.html) | Dated symptom frequency, urgency or severity; source of the reported information |
| Patient-reported medication use (later) | [MedicationStatement](https://hl7.org/fhir/R4/medicationstatement.html) | What the patient reports taking and when |
| Personal health goal (later) | [Goal](https://hl7.org/fhir/R4/goal.html) | Patient-defined goal, target and status |

### Design considerations

- An ultrasound report is different from the underlying imaging study. The report is the first priority; support for [ImagingStudy](https://hl7.org/fhir/R4/imagingstudy.html) or viewing image files can come later.
- A prescription does not establish that the patient actually takes the medication.
- Distinguish a clinician-recorded diagnosis from a patient-selected concern. The app must not infer or assert a diagnosis.
- A symptom trend describes reported experience; it does not establish that a treatment caused an improvement.
- Some records contain explicit links to a condition (for example, `MedicationRequest.reasonReference`). Others may not. Initially, allow manual, patient-confirmed associations where necessary, clearly labelled as such.
- Confirm which resources, elements, search parameters, and permissions are available in the course sandbox before implementing live retrieval. Use synthetic data where necessary, clearly marked. No EHR write-back is planned for the MVP.

## Task 4 — One-screen sketch

A single dashboard organized around a selected health concern. The examples are invented and are not treatment recommendations.

| **HealthLens · My Health Journey** |
| :--- |
| **Patient:** Alex Parker (fictional) &nbsp; · &nbsp; **DOB:** 1985-05-12 |
| **Health concern:** Overactive bladder &nbsp; ▾ |
| **MY SYMPTOM TRENDS** — Reported urgency episodes over time |
| Week 1: 8/day · Week 2: 7/day · Week 3: 6/day · Week 4: 5/day (illustrative line chart in the eventual app) |
| **MY INVESTIGATIONS** |
| Bladder ultrasound — Nov 3 · Final report · View findings |
| Urinalysis — Oct 28 · Final result · View details |
| **MY TREATMENTS** |
| Example bladder medication — Nov 4 · Active prescription · View prescribed details |
| *Demo data only. Dates, results and treatments are fictional.* |

### MVP — three essential features

1. Select a health concern and display the information for the authorized patient. Begin with one predefined OAB example.
2. Display the selected concern's relevant investigations and prescribed treatments, with dates and data sources.
3. Visualize dated symptom observations when available; otherwise use clearly labelled synthetic sample data or show an empty state.

### Later

- Daily symptom diary and patient-entered symptom observations.
- Patient-defined goals and progress review.
- Medication-use and adherence tracking.
- Appointment preparation summary and questions to discuss.
- Patient-controlled record sharing using SMART Health Links.
- Additional health concerns, multiple data sources and more advanced suggestions for linking relevant records (with patient review).

### Open Build Hour questions

- Which of Condition, Observation, DiagnosticReport, MedicationRequest and QuestionnaireResponse are actually supported by the teaching FHIR server?
- How should an app associate records with a selected concern when the source data has no explicit condition references?
- Can the sandbox supply repeated symptom observations, or should the first version use synthetic data? What options are available for later patient-entered data without requiring EHR write access?

## Week 7 checklist

- [x] Task 1 — Fork created under [wan-huang/Smart-App](https://github.com/wan-huang/Smart-App).
- [x] Task 2 — Main user, problem and purpose statement defined.
- [x] Task 3 — Initial information and FHIR resource mapping documented.
- [x] Task 4 — One-screen sketch, three MVP features and later ideas documented.

These are working notes, not a commitment to implement every resource or feature. Revise the scope as the teaching environment and user needs become clearer.
