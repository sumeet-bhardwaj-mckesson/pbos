# CBOS Configuration Engine Architecture

## Version 1.0

## Purpose

The Configuration Engine is the foundation that allows CBOS to support multiple creative industries without requiring code changes.

The goal is to make CBOS:

```text
Configurable
Metadata Driven
Industry Agnostic
Multi-Tenant
```

while maintaining a stable core platform.

---

# Vision

Every organization should be able to configure:

* Project Types
* Workflows
* Forms
* Fields
* Statuses
* Roles
* Permission Sets
* Business Templates

without developer involvement.

---

# Core Principles

## Principle 1

Everything is metadata.

Business behavior should be represented through configuration whenever possible.

---

## Principle 2

Configuration belongs to organizations.

Each organization may customize its own configuration.

---

## Principle 3

Configuration must be versioned.

Organizations must be able to:

* Draft
* Publish
* Rollback

configurations.

---

## Principle 4

Configuration must be auditable.

Every change must be tracked.

---

# Configuration Architecture

```text
ConfigurationPackage
│
├── ProjectTypes
├── FieldDefinitions
├── StatusDefinitions
├── FormDefinitions
├── WorkflowTemplates
├── RoleTemplates
├── PermissionSets
└── BusinessTemplates
```

---

# Project Type Engine

## Entity

ProjectType

### Attributes

```text
id
organization_id
name
code
description
icon
color
is_active
```

### Examples

Photography:

```text
Wedding
Maternity
Newborn
Family
Corporate Shoot
```

Agency:

```text
Campaign
Content Production
Brand Launch
```

Podcast:

```text
Episode
Season
Interview
```

---

# Custom Field Engine

## FieldDefinition

```text
id
organization_id
entity_name
field_name
field_label
field_type
required
default_value
validation_rules
```

---

## Supported Field Types

```text
text
textarea
number
currency
date
datetime
boolean
select
multi_select
image
file
json
```

---

## FieldOption

```text
id
field_definition_id
value
label
sort_order
```

---

## FieldValue

```text
id
field_definition_id
entity_id
value
```

---

# Status Engine

## StatusDefinition

```text
id
organization_id
entity_name
name
code
color
sort_order
is_terminal
```

---

## Example

Project Statuses:

```text
Draft
Planned
Active
Review
Completed
Archived
```

Lead Statuses:

```text
New
Contacted
Qualified
Won
Lost
```

---

# Form Engine

## FormDefinition

```text
id
organization_id
name
description
entity_name
```

---

## FormField

```text
id
form_id
field_definition_id
display_order
```

---

## FormSubmission

```text
id
form_id
submitted_by
submitted_at
```

---

## Example Forms

```text
Lead Form
Client Intake Form
Shoot Planning Form
Delivery Confirmation Form
```

---

# Workflow Template Engine

## WorkflowTemplate

```text
id
organization_id
name
description
version
```

---

## WorkflowStage

```text
id
workflow_template_id
name
sequence
```

---

## WorkflowTransition

```text
id
source_stage_id
target_stage_id
```

---

## Example

Photography Workflow

```text
Lead
↓
Consultation
↓
Booking
↓
Shoot
↓
Editing
↓
Delivery
```

Agency Workflow

```text
Lead
↓
Proposal
↓
Approval
↓
Production
↓
Review
↓
Publishing
```

---

# Role Template Engine

## RoleTemplate

```text
id
organization_id
name
description
```

Examples:

```text
Photographer
Editor
Sales Executive
Studio Manager
```

---

# Permission Set Engine

## PermissionSet

```text
id
organization_id
name
description
```

---

## PermissionSetItem

```text
id
permission_set_id
permission_code
```

---

## Example

Gallery Manager

```text
Gallery.View
Gallery.Upload
Gallery.Share
Gallery.Download
```

---

# Business Templates

## Purpose

Business Templates provide prebuilt configurations.

---

## Examples

Photography Studio Template

Contains:

```text
Project Types
Forms
Statuses
Roles
Permission Sets
Workflows
```

---

Agency Template

Contains:

```text
Campaign Types
Approval Workflows
Agency Roles
Agency Forms
```

---

Podcast Template

Contains:

```text
Episode Types
Publishing Workflows
Podcast Roles
```

---

# Versioning Strategy

Every configuration entity supports:

```text
Draft
Published
Archived
```

and version history.

---

# Audit Requirements

Every configuration change records:

```text
User
Timestamp
Old Value
New Value
Reason
```

---

# Multi-Tenant Rules

Every configuration entity must contain:

```text
organization_id
```

No organization can access another organization's configuration.

---

# Future Roadmap

Phase 1

```text
Project Types
Custom Fields
Statuses
```

Phase 2

```text
Forms
Roles
Permission Sets
```

Phase 3

```text
Workflow Builder
Business Templates
```

Phase 4

```text
AI Generated Configurations
```

---

# Constitutional Rule

No industry-specific behavior shall be hardcoded when it can be represented through the Configuration Engine.

---

