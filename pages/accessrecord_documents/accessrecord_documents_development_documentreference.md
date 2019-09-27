---
title: DocumentReference
keywords: structured design
tags: [design,structured]
sidebar: accessrecord_documents_sidebar
permalink: accessrecord_documents_development_documents.html
summary: "Guidance for populating and consuming the DocumentReference resource"
div: resource-page
---

## Introduction ##

The headings below list the elements of the DocumentReference resource and describe how to populate and consume them.

{% include important.html content="Any element not specifically listed below **SHOULD NOT** be populated or consumed." %}

{% include tip.html content="You'll find it helpful to read it in conjunction with the [DocumentReference profile definition](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-DocumentReference-1)." %}

## DocumentReference elements ##

### id ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Id</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The logical identifier of the DocumentReference resource.


### meta.profile ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>uri</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..*</td>
  </tr>
</table>

The DocumentReference profile URL.

Fixed value [https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-DocumentReference-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-DocumentReference-1)

### masterIdentifier ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Id</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

Master Version Specific Identifier

### identifier ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Identifier</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..*</td>
  </tr>
</table>

This is for business identifiers.
This is sliced to include a cross-care setting identifier which **MUST** be populated. The codeSystem for this identifier is  `https://fhir.nhs.uk/Id/cross-care-setting-identifier`.
This **MUST** be a GUID.

_Providing_  systems **MUST** ensure this GUID is globally unique and a persistent identifier (that is, it doesn’t change between requests and, therefore, is stored with the source data).

Where  _consuming_  systems are integrating data from this resource to their local system, they **MUST** also persist this GUID at the same time.

### status ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>code</code></td>
  </tr>
</table>

current | superseded | entered-in-error
This field will always have default value of current as only the latest version of the document is retrieved.

### type ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>codeableConcept</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Kind of document.

### subject ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Patient)</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

A reference to the patient who is the subject of the document.

### created ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> DateTime</td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

Creation/Edit datetime of the document.

### indexed ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Instant</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

When the document reference was created.

### author ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>dateTime</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

Who and/or what authored the document.


### custodian ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Organisation)</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

Organisation which maintains this document.


### description ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>string</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

Human-readable description (title).

### content.attachment.data ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>base64Binary</code></td>
    <td><b>Optionality:</b> Required/Optional</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

### content.attachment.url ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>url</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

URL to retrieve the document, this **MUST** be populated when the document is available.

### content.attachment.size ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>unsignedInt</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Size of the file.

The binary file (base64 binary). </br>
This field will get populated only when the document is being retrieved. It will **NOT** be populated during the search document function.

### content.attachment.title ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>string</code></td>
    <td><b>Optionality:</b> Optional</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

To be used when only a placeholder for a document is available. This **MUST** be populated with the reason why the file isn't available.

### content.format ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>coding</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Format/content rules for the document.


### context.encounter ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(CareConnect-GPC-Encounter-1)</code></td>
    <td><b>Optionality:</b> Required/Optional</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

Reference to the consultation the document was created/attached in.

### context.practiceSetting ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>codeableConcept</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

Additional details about where the content was created (for example, clinical specialty).

### context.sourcePatientInfo ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b><code>Reference(CareConnect-GPC-Patient-1)</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

Patient demographics from source.
