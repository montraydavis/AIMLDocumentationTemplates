{{!-- Root document --}}
{{#*inline "document"}}
# {{name}} Documentation

{{description}}

## Table of Contents
{{#if usingDirectives}}
- [Using Directives](#using-directives)
{{/if}}
{{#if globalAttributes}}
- [Global Attributes](#global-attributes)
{{/if}}
{{#each namespaces}}
- [Namespace: {{name}}](#namespace-{{slugify name}})
{{/each}}
{{#each topLevelTypes}}
- [{{kind}}: {{name}}](#{{slugify kind}}-{{slugify name}})
{{/each}}

{{#if usingDirectives}}
## Using Directives

```csharp
{{#each usingDirectives}}
using {{this}};
{{/each}}
```
{{/if}}

{{#if globalAttributes}}
## Global Attributes

```csharp
{{#each globalAttributes}}
[assembly: {{this}}]
{{/each}}
```
{{/if}}

{{#each namespaces}}
{{> namespace}}
{{/each}}

{{#each topLevelTypes}}
{{> type}}
{{/each}}
{{/inline}}

{{!-- Namespace --}}
{{#*inline "namespace"}}
## Namespace: {{name}}

{{description}}

{{#if usingDirectives}}
### Namespace-specific Using Directives

```csharp
{{#each usingDirectives}}
using {{this}};
{{/each}}
```
{{/if}}

{{#each types}}
{{> type}}
{{/each}}
{{/inline}}

{{!-- Type (Class, Interface, Struct, Enum, Delegate, Record) --}}
{{#*inline "type"}}
## {{kind}}: {{name}}

{{description}}

{{#if attributes}}
### Attributes

```csharp
{{#each attributes}}
[{{this}}]
{{/each}}
```
{{/if}}

```csharp
{{visibility}} {{#if isStatic}}static {{/if}}{{kind}} {{name}}{{> genericParameters}}
```

{{#if isEnum}}
{{> enumMembers}}
{{else if isDelegate}}
{{> delegateSignature}}
{{else}}
{{> typeMembers}}
{{/if}}

{{#if examples}}
### Examples

{{#each examples}}
```csharp
{{this}}
```
{{/each}}
{{/if}}
{{/inline}}

{{!-- Generic Parameters --}}
{{#*inline "genericParameters"}}
{{#if genericParameters}}
<{{#each genericParameters}}{{this}}{{#unless @last}}, {{/unless}}{{/each}}>
{{/if}}
{{/inline}}

{{!-- Enum Members --}}
{{#*inline "enumMembers"}}
### Enum Members

| Name | Value | Description |
|------|-------|-------------|
{{#each members}}
| {{name}} | {{#if value}}{{value}}{{else}}-{{/if}} | {{description}} |
{{/each}}
{{/inline}}

{{!-- Delegate Signature --}}
{{#*inline "delegateSignature"}}
### Delegate Signature

```csharp
{{returnType}} {{name}}({{> parameters}});
```

{{#if parameters}}
#### Parameters

| Name | Type | Description |
|------|------|-------------|
{{#each parameters}}
| {{name}} | {{type}} | {{description}} |
{{/each}}
{{/if}}

{{#if returnDescription}}
#### Returns

{{returnDescription}}
{{/if}}
{{/inline}}

{{!-- Type Members (for classes, interfaces, structs, records) --}}
{{#*inline "typeMembers"}}
{{#if fields}}
### Fields

{{#each fields}}
{{> field}}
{{/each}}
{{/if}}

{{#if properties}}
### Properties

{{#each properties}}
{{> property}}
{{/each}}
{{/if}}

{{#if methods}}
### Methods

{{#each methods}}
{{> method}}
{{/each}}
{{/if}}

{{#if events}}
### Events

{{#each events}}
{{> event}}
{{/each}}
{{/if}}

{{#if indexers}}
### Indexers

{{#each indexers}}
{{> indexer}}
{{/each}}
{{/if}}

{{#if operators}}
### Operators

{{#each operators}}
{{> operator}}
{{/each}}
{{/if}}

{{#if constructors}}
### Constructors

{{#each constructors}}
{{> constructor}}
{{/each}}
{{/if}}

{{#if destructor}}
### Destructor

{{> destructor}}
{{/if}}

{{#if nestedTypes}}
### Nested Types

{{#each nestedTypes}}
{{> type}}
{{/each}}
{{/if}}
{{/inline}}

{{!-- Field --}}
{{#*inline "field"}}
#### {{name}}

{{description}}

```csharp
{{#if attributes}}
{{#each attributes}}
[{{this}}]
{{/each}}
{{/if}}
{{visibility}} {{#if isStatic}}static {{/if}}{{#if isReadonly}}readonly {{/if}}{{type}} {{name}}{{#if initializer}} = {{initializer}}{{/if}};
```
{{/inline}}

{{!-- Property --}}
{{#*inline "property"}}
#### {{name}}

{{description}}

```csharp
{{#if attributes}}
{{#each attributes}}
[{{this}}]
{{/each}}
{{/if}}
{{visibility}} {{#if isStatic}}static {{/if}}{{type}} {{name}} { {{#each accessors}}{{this}}{{#unless @last}}; {{/unless}}{{/each}} }
```

{{#if examples}}
##### Examples

{{#each examples}}
```csharp
{{this}}
```
{{/each}}
{{/if}}
{{/inline}}

{{!-- Method --}}
{{#*inline "method"}}
#### {{name}}

{{description}}

```csharp
{{#if attributes}}
{{#each attributes}}
[{{this}}]
{{/each}}
{{/if}}
{{visibility}} {{#if isStatic}}static {{/if}}{{#if isVirtual}}virtual {{/if}}{{#if isOverride}}override {{/if}}{{returnType}} {{name}}({{> parameters}})
```

{{#if parameters}}
##### Parameters

| Name | Type | Description |
|------|------|-------------|
{{#each parameters}}
| {{name}} | {{type}} | {{description}} |
{{/each}}
{{/if}}

{{#if returnDescription}}
##### Returns

{{returnDescription}}
{{/if}}

{{#if examples}}
##### Examples

{{#each examples}}
```csharp
{{this}}
```
{{/each}}
{{/if}}

{{#if localFunctions}}
##### Local Functions

{{#each localFunctions}}
{{> localFunction}}
{{/each}}
{{/if}}
{{/inline}}

{{!-- Parameters --}}
{{#*inline "parameters"}}
{{#each this}}
{{#if attributes}}{{#each attributes}}[{{this}}] {{/each}}{{/if}}{{#if isRef}}ref {{/if}}{{#if isOut}}out {{/if}}{{type}} {{name}}{{#if defaultValue}} = {{defaultValue}}{{/if}}{{#unless @last}}, {{/unless}}
{{/each}}
{{/inline}}

{{!-- Local Function --}}
{{#*inline "localFunction"}}
###### {{name}}

{{description}}

```csharp
{{returnType}} {{name}}({{> parameters}})
```

{{#if parameters}}
Parameters:

| Name | Type | Description |
|------|------|-------------|
{{#each parameters}}
| {{name}} | {{type}} | {{description}} |
{{/each}}
{{/if}}

{{#if returnDescription}}
Returns:

{{returnDescription}}
{{/if}}
{{/inline}}

{{!-- Event --}}
{{#*inline "event"}}
#### {{name}}

{{description}}

```csharp
{{#if attributes}}
{{#each attributes}}
[{{this}}]
{{/each}}
{{/if}}
{{visibility}} {{#if isStatic}}static {{/if}}event {{type}} {{name}};
```

{{#if examples}}
##### Examples

{{#each examples}}
```csharp
{{this}}
```
{{/each}}
{{/if}}
{{/inline}}

{{!-- Indexer --}}
{{#*inline "indexer"}}
#### Indexer

{{description}}

```csharp
{{#if attributes}}
{{#each attributes}}
[{{this}}]
{{/each}}
{{/if}}
{{visibility}} {{type}} this[{{> parameters}}] { {{#each accessors}}{{this}}{{#unless @last}}; {{/unless}}{{/each}} }
```

{{#if parameters}}
##### Parameters

| Name | Type | Description |
|------|------|-------------|
{{#each parameters}}
| {{name}} | {{type}} | {{description}} |
{{/each}}
{{/if}}

{{#if examples}}
##### Examples

{{#each examples}}
```csharp
{{this}}
```
{{/each}}
{{/if}}
{{/inline}}

{{!-- Operator --}}
{{#*inline "operator"}}
#### {{name}} Operator

{{description}}

```csharp
{{#if attributes}}
{{#each attributes}}
[{{this}}]
{{/each}}
{{/if}}
{{visibility}} static {{returnType}} operator {{symbol}}({{> parameters}})
```

{{#if parameters}}
##### Parameters

| Name | Type | Description |
|------|------|-------------|
{{#each parameters}}
| {{name}} | {{type}} | {{description}} |
{{/each}}
{{/if}}

{{#if returnDescription}}
##### Returns

{{returnDescription}}
{{/if}}

{{#if examples}}
##### Examples

{{#each examples}}
```csharp
{{this}}
```
{{/each}}
{{/if}}
{{/inline}}

{{!-- Constructor --}}
{{#*inline "constructor"}}
#### {{name}}

{{description}}

```csharp
{{#if attributes}}
{{#each attributes}}
[{{this}}]
{{/each}}
{{/if}}
{{visibility}} {{name}}({{> parameters}}){{#if baseConstructorArgs}} : base({{baseConstructorArgs}}){{/if}}
```

{{#if parameters}}
##### Parameters

| Name | Type | Description |
|------|------|-------------|
{{#each parameters}}
| {{name}} | {{type}} | {{description}} |
{{/each}}
{{/if}}

{{#if examples}}
##### Examples

{{#each examples}}
```csharp
{{this}}
```
{{/each}}
{{/if}}
{{/inline}}

{{!-- Destructor --}}
{{#*inline "destructor"}}
#### ~{{name}}

{{description}}

```csharp
~{{name}}()
```

{{#if examples}}
##### Examples

{{#each examples}}
```csharp
{{this}}
```
{{/each}}
{{/if}}
{{/inline}}

{{!-- Helper function to create URL-friendly slugs --}}
{{#*inline "slugify"}}
{{lowercase (replace " " "-" (replace "." "" str))}}
{{/inline}}

{{!-- Main template --}}
{{> document}}
