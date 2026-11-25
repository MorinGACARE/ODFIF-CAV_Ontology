# Connected Autonomous Vehicles Digital Forensics Ontology (CAV-DFO)

Version: 1.1.0

Serialization: OWL / RDF-XML (.owl)

Namespace / Base IRI: http://www.example.org/cav-df-ontology#

Overview

The Connected Autonomous Vehicles Digital Forensics Ontology (CAV-DFO) provides a formal, machine-readable knowledge representation for investigating physical and cyber incidents in Connected Autonomous Vehicles (CAVs). Designed for digital forensic practitioners, researchers, and knowledge engineers, CAV-DFO models vehicle hardware architectures, internal buses, Vehicle-to-Everything (V2X) communications, cybersecurity events, multi-source digital evidence correlation, and legal/ethical constraints.

The ontology enables automated reasoning, structured forensic queries, and multi-line evidence corroboration—linking inculpatory and exculpatory artifacts from internal ECUs, Event Data Recorders (EDRs), Data Storage Systems for Automated Driving (DSSAD), and external Roadside Units (RSUs) to forensic assertions and reports.

Standards & Guidelines Alignment

CAV-DFO is structured to align with international automotive cybersecurity, operational safety, and digital forensics frameworks:

ISO/IEC 27037: Guidelines for identification, collection, acquisition, and preservation of digital evidence.

ISO/SAE 21434: Road vehicles — Cybersecurity engineering (cybersecurity events, threat severity, and attack vectors).

ISO 34503: Road vehicles — Test scenarios for automated driving systems — Specification for operational design domain.

NIST SP 800-86: Guide to Integrating Forensic Techniques into Incident Response (evidence integrity and chain of custody).

NHTSA Automated Driving Recommendations: Guidance on automated driving system data recording and safety operations.

Ontology Architecture (Five Core Sub-Domains)

CAV-DFO organizes domain concepts, object properties, datatype attributes, and illustrative instances across five integrated modules:

Actor Ontology (Actor)

Models human and organizational stakeholders involved in CAV operation, compromise, emergency response, and investigation—including Driver, Occupant, ByStander (Pedestrian), FirstResponder (FirstAider, PoliceOfficer), Investigator, Manufacturer (OEM), Operator (Fleet Operator), and Adversary.

Data Sources & CAV Architecture Ontology (DataSource, AVSystemComponent, DataFile)

Distinguishes InternalDataSource (e.g., ECU, Sensor, CameraSensor, LidarSensor, RadarSensor, UltrasonicSensor, GPSReceiver, InertialMeasurementUnit_IMU, WheelSpeedSensor) from ExternalDataSource (e.g., RoadsideUnit, TrafficControlCenter_ITC, CellularBaseStation_5G_gNB, SecurityCredentialManagementSystem_SCMS, CertificateRevocationList_CRL, GNSS_SatelliteConstellation). Also captures Actuator subclasses, internal/external CommunicationProtocol stacks (CANBus, Ethernet, V2XProtocol), storage systems (EventDataRecorder, DSSAD, NonVolatileMemory, InfotainmentSystem), and granular SAE J2735 / ETSI V2XMessage payloads (BSM, CAM, DENM, SPaT, MAP, PSM, MCM, CPM).

Evidence Correlation & Analysis Ontology (DigitalEvidence, Assertion)

Supports multi-source forensic reasoning by distinguishing InculpatoryEvidence and ExculpatoryEvidence, linking artifacts to ForensicTool, AnalysisMethod (TimelineAnalysis, Reconstruction, HIL_SIL_Simulation), ChainOfCustody, EvidenceIntegrity, and ForensicReport.

Incident & Cybersecurity Ontology (Incident, CybersecurityEvent)

Categorizes physical and cyber occurrences, including PhysicalIncident (VehicleCrash), NearMiss, NonCyberIncident, SensorFusionAnomaly, AttackVector, and CyberAttack subclasses (DenialOfService, Malware, SensorSpoofing, GNSS_Spoofing, GNSS_Jamming, LiDAR_Optics_Dazzling, CAN_Frame_Injection).

Legal & Ethical Ontology (LegalRequirement, EthicalPrinciple)

Captures statutory and normative governance constraints, including LegalAdmissibility, DataPrivacyRegulation (e.g., GDPR/CCPA), Consent, and EthicalPrinciple subclasses (Accountability, Fairness, Transparency).

Repository Contents

CAV-DFO v1.1.0_22Sep2026.owl — Complete OWL/RDF-XML ontology file containing classes, disjointness axioms, bidirectional object properties (owl:inverseOf and owl:SymmetricProperty), owl:unionOf domain/range definitions, datatype properties, and sample forensic scenario instantiations.

README.md — Documentation overview, usage guide, and validation notes.

How to Use

1. Open and Inspect in Protégé

Download or clone this repository, or open the raw .owl URL directly in Protégé (File > Open from URL... or File > Open...).

Navigate to the Active Ontology, Classes, Object Properties, Data Properties, and Individuals by class tabs to explore the taxonomy and scenario instances (such as Crash_Incident_20260315).

2. Run Logical Consistency Checking (HermiT)

In Protégé, select Reasoner > HermiT.

Click Reasoner > Start reasoner (or Synchronize).

Verify that the ontology classifies cleanly with zero inconsistencies and no unsatisfiable classes under owl:Nothing.

3. Query with SPARQL

You can query forensic relationships—such as tracing which digital evidence supports a forensic assertion and from which data source it was acquired—using Protégé's SPARQL Query tab or rdflib:

PREFIX cav: <http://www.example.org/cav-df-ontology#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT ?assertion ?evidence ?source ?format
WHERE {
  ?assertion a cav:Assertion ;
             cav:isSupportedBy ?evidence .
  ?evidence cav:isAcquiredFrom ?source .
  OPTIONAL { ?source cav:hasDataFormat ?format }
}


Quality & FAIR Validation

Structural & Semantic Evaluation (OOPS!): Evaluated against the OntOlogy Pitfall Scanner! (OOPS!), incorporating owl:unionOf for multi-class domains/ranges, explicit owl:inverseOf pairs, owl:disjointWith axioms, and complete rdfs:label / rdfs:comment annotations.

FAIR Assessment (FOOPS!): Hosted via GitHub to provide open HTTP/HTTPS access, versioned IRIs (owl:versionIRI), and structured Dublin Core (dc:title, dc:creator, dc:description) metadata.

Citation

If you use CAV-DFO in your digital forensics research or autonomous vehicle incident analysis, please cite this repository and reference CAV-DFO v1.1.0.
