# SemEval 2024 Task 2: Exploring Label Prediction and Supporting Fact Retrieval

This repository contains the code and results for my project on SemEval 2024 Task 2. I have experimented with various models and approaches to solve the problem of label prediction and supporting fact retrieval from CTR (Clinical Trial Reports). Note that I did not participate in the official competition but took this task as a project to explore different methodologies.

## Approaches and Results

### 1. Fine-tuning GPT-3.5 Turbo

- **Label Prediction F1 Score:** 51%
- **Supporting Facts Retrieval Accuracy:** 37%

### 2. Fine-tuning with Free Models

- **BioBERT:** 47% F1 Score on label prediction
- **Llama2:** Crashed due to insufficient RAM
- **T5-small:** Poor performance

### 3. Artificial Neural Networks (ANN) and Recurrent Neural Networks (RNN)

- **ANN:** 60% F1 Score on label prediction
- **RNN:** Crashed due to insufficient RAM

## Dataset

The dataset contains one \`CT\` (Clinical Trials) folder which holds all clinical trials data in JSON format. Additionally, the \`Complete\_Dataset\` folder includes \`train.json\` and \`Gold\_test.json\` files. I have preprocessed these JSON files and converted them into a CSV file named \`merged\_dataset\_new.csv\`.

You can see the dataset from the [link](https://github.com/ai-systems/nli4ct).

### Data Preprocessing

During preprocessing, I created the following columns in the CSV file:

-\`test\_ID\`

-\`Type\`

-\`Section\_id\`

-\`Primary\_id\`

-\`Secondary\_id\`

-\`Statement\`

-\`Label\`

-\`Primary\_evidence\_index\`: Extracted statements based on the indexes given in \`train.json\`.

-\`Secondary\_evidence\_index\`: Extracted statements based on the indexes given in \`train.json\`.

-\`Reference\_data\`: Extracted all the \`Section\_id\` parts.

### Example Data Structures

### Train Data (JSON)

\`\`\`json {

"5bc844fc-e852-4270-bfaf-36ea9eface3d": {

"Type": "Comparison",

"Section\_id": "Intervention",

"Primary\_id": "NCT01928186",

"Secondary\_id": "NCT00684983",

"Statement": "All the primary trial participants do not receive any oral capecitabine, oral lapatinib ditosylate or cixutumumab IV, in contrast all the secondary trial subjects receive these.",

"Label": "Contradiction",

"Primary\_evidence\_index": [0, 1, 2, 3, 4, 5],

"Secondary\_evidence\_index": [0, 1, 2, 3, 4, 5]     }

 }

### Clinical Trials Data (JSON)

{
"Clinical Trial ID": "NCT00001832",
"Intervention": [
"INTERVENTION 1: ",
"  Abl Cells IV + Cyclophosphamide 30 mg/kg",
"  Phase 1 Cyclophosphamide Dose Escalation: Fludarabine 5x25mg/m^2 + Cyclophosphamide 2x30mg/kg + Cells intravenous (IV)",
"INTERVENTION 2: ",
"  Abl Cells IV + Cyclophosphamide 60 mg/kg",
"  Phase 1 Cyclophosphamide Dose Escalation: Fludarabine 5x25mg/m^2 + Cyclophosphamide 2x60mg/kg + Cells intravenous (IV)"
],
"Eligibility": [
"INCLUSION CRITERIA",
"  Patients must have evaluable metastatic melanoma that is refractory to standard therapy.",
"  Age greater than or equal to 16 years.",
"  Patients of both genders must be willing to practice birth control for four months after receiving the preparative regimen.",
"  Clinical performance status of Eastern Cooperative Oncology Group (ECOG) 0, 1 at entry to the trial and at the time of chemotherapy induction.",
"  Absolute neutrophil count greater than 1000/mm^3.",
"  Platelet count greater than 100,000/mm^3.",
"  Hemoglobin greater than 8.0 g/dl.",
"  Serum alanine aminotransferase (ALT)/aspartate aminotransferase (AST) less than two times the upper limit of normal.",
"  Serum creatinine less than or equal to 1.6 mg/dl.",
"  Total bilirubin less than or equal to 1.6 mg/dl, except for patients with Gilbert's Syndrome who must have a total bilirubin less than 3.0 mg/dl.",
"  More than four weeks must have elapsed since any prior therapy at the time the patient receives the preparative regimen.",
"  Women of child-bearing potential must have a negative pregnancy test because of the potentially dangerous effects of the preparative chemotherapy on the fetus.",
"  Life expectancy of greater than three months.",
"  No steroid therapy required.",
"  Seronegative for human immunodeficiency virus (HIV) antibody. (The experimental treatment being evaluated in this protocol depends on an intact immune system. Patients who are HIV seropositive can have decreased immune competence and thus be less responsive to the experimental treatment and more susceptible to its toxicities.)",
"  Seronegative for hepatitis B antigen.",
"  Patients to receive high dose interleukin 2 (IL-2) must have no active systemic infections, coagulation disorders or other major medical illnesses of the cardiovascular, respiratory or immune system.",
"  Patients who will receive high dose IL-2 as part of the phase I portion of this study or who will be randomized must be eligible to receive high dose IL-2.",
"  Any patient receiving IL-2 must sign a durable power of attorney."
],
"Results": [
"Outcome Measurement: ",
"  Clinical Response",
"  Complete response (CR) is defined as the disappearance of all clinical evidence of disease. Partial response (PR) is a 50% or greater decrease in the sum of the products of perpendicular diameters of all measurable lesions for at least one month. No new lesions may appear, and none may increase. Minor response (MR) is a 25-49% decrease in the sum of the products of the perpendicular diameters of all measurable lesions. Appearance of new lesions following a PR or CR are considered relapses. Patients with progressive disease (PD) and no evidence of stable disease will be taken off study after receiving IL-2.",
"  Time frame: Every three to four weeks after the treatment, for up to 5 years.",
"Results 1: ",
"  Arm/Group Title: Abl Cells IV + Cyclophosphamide 30 mg/kg",
"  Arm/Group Description: Phase 1 Cyclophosphamide Dose Escalation: Fludarabine 5x25mg/m^2 + Cyclophosphamide 2x30mg/kg + Cells intravenous (IV)",
"  Overall Number of Participants Analyzed: 3",
"  Measure Type: Number",
"  Unit of Measure: Participants  Complete Response: 0",
"  Partial Response: 0",
"  Minor Response: 0",
"  Progressive Disease: 0",
"  Mixed Response: 0",
"  No Response: 3",
"Stable Disease: 0",
"Results 2: ",
"  Arm/Group Title: Abl Cells IV + Cyclophosphamide 60 mg/kg",
"  Arm/Group Description: Phase 1 Cyclophosphamide Dose Escalation: Fludarabine 5x25mg/m^2 + Cyclophosphamide 2x60mg/kg + Cells intravenous (IV)",
"  Overall Number of Participants Analyzed: 3",
"  Measure Type: Number",
"  Unit of Measure: Participants  Complete Response: 0",
"  Partial Response: 0",
"  Minor Response: 0",
"  Progressive Disease: 0",
"  Mixed Response: 0",
"  No Response: 3",
"Stable Disease: 0"
],
"Adverse Events": [
"Adverse Events 1:",
"  Total: 0/3 (0.00%)",
"  Lymphocyte count decreased 0/3 (0.00%)",
"  Neutrophil count decreased 0/3 (0.00%)",
"  Thrombotic microangiopathy 0/3 (0.00%)",
"  Disseminated intravascular coagulation 0/3 (0.00%)",
"  Sinus tachycardia 0/3 (0.00%)",
"  Hypotension 0/3 (0.00%)",
"  left ventricular dysfunction 0/3 (0.00%)",
"  Vision blurred 0/3 (0.00%)",
"  General symptom 0/3 (0.00%)",
"Adverse Events 2:",
"  Total: 0/3 (0.00%)",
"  Lymphocyte count decreased 0/3 (0.00%)",
"  Neutrophil count decreased 0/3 (0.00%)",
"  Thrombotic microangiopathy 0/3 (0.00%)",
"  Disseminated intravascular coagulation 0/3 (0.00%)",
"  Sinus tachycardia 0/3 (0.00%)",
"  Hypotension 0/3 (0.00%)",
"  left ventricular dysfunction 0/3 (0.00%)",
"  Vision blurred 0/3 (0.00%)",
"  General symptom 0/3 (0.00%)"
]
}
