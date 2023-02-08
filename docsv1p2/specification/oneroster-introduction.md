var introduction=`


# Introduction

The IMS OneRoster&reg;(OR) specification supports securely sharing class rosters and related data between a student information system (SIS) and any other system, typically a content application or learning information system (LMS). The OneRoster standard supports spreadsheet-style (CSV) export-import as well as direct system exchanges using REST APIs. With OneRoster, schools pave the way for digital resources for teaching and learning and eliminate problems before they happen.

Teachers, institutional technical administrators, and suppliers all benefit when OneRoster integrations are implemented. Anyone who takes part in the management of the many and diverse tools and technologies in schools and districts benefit from the consistency and standardization offered by the OneRoster standard.

## Status of this document

This document is the Candidate Final Public release, meaning the technical specification is also in Candidate Final Public status. IMS members are currently working towards successful completion of conformance certification.

IMS strongly encourages its members and the community to provide feedback to continue the evolution and improvement of the OneRoster standard. To join the IMS developer and conformance certification community focused on OneRoster and the other related IMS standards please visit the IMS EduERP alliance online here: [https://www.imsglobal.org/lis/alliance.html](https://www.imsglobal.org/lis/alliance.html)
  
## Where Can I Get Help?
  
If you have questions or need help with implementing OneRoster or achieving conformance certification, here are some available resources:
  
- [Public Forum](https://www.imsglobal.org/forums/ims-global-public-forums-and-resources/learning-information-services-oneroster-public-forum) - for all parties interested in OneRoster.
- [OneRoster Support](https://www.imsglobal.org/forums/ims-affiliate-member-forum/oneroster-support) - for EduERP Alliance, Affiliate, and Contributing Members.
- [OneRoster Developer FAQs](https://support.imsglobal.org/support/solutions/folders/48000346663) - series of articles published by the IMS staff answering frequently asked implementation questions.
- IMS Contributing Members have access to private GitHub repositories and a Slack channel for OneRoster Project Group discussions and collaborations. Contact an IMS staff member to gain access.

<section>
  <h1>Specification</h1>

  <p>The OneRoster (OR) v1p2 Standard documentation is split by it's services and transport protocols.  For REST implementations this is split into an information model document and a REST binding document. For CSV implementations there is one document that describes the data and file structure for CSV file exchange. The information model documents describe the data dictionary and logical data model for the service. The REST binding documents describe the serialization and endpoint definitions for the service. There is also a formal profile for the Gradebook service that enables hierarchical assessments outside of a required class context.</p>

  <h2>REST Documents</h2>
  <ul>
    <li>Rostering Service Documents</li>
      <ul>
        <li>[[[OR-ROS-SM-12]]]</li>
        <li>[[[OR-ROS-RJ-12]]]</li>
      </ul>
    <li>Gradebook Service Documents</li>
    <ul>
      <li>[[[OR-GBK-SM-12]]]</li>
      <li>[[[OR-GBK-RJ-12]]]</li>
      <li>[[[OR-ARP-12]]]</li>
    </ul>
    <li>Resource Service Documents</li>
    <ul>
      <li>[[[OR-RES-SM-12]]]</li>
      <li>[[[OR-RES-RJ-12]]]</li>
    </ul>
  </ul>  
  <h2>CSV Documents</h2>
  <ul>
    <li>[[[OR-CSV-12]]]</li>
  </ul>
  <h2>Supporting Documents</h2>
  <ul>
    <li>[[[OR-IMPL-12]]]</li>
    <li>[[[OR-CERT-12]]]</li>
  </ul>
  
</section>
<section id="conformance">
## Conformance Certification

IMS offers a process for testing the conformance of products using the IMS certification test suite. Certification designates passing a set of tests that verify the standard has been implemented correctly and guarantees a product’s interoperability across hundreds of other certified products. The OneRoster  1.2 Conformance Certification Guide [[OR-CERT-12]] provides details about the testing process, requirements, and how to get started.

Conformance certification is much better than claims of “compliance," since the only way IMS can guarantee interoperability is by obtaining certification for the latest version of the standard. Only products listed in the official <a href="https://imscert.org">IMS Certified Product Directory</a> can claim conformance certification. IMS certification provides the assurance that a solution will integrate securely and seamlessly into an institution's digital learning ecosystem.

In order to become certified a paid IMS membership is necessary. Here's why: while conformance certification provides a "seal" for passing prescribed tests it is much more than that. It is a commitment by a supplier to the IMS community for continuous support for achieving "plug and play" integration.  Certification implies ongoing community commitment to resolve problems, revise implementations and retest as need. For that reason, only IMS Contributing Members, Affiliate Members and Alliance members are eligible to apply for conformance certification. Details and benefits of membership are listed at [https://www.imsglobal.org/imsmembership.html](https://www.imsglobal.org/imsmembership.html).
</section>

## Product Directory Listing

The [IMS Certified Product Directory](https://imscert.org/) is the official listing of products that have passed IMS Global conformance certification testing. Products that are listed in this directory are guaranteed to meet the IMS standards for which they have passed testing. If you experience an integration issue with a product listed here, IMS will work with the supplier to resolve the problem. If a product is NOT listed here it has either not passed IMS testing or its certification has expired.

## Acronyms

The following acronyms are used in this document

| Acronym | Description |
| :--- | :---|
| AfA PNP | Access for All Personal Needs and Preferences |
| BOM | Byte Order Mark |
| CEDS | Common Education Data Standards |
| CSV | Comma Separated Values |
| GUID | Globally Unique Identifier |
| IETF | Internet Engineering Task Force |
| JSON | JavaScript Object Notation |
| LDAP | Lightweight Directory Access Protocol |
| LMS | Learning Management System |
| LTI | Learning Tools Interoperability |
| NCES | National Center for Educational Statistics |
| OR | OneRoster |
| ORCA | OneRoster Consumer API |
| REST | Representational State Transfer |
| RFC | Request For Comment |
| SIS | Student Information System |
| TLS | Transaction Layer Security |
| UTF | Unicode Transformation Format |
| UUID | Universally Unique Identifier |



# OneRoster Interoperability Architecture

Like all IMS specifications, the OneRoster specification describes data in motion i.e. the exchange of information achieved using agreed interoperability. For OneRoster the information being exchanged is contained in three groups:

- Class Rosters - the set of people enrolled on a class at a site and for a set period;
- Gradebooks - the data is broken into results, lineItems (a set of results) and categories (a set of lineItems).
- Resources - to identify the set of resources that are required for a class and/or a course;


OneRoster 1.2 serves as a major upgrade to OneRoster 1.1. This version to the educational content, tool and platform rostering standard and consists of three distinct services available in previous revisions. A brief list of features supported in OneRoster 1.2 are:
- Simplification of workflows by separation into 3 distinct services:

- Multiple transfer options to support multiple system requirements. OneRoster supports transmission through spreadsheet-style CSV templates or through system to system data exchange (REST API)
- Support of sort, filter, and field selection
  
## OneRoster Process Flow
  
OneRoster defines two roles, a Provider and a Consumer. Technical administrators or other users of the CSV will export from the Provider system such as a student information system and import to a consumer system, such as an LMS or a digital text. REST API-based products adopt the same concepts but users are not handling files directly since the exchange is system-to-system. 
![OneRoster Architecture](files/images/fig2p1_architecturev1.jpg "OneRoster Architecture")

## Additional Product Considerations  
When selecting products it is very important to understand what OneRoster product type you are considering purchasing. Will the product be a OneRoster Provider or a OneRoster Consumer?  Or is the product performing an Aggregator service, which is a Consumer of data from one system and Provider of that data to another system?  An Aggregator service usually performs additional value-added services to help make the onboarding and enrollment of students in multiple platforms easier and more efficient. Because of their intermediary role, to be compliant, Aggregator product types must be certified as both Consumers and Providers.

`;