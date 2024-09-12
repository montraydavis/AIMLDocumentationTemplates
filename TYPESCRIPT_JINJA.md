# {{ name }} Documentation

{{ description }}

## Table of Contents
{% if modules %}
- [Modules](#modules)
{% endif %}
{% if interfaces %}
- [Interfaces](#interfaces)
{% endif %}
{% if classes %}
- [Classes](#classes)
{% endif %}
{% if functions %}
- [Functions](#functions)
{% endif %}
{% if types %}
- [Types](#types)
{% endif %}
{% if enums %}
- [Enums](#enums)
{% endif %}
{% if variables %}
- [Variables](#variables)
{% endif %}

{% if modules %}
## Modules

{% for module in modules %}
### {{ module.name }}

{{ module.description }}

{% if module.exports %}
#### Exports
{% for export in module.exports %}
- {{ export }}
{% endfor %}
{% endif %}

{% endfor %}
{% endif %}

{% if interfaces %}
## Interfaces

{% for interface in interfaces %}
### {{ interface.name }}

{{ interface.description }}

{% if interface.type_parameters %}
#### Type Parameters
{% for param in interface.type_parameters %}
- `{{ param.name }}`: {{ param.description }}
{% endfor %}
{% endif %}

{% if interface.properties %}
#### Properties
| Name | Type | Description |
|------|------|-------------|
{% for prop in interface.properties %}
| {{ prop.name }} | `{{ prop.type }}` | {{ prop.description }} |
{% endfor %}
{% endif %}

{% if interface.methods %}
#### Methods
{% for method in interface.methods %}
##### `{{ method.name }}`

{{ method.description }}

{% if method.parameters %}
Parameters:
{% for param in method.parameters %}
- `{{ param.name }}`: `{{ param.type }}` - {{ param.description }}
{% endfor %}
{% endif %}

Returns: `{{ method.return_type }}`

{% endfor %}
{% endif %}

{% endfor %}
{% endif %}

{% if classes %}
## Classes

{% for class in classes %}
### {{ class.name }}

{{ class.description }}

{% if class.type_parameters %}
#### Type Parameters
{% for param in class.type_parameters %}
- `{{ param.name }}`: {{ param.description }}
{% endfor %}
{% endif %}

{% if class.constructor %}
#### Constructor
{% for param in class.constructor.parameters %}
- `{{ param.name }}`: `{{ param.type }}` - {{ param.description }}
{% endfor %}
{% endif %}

{% if class.properties %}
#### Properties
| Name | Type | Description |
|------|------|-------------|
{% for prop in class.properties %}
| {{ prop.name }} | `{{ prop.type }}` | {{ prop.description }} |
{% endfor %}
{% endif %}

{% if class.methods %}
#### Methods
{% for method in class.methods %}
##### `{{ method.name }}`

{{ method.description }}

{% if method.parameters %}
Parameters:
{% for param in method.parameters %}
- `{{ param.name }}`: `{{ param.type }}` - {{ param.description }}
{% endfor %}
{% endif %}

Returns: `{{ method.return_type }}`

{% endfor %}
{% endif %}

{% endfor %}
{% endif %}

{% if functions %}
## Functions

{% for function in functions %}
### {{ function.name }}

{{ function.description }}

{% if function.parameters %}
#### Parameters
{% for param in function.parameters %}
- `{{ param.name }}`: `{{ param.type }}` - {{ param.description }}
{% endfor %}
{% endif %}

Returns: `{{ function.return_type }}`

{% if function.example %}
#### Example
```typescript
{{ function.example }}
```
{% endif %}

{% endfor %}
{% endif %}

{% if types %}
## Types

{% for type in types %}
### {{ type.name }}

{{ type.description }}

```typescript
type {{ type.name }} = {{ type.definition }};
```

{% endfor %}
{% endif %}

{% if enums %}
## Enums

{% for enum in enums %}
### {{ enum.name }}

{{ enum.description }}

| Member | Value | Description |
|--------|-------|-------------|
{% for member in enum.members %}
| {{ member.name }} | {{ member.value }} | {{ member.description }} |
{% endfor %}

{% endfor %}
{% endif %}

{% if variables %}
## Variables

{% for variable in variables %}
### {{ variable.name }}

{{ variable.description }}

Type: `{{ variable.type }}`

{% if variable.initial_value %}
Initial Value: `{{ variable.initial_value }}`
{% endif %}

{% endfor %}
{% endif %}
