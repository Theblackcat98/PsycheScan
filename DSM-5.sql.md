```sql
-- Create Disorders table
CREATE TABLE Disorders (
  disorder_id INT PRIMARY KEY,
  uid VARCHAR(50),
  dsm_id VARCHAR(50),
  diagnosis VARCHAR(255),
  more_info_id INT,
  FOREIGN KEY (more_info_id) REFERENCES More_Info(more_info_id)
);

-- Create Diagnosis table
CREATE TABLE Diagnosis (
  diagnosis_id INT PRIMARY KEY,
  disorder_id INT,
  diagnostic_features VARCHAR(255),
  associated_features VARCHAR(255),
  diagnostic_markers VARCHAR(255),
  differential_diagnosis VARCHAR(255),
  comorbidity VARCHAR(255),
  FOREIGN KEY (disorder_id) REFERENCES Disorders(disorder_id)
);

-- Create Diagnostic_Criteria table
CREATE TABLE Diagnostic_Criteria (
  criteria_id INT PRIMARY KEY,
  diagnosis_id INT,
  criteria_description VARCHAR(255),
  FOREIGN KEY (diagnosis_id) REFERENCES Diagnosis(diagnosis_id)
);

-- Create More_Info table
CREATE TABLE More_Info (
  more_info_id INT PRIMARY KEY,
  prevalence VARCHAR(255),
  development_and_course VARCHAR(255),
  risk_and_prognosis_factors VARCHAR(255),
  culture_related_issues VARCHAR(255),
  gender_related_issues VARCHAR(255),
  functional_consequences VARCHAR(255)
);

CREATE TABLE `Disorder`(
  id UUID NOT NULL,
  `name` TINYTEXT NOT NULL,
  `DIS_id` TINYTEXT,
  category SET,
  PRIMARY KEY(id)
) ENGINE = Default;

CREATE TABLE `Diagnosis`(
  `Disorder_id` UUID NOT NULL,
  `Diagnostic Criteria` MEDIUMTEXT,
  `Diagnostic Features` MEDIUMTEXT,
  `Associated Features Supporting Diagnosis` MEDIUMTEXT,
  `Diagnostic Markers` MEDIUMTEXT,
  `Differential Diagnosis` MEDIUMTEXT,
  `Comorbidity` MEDIUMTEXT,
  PRIMARY KEY(`Disorder_id`)
) ENGINE = Default;

  CREATE FULLTEXT INDEX `Diagnosis_ix_1` USING BTREE ON `Diagnosis`
    (`Diagnostic Criteria`) ALGORITHM DEFAULT;
  
CREATE TABLE `More Info`(
  `Disorder_id` UUID NOT NULL,
  `Prevalence` MEDIUMTEXT,
  `Development and Course` MEDIUMTEXT,
  `Risk and Prognosis` MEDIUMTEXT,
  `Culture Related Diagnostic Issues` MEDIUMTEXT,
  `Gender Related Diagnostic Issues` MEDIUMTEXT,
  `Functional Consequences` MEDIUMTEXT,
  PRIMARY KEY(`Disorder_id`)
) ENGINE = Default;

CREATE TABLE `Disorder IDs`
  (`DIS_id` UUID NOT NULL, `GOV_id` TINYTEXT, PRIMARY KEY(`DIS_id`)) COMMENT
  'Points to either the DSM-5 Disorder ID or the Government defined one.';

ALTER TABLE `Diagnosis`
  ADD CONSTRAINT `Disorder_Diagnosis`
    FOREIGN KEY (`Disorder_id`) REFERENCES `Disorder` (id);

ALTER TABLE `More Info`
  ADD CONSTRAINT `Disorder_More Info`
    FOREIGN KEY (`Disorder_id`) REFERENCES `Disorder` (id);

```