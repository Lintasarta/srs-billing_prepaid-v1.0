# Non-Functional Requirements

| ID | Requirement | Needs |
|---|---|---|
| NF-001 | Availability | The system must be available 24 hours a day, 7 days a week. |
| NF-002 | Language | All text displayed in the user interface must be in English. |
| NF-003 | Data Integrity | All billing, payment, and contract information must be accurately stored and auditable. All changes to billing terms must be logged. |
| NF-004 | Security | Uploaded contract documents must be stored securely and accessible only to authorized personnel (Product Manager, Superadmin) and the customer. |
| NF-005 | Scalability | The system must be able to handle a growing number of postpaid customers, projects. |
| NF-006 | Pricing Model Transparency | The system SHALL provide a transparent calculation model for resource usage costs, detailing calculation parameters including Container Run Duration (Hours), CPU Allocation (vCPU), RAM Allocation (GiB), and Node Information (e.g., nvidia.com.gpu_type.h100). |
| NF-007 | Unit Pricing Definition | The system SHALL define and apply clear unit pricing for all measured resources: CPU Cost ($/CPU-Hour), RAM Cost ($/GiB-Hour), and GPU Cost ($/Hour). |
