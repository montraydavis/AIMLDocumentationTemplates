# {{name}} Documentation

{{description}}

## Table of Contents
{{#if modules}}
- [Modules](#modules)
{{/if}}
{{#if interfaces}}
- [Interfaces](#interfaces)
{{/if}}
{{#if classes}}
- [Classes](#classes)
{{/if}}
{{#if functions}}
- [Functions](#functions)
{{/if}}
{{#if types}}
- [Types](#types)
{{/if}}
{{#if enums}}
- [Enums](#enums)
{{/if}}
{{#if variables}}
- [Variables](#variables)
{{/if}}

{{#if modules}}
## Modules

{{#each modules}}
### {{name}}

{{description}}

{{#if exports}}
#### Exports
{{#each exports}}
- {{this}}
{{/each}}
{{/if}}

{{/each}}
{{/if}}

{{#if interfaces}}
## Interfaces

{{#each interfaces}}
### {{name}}

{{description}}

{{#if typeParameters}}
#### Type Parameters
{{#each typeParameters}}
- `{{name}}`: {{description}}
{{/each}}
{{/if}}

{{#if properties}}
#### Properties
| Name | Type | Description |
|------|------|-------------|
{{#each properties}}
| {{name}} | `{{type}}` | {{description}} |
{{/each}}
{{/if}}

{{#if methods}}
#### Methods
{{#each methods}}
##### `{{name}}`

{{description}}

{{#if parameters}}
Parameters:
{{#each parameters}}
- `{{name}}`: `{{type}}` - {{description}}
{{/each}}
{{/if}}

Returns: `{{returnType}}`

{{/each}}
{{/if}}

{{/each}}
{{/if}}

{{#if classes}}
## Classes

{{#each classes}}
### {{name}}

{{description}}

{{#if typeParameters}}
#### Type Parameters
{{#each typeParameters}}
- `{{name}}`: {{description}}
{{/each}}
{{/if}}

{{#if constructor}}
#### Constructor
{{#each constructor.parameters}}
- `{{name}}`: `{{type}}` - {{description}}
{{/each}}
{{/if}}

{{#if properties}}
#### Properties
| Name | Type | Description |
|------|------|-------------|
{{#each properties}}
| {{name}} | `{{type}}` | {{description}} |
{{/each}}
{{/if}}

{{#if methods}}
#### Methods
{{#each methods}}
##### `{{name}}`

{{description}}

{{#if parameters}}
Parameters:
{{#each parameters}}
- `{{name}}`: `{{type}}` - {{description}}
{{/each}}
{{/if}}

Returns: `{{returnType}}`

{{/each}}
{{/if}}

{{/each}}
{{/if}}

{{#if functions}}
## Functions

{{#each functions}}
### {{name}}

{{description}}

{{#if parameters}}
#### Parameters
{{#each parameters}}
- `{{name}}`: `{{type}}` - {{description}}
{{/each}}
{{/if}}

Returns: `{{returnType}}`

{{#if example}}
#### Example
```typescript
{{example}}
```
{{/if}}

{{/each}}
{{/if}}

{{#if types}}
## Types

{{#each types}}
### {{name}}

{{description}}

```typescript
type {{name}} = {{definition}};
```

{{/each}}
{{/if}}

{{#if enums}}
## Enums

{{#each enums}}
### {{name}}

{{description}}

| Member | Value | Description |
|--------|-------|-------------|
{{#each members}}
| {{name}} | {{value}} | {{description}} |
{{/each}}

{{/each}}
{{/if}}

{{#if variables}}
## Variables

{{#each variables}}
### {{name}}

{{description}}

Type: `{{type}}`

{{#if initialValue}}
Initial Value: `{{initialValue}}`
{{/if}}

{{/each}}
{{/if}}
