---
title: Observation - uncategorised data
keywords: getcarerecord
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_uncategorisedData_guidance.html
summary: "Guidance for populating and consuming the uncategorised data from GP systems using GP Connect"
---

## What is Categorised Data ##
When a clinician / user of a GP Clinical System records clinical data they may, as part of entering the information, identify what type of information they are recording.

For example, where the clinician uses a GP systems allergy function to record a patient’s allergy information it is explicitly identified in the system as an allergy.

The volume of this categorisation varies between provider systems. For the majority of provider systems, the following types of information are explicitly categorised when they are recorded.
* Allergy
* Appointment
* Consultation
* Demographics
* Diary Entry
* Document
* Flag / Alert
* Immunisation
* Medication and Medical Device
* Problem
* Referral
* Test Request
* Test Result

## What is Uncategorised Data ##
There is data that a clinician / user will enter without identifying what type of information they are recorded. This information is usually entered as either free text or a combination of clinical code(s), values, qualifiers and text.

For example:
* The clinician records the patient’s resting pulse by recording the resting pulse clinical code followed by a value of the patient’s pulse.
* The clinician records that a patient has a sore throat by recording the sore throat clinical code
* The patient records that a patient reports being irritable with their family as a piece of free text

For the majority of provider systems, the following types of information are not explicitly categorised when they are recorded.
* Condition
* Family History
* Observation
* Procedure

Consideration was given to attempting to categorise data using the recorded clinical codes. It was decided not to progress this based on a clinical review of its risks and benefits.

## Uncategorised Data Definition ## 

* Uncategorised data is any item of data in the patient record that does not fit into one of the existing or planned clinical areas defined by GP Connect

## Qualifiers ##

In GP systems, structured records can have additional coded or structured attributes that refine or expand the meaning of the coded element of the record. These additional attributes are commonly known as qualifiers. Structured records may have one or more qualifiers. The qualifiers are used refine the meaning of the coded element of the record. 

Each provider system supports a different set of qualifiers. However, there are three key qualifiers that are common across all provider systems:

* Laterality -	For example: A patient record may have a fracture of the left femur
* Severity -	For example: A patient record may have a severe asthmatic attack
* Episodicity - 	For example: This is the patients first episode of an asthmatic attack

The provider system will translate all of the qualifiers included with the clinical code into human readable text and concatenated them with the text entered by the recorder (placing the qualifiers first) and placing in observation.comment.

## Values ##

Values are any reading or result that is recorded with the uncategorised data.

For example: The uncategorised data 50373000 (Body Height) may have a value of 156cm.


### Single values ###
The majority of uncategorised data that contains values will only have a single value.
In these cases, the value will be exported in observation.value.

### Multiple Values ###
There are some cases where an item of uncategorised data may contain multiple values. 
This happens when:
* There is a single clinical code that describes the uncategorised data as a whole; and
* Each recorded value in the uncategorised data is described by its own clinical code

In these cases, each value will be exported in an instance of observation.component.

## Blood Pressure ##
Where the clinician / user has explicitely chosen the clinical codes to record a blood pressure reading in the provider system, the provider system MUST export the blood pressure reading using as uncategorised data using the clinical codes (or SNOMED CT translations) chosen by the clinician / user.


Where the clinician / user has NOT explicitely selected the clinical codes to record a blood pressure reading in the provider system, the provider system MUST export the blood pressure using the CareConnect Blood Pressure observation:

    https://fhir.hl7.org.uk/STU3/StructureDefinition/CareConnect-BloodPressure-Observation-1



