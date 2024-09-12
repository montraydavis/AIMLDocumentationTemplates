# {{ name }} Documentation

{{ description }}

## Table of Contents
{% if databases %}
- [Databases](#databases)
{% endif %}
{% if schemas %}
- [Schemas](#schemas)
{% endif %}
{% if tables %}
- [Tables](#tables)
{% endif %}
{% if views %}
- [Views](#views)
{% endif %}
{% if stored_procedures %}
- [Stored Procedures](#stored-procedures)
{% endif %}
{% if functions %}
- [Functions](#functions)
{% endif %}
{% if triggers %}
- [Triggers](#triggers)
{% endif %}

{% if databases %}
## Databases

{% for database in databases %}
### {{ database.name }}

{{ database.description }}

{% if database.tables %}
#### Tables
{% for table in database.tables %}
- [{{ table.name }}](#table-{{ table.name|slugify }})
{% endfor %}
{% endif %}

{% if database.views %}
#### Views
{% for view in database.views %}
- [{{ view.name }}](#view-{{ view.name|slugify }})
{% endfor %}
{% endif %}

{% if database.stored_procedures %}
#### Stored Procedures
{% for sp in database.stored_procedures %}
- [{{ sp.name }}](#procedure-{{ sp.name|slugify }})
{% endfor %}
{% endif %}

{% if database.functions %}
#### Functions
{% for func in database.functions %}
- [{{ func.name }}](#function-{{ func.name|slugify }})
{% endfor %}
{% endif %}

{% endfor %}
{% endif %}

{% if schemas %}
## Schemas

{% for schema in schemas %}
### {{ schema.name }}

{{ schema.description }}

{% endfor %}
{% endif %}

{% if tables %}
## Tables

{% for table in tables %}
### <a name="table-{{ table.name|slugify }}"></a>{{ table.name }}

{{ table.description }}

#### Columns

| Name | Data Type | Nullable | Description |
|------|-----------|----------|-------------|
{% for column in table.columns %}
| {{ column.name }} | {{ column.data_type }} | {% if column.is_nullable %}Yes{% else %}No{% endif %} | {{ column.description }} |
{% endfor %}

{% if table.primary_key %}
#### Primary Key
{{ table.primary_key }}
{% endif %}

{% if table.foreign_keys %}
#### Foreign Keys
{% for fk in table.foreign_keys %}
- {{ fk }}
{% endfor %}
{% endif %}

{% if table.indexes %}
#### Indexes
{% for index in table.indexes %}
- {{ index.name }}: {{ index.description }}
{% endfor %}
{% endif %}

{% endfor %}
{% endif %}

{% if views %}
## Views

{% for view in views %}
### <a name="view-{{ view.name|slugify }}"></a>{{ view.name }}

{{ view.description }}

#### Definition
```sql
{{ view.definition }}
```

{% endfor %}
{% endif %}

{% if stored_procedures %}
## Stored Procedures

{% for sp in stored_procedures %}
### <a name="procedure-{{ sp.name|slugify }}"></a>{{ sp.name }}

{{ sp.description }}

#### Parameters
{% if sp.parameters %}
| Name | Data Type | Direction | Description |
|------|-----------|-----------|-------------|
{% for param in sp.parameters %}
| {{ param.name }} | {{ param.data_type }} | {{ param.direction }} | {{ param.description }} |
{% endfor %}
{% else %}
This procedure does not take any parameters.
{% endif %}

#### Definition
```sql
{{ sp.definition }}
```

{% endfor %}
{% endif %}

{% if functions %}
## Functions

{% for func in functions %}
### <a name="function-{{ func.name|slugify }}"></a>{{ func.name }}

{{ func.description }}

#### Parameters
{% if func.parameters %}
| Name | Data Type | Description |
|------|-----------|-------------|
{% for param in func.parameters %}
| {{ param.name }} | {{ param.data_type }} | {{ param.description }} |
{% endfor %}
{% else %}
This function does not take any parameters.
{% endif %}

#### Returns
{{ func.returns }}

#### Definition
```sql
{{ func.definition }}
```

{% endfor %}
{% endif %}

{% if triggers %}
## Triggers

{% for trigger in triggers %}
### {{ trigger.name }}

{{ trigger.description }}

#### Associated Table
{{ trigger.table }}

#### Trigger Type
{{ trigger.type }}

#### Definition
```sql
{{ trigger.definition }}
```

{% endfor %}
{% endif %}
