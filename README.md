# Early Detection of X
## Scope
### Goal: 
Early detection of X

### Interventions
TBD

### Data

### Analysis to be done
- Predict risk of X in the next Y months
- Baselines: 
  1. current practice
  2. guidelines
- Metric: Precision at top k (:warning: need to determine k based on capacity)
- Fairness metric: TPR disparity by Race, Gender, SES, access, etc.

### Validaton Study
- Select x patients to run a trial
- Measure precision compared to current practice and guidelines

### Ethical Issues
- Fairness
- Privacy
- ...

## Formulation
For every patient who has *been seen* at the hospital in the past *y* years and  has not been diagnosed with X yet, identify the top k who are risk of X in the next z months to refer for clinical interventions. 

## Data Details
### Raw Data

## Analysis Details
We are using Triage to build and select models. Some backlground and tutorials on Triage:
1. [Quick intro to Triage](https://dssg.github.io/triage/quickstart/)
2. [Suggested workflow](https://dssg.github.io/triage/triage_project_workflow/)
3. [Understanding the configuration file](https://dssg.github.io/triage/experiments/experiment-config/#experiment-configuration)
  

### Triage details
#### config files
1. [triage_config.yaml](triage/triage_config.yaml): 

#### Running triage
Triage is installed on the server. It gets data from the postgresql server and runs models based on what we define in the config file above.
To run, type:
``python3 run.py -c configfilename ''

**Choices to Make**
1. replace flag
2. save predictions
3. number of processors to use

### Design Decisions
[Spreadsheet to list different options for design decisions](https://docs.google.com/spreadsheets/d/1NNBnxjeZ1ELEeLgSiNWq1riM1Q7tQL9vgUpvd7FgPzY/edit#gid=0)
1. cohort definition
2. label/outcome definition
3. temporal setup

#### Cohort
1. All patients in the data who have had an encounter in the past 12 months and have not had any eGFRS or any abnormal eGFRs ever. 
2. Exclude patients who had an eGFR in the past 3 months (we don't want them to come back for an eGFR)
3. :warning: Expand to other indicators of prior CKD diagnosis such as prescriptions, diagnosis codes, etc.

#### Outcome to predict / Label - what and how far out?
1. OUD in the next 12 months. 

#### Temporal Decisions
1. how often do we predict? every day, week, month or before an appointment
2. how far out do we predict? 1 year for now

#### Features to create
[Spreadsheet to create feature ideas](https://docs.google.com)

#### Sensitive groups for bias analysis
1. race
2. gender
3. location?
4. prior conditions
5. visit frequency
6. income


## Useful pointers
