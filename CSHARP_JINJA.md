{# Root document #}
{% macro document() %}
# {{ name }} Documentation

{{ description }}

## Table of Contents
{% if using_directives %}
- [Using Directives](#using-directives)
{% endif %}
{% if global_attributes %}
- [Global Attributes](#global-attributes)
{% endif %}
{% for ns in namespaces %}
- [Namespace: {{ ns.name }}](#namespace-{{ ns.name|slugify }})
{% endfor %}
{% for type in top_level_types %}
- [{{ type.kind|title }}: {{ type.name }}](#{{ type.kind|slugify }}-{{ type.name|slugify }})
{% endfor %}

{% if using_directives %}
## Using Directives

```csharp
{% for directive in using_directives %}
using {{ directive }};
{% endfor %}
```
{% endif %}

{% if global_attributes %}
## Global Attributes

```csharp
{% for attr in global_attributes %}
[assembly: {{ attr }}]
{% endfor %}
```
{% endif %}

{% for ns in namespaces %}
{{ namespace(ns) }}
{% endfor %}

{% for type in top_level_types %}
{{ type_def(type) }}
{% endfor %}
{% endmacro %}

{# Namespace #}
{% macro namespace(ns) %}
## Namespace: {{ ns.name }}

{{ ns.description }}

{% if ns.using_directives %}
### Namespace-specific Using Directives

```csharp
{% for directive in ns.using_directives %}
using {{ directive }};
{% endfor %}
```
{% endif %}

{% for type in ns.types %}
{{ type_def(type) }}
{% endfor %}
{% endmacro %}

{# Type (Class, Interface, Struct, Enum, Delegate, Record) #}
{% macro type_def(type) %}
## {{ type.kind|title }}: {{ type.name }}

{{ type.description }}

{% if type.attributes %}
### Attributes

```csharp
{% for attr in type.attributes %}
[{{ attr }}]
{% endfor %}
```
{% endif %}

```csharp
{{ type.visibility }} {% if type.is_static %}static {% endif %}{{ type.kind }} {{ type.name }}{{ generic_parameters(type.generic_parameters) }}
```

{% if type.is_enum %}
{{ enum_members(type.members) }}
{% elif type.is_delegate %}
{{ delegate_signature(type) }}
{% else %}
{{ type_members(type) }}
{% endif %}

{% if type.examples %}
### Examples

{% for example in type.examples %}
```csharp
{{ example }}
```
{% endfor %}
{% endif %}
{% endmacro %}

{# Generic Parameters #}
{% macro generic_parameters(params) %}
{% if params %}<{{ params|join(', ') }}>{% endif %}
{% endmacro %}

{# Enum Members #}
{% macro enum_members(members) %}
### Enum Members

| Name | Value | Description |
|------|-------|-------------|
{% for member in members %}
| {{ member.name }} | {% if member.value %}{{ member.value }}{% else %}-{% endif %} | {{ member.description }} |
{% endfor %}
{% endmacro %}

{# Delegate Signature #}
{% macro delegate_signature(delegate) %}
### Delegate Signature

```csharp
{{ delegate.return_type }} {{ delegate.name }}({{ parameters(delegate.parameters) }});
```

{% if delegate.parameters %}
#### Parameters

| Name | Type | Description |
|------|------|-------------|
{% for param in delegate.parameters %}
| {{ param.name }} | {{ param.type }} | {{ param.description }} |
{% endfor %}
{% endif %}

{% if delegate.return_description %}
#### Returns

{{ delegate.return_description }}
{% endif %}
{% endmacro %}

{# Type Members (for classes, interfaces, structs, records) #}
{% macro type_members(type) %}
{% if type.fields %}
### Fields

{% for field in type.fields %}
{{ field_def(field) }}
{% endfor %}
{% endif %}

{% if type.properties %}
### Properties

{% for property in type.properties %}
{{ property_def(property) }}
{% endfor %}
{% endif %}

{% if type.methods %}
### Methods

{% for method in type.methods %}
{{ method_def(method) }}
{% endfor %}
{% endif %}

{% if type.events %}
### Events

{% for event in type.events %}
{{ event_def(event) }}
{% endfor %}
{% endif %}

{% if type.indexers %}
### Indexers

{% for indexer in type.indexers %}
{{ indexer_def(indexer) }}
{% endfor %}
{% endif %}

{% if type.operators %}
### Operators

{% for operator in type.operators %}
{{ operator_def(operator) }}
{% endfor %}
{% endif %}

{% if type.constructors %}
### Constructors

{% for constructor in type.constructors %}
{{ constructor_def(constructor) }}
{% endfor %}
{% endif %}

{% if type.destructor %}
### Destructor

{{ destructor_def(type.destructor) }}
{% endif %}

{% if type.nested_types %}
### Nested Types

{% for nested_type in type.nested_types %}
{{ type_def(nested_type) }}
{% endfor %}
{% endif %}
{% endmacro %}

{# Field #}
{% macro field_def(field) %}
#### {{ field.name }}

{{ field.description }}

```csharp
{% if field.attributes %}
{% for attr in field.attributes %}
[{{ attr }}]
{% endfor %}
{% endif %}
{{ field.visibility }} {% if field.is_static %}static {% endif %}{% if field.is_readonly %}readonly {% endif %}{{ field.type }} {{ field.name }}{% if field.initializer %} = {{ field.initializer }}{% endif %};
```
{% endmacro %}

{# Property #}
{% macro property_def(property) %}
#### {{ property.name }}

{{ property.description }}

```csharp
{% if property.attributes %}
{% for attr in property.attributes %}
[{{ attr }}]
{% endfor %}
{% endif %}
{{ property.visibility }} {% if property.is_static %}static {% endif %}{{ property.type }} {{ property.name }} { {{ property.accessors|join('; ') }} }
```

{% if property.examples %}
##### Examples

{% for example in property.examples %}
```csharp
{{ example }}
```
{% endfor %}
{% endif %}
{% endmacro %}

{# Method #}
{% macro method_def(method) %}
#### {{ method.name }}

{{ method.description }}

```csharp
{% if method.attributes %}
{% for attr in method.attributes %}
[{{ attr }}]
{% endfor %}
{% endif %}
{{ method.visibility }} {% if method.is_static %}static {% endif %}{% if method.is_virtual %}virtual {% endif %}{% if method.is_override %}override {% endif %}{{ method.return_type }} {{ method.name }}({{ parameters(method.parameters) }})
```

{% if method.parameters %}
##### Parameters

| Name | Type | Description |
|------|------|-------------|
{% for param in method.parameters %}
| {{ param.name }} | {{ param.type }} | {{ param.description }} |
{% endfor %}
{% endif %}

{% if method.return_description %}
##### Returns

{{ method.return_description }}
{% endif %}

{% if method.examples %}
##### Examples

{% for example in method.examples %}
```csharp
{{ example }}
```
{% endfor %}
{% endif %}

{% if method.local_functions %}
##### Local Functions

{% for local_func in method.local_functions %}
{{ local_function_def(local_func) }}
{% endfor %}
{% endif %}
{% endmacro %}

{# Parameters #}
{% macro parameters(params) %}
{% for param in params %}
{% if param.attributes %}{% for attr in param.attributes %}[{{ attr }}] {% endfor %}{% endif %}{% if param.is_ref %}ref {% endif %}{% if param.is_out %}out {% endif %}{{ param.type }} {{ param.name }}{% if param.default_value %} = {{ param.default_value }}{% endif %}{% if not loop.last %}, {% endif %}
{% endfor %}
{% endmacro %}

{# Local Function #}
{% macro local_function_def(func) %}
###### {{ func.name }}

{{ func.description }}

```csharp
{{ func.return_type }} {{ func.name }}({{ parameters(func.parameters) }})
```

{% if func.parameters %}
Parameters:

| Name | Type | Description |
|------|------|-------------|
{% for param in func.parameters %}
| {{ param.name }} | {{ param.type }} | {{ param.description }} |
{% endfor %}
{% endif %}

{% if func.return_description %}
Returns:

{{ func.return_description }}
{% endif %}
{% endmacro %}

{# Event #}
{% macro event_def(event) %}
#### {{ event.name }}

{{ event.description }}

```csharp
{% if event.attributes %}
{% for attr in event.attributes %}
[{{ attr }}]
{% endfor %}
{% endif %}
{{ event.visibility }} {% if event.is_static %}static {% endif %}event {{ event.type }} {{ event.name }};
```

{% if event.examples %}
##### Examples

{% for example in event.examples %}
```csharp
{{ example }}
```
{% endfor %}
{% endif %}
{% endmacro %}

{# Indexer #}
{% macro indexer_def(indexer) %}
#### Indexer

{{ indexer.description }}

```csharp
{% if indexer.attributes %}
{% for attr in indexer.attributes %}
[{{ attr }}]
{% endfor %}
{% endif %}
{{ indexer.visibility }} {{ indexer.type }} this[{{ parameters(indexer.parameters) }}] { {{ indexer.accessors|join('; ') }} }
```

{% if indexer.parameters %}
##### Parameters

| Name | Type | Description |
|------|------|-------------|
{% for param in indexer.parameters %}
| {{ param.name }} | {{ param.type }} | {{ param.description }} |
{% endfor %}
{% endif %}

{% if indexer.examples %}
##### Examples

{% for example in indexer.examples %}
```csharp
{{ example }}
```
{% endfor %}
{% endif %}
{% endmacro %}

{# Operator #}
{% macro operator_def(operator) %}
#### {{ operator.name }} Operator

{{ operator.description }}

```csharp
{% if operator.attributes %}
{% for attr in operator.attributes %}
[{{ attr }}]
{% endfor %}
{% endif %}
{{ operator.visibility }} static {{ operator.return_type }} operator {{ operator.symbol }}({{ parameters(operator.parameters) }})
```

{% if operator.parameters %}
##### Parameters

| Name | Type | Description |
|------|------|-------------|
{% for param in operator.parameters %}
| {{ param.name }} | {{ param.type }} | {{ param.description }} |
{% endfor %}
{% endif %}

{% if operator.return_description %}
##### Returns

{{ operator.return_description }}
{% endif %}

{% if operator.examples %}
##### Examples

{% for example in operator.examples %}
```csharp
{{ example }}
```
{% endfor %}
{% endif %}
{% endmacro %}

{# Constructor #}
{% macro constructor_def(constructor) %}
#### {{ constructor.name }}

{{ constructor.description }}

```csharp
{% if constructor.attributes %}
{% for attr in constructor.attributes %}
[{{ attr }}]
{% endfor %}
{% endif %}
{{ constructor.visibility }} {{ constructor.name }}({{ parameters(constructor.parameters) }}){% if constructor.base_constructor_args %} : base({{ constructor.base_constructor_args }}){% endif %}
```

{% if constructor.parameters %}
##### Parameters

| Name | Type | Description |
|------|------|-------------|
{% for param in constructor.parameters %}
| {{ param.name }} | {{ param.type }} | {{ param.description }} |
{% endfor %}
{% endif %}

{% if constructor.examples %}
##### Examples

{% for example in constructor.examples %}
```csharp
{{ example }}
```
{% endfor %}
{% endif %}
{% endmacro %}

{# Destructor #}
{% macro destructor_def(destructor) %}
#### ~{{ destructor.name }}

{{ destructor.description }}

```csharp
~{{ destructor.name }}()
```

{% if destructor.examples %}
##### Examples

{% for example in destructor.examples %}
```csharp
{{ example }}
```
{% endfor %}
{% endif %}
{% endmacro %}

{# Main template #}
{{ document() }}
