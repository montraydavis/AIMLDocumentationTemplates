# {{name}} Documentation

{{description}}

## Table of Contents
{{#if databases}}
- [Databases](#databases)
{{/if}}
{{#if schemas}}
- [Schemas](#schemas)
{{/if}}
{{#if tables}}
- [Tables](#tables)
{{/if}}
{{#if views}}
- [Views](#views)
{{/if}}
{{#if storedProcedures}}
- [Stored Procedures](#stored-procedures)
{{/if}}
{{#if functions}}
- [Functions](#functions)
{{/if}}
{{#if triggers}}
- [Triggers](#triggers)
{{/if}}

{{#if databases}}
## Databases

{{#each databases}}
### {{name}}

{{description}}

{{#if tables}}
#### Tables
{{#each tables}}
- [{{name}}](#table-{{slugify name}})
{{/each}}
{{/if}}

{{#if views}}
#### Views
{{#each views}}
- [{{name}}](#view-{{slugify name}})
{{/each}}
{{/if}}

{{#if storedProcedures}}
#### Stored Procedures
{{#each storedProcedures}}
- [{{name}}](#procedure-{{slugify name}})
{{/each}}
{{/if}}

{{#if functions}}
#### Functions
{{#each functions}}
- [{{name}}](#function-{{slugify name}})
{{/each}}
{{/if}}

{{/each}}
{{/if}}

{{#if schemas}}
## Schemas

{{#each schemas}}
### {{name}}

{{description}}

{{/each}}
{{/if}}

{{#if tables}}
## Tables

{{#each tables}}
### <a name="table-{{slugify name}}"></a>{{name}}

{{description}}

#### Columns

| Name | Data Type | Nullable | Description |
|------|-----------|----------|-------------|
{{#each columns}}
| {{name}} | {{dataType}} | {{#if isNullable}}Yes{{else}}No{{/if}} | {{description}} |
{{/each}}

{{#if primaryKey}}
#### Primary Key
{{primaryKey}}
{{/if}}

{{#if foreignKeys}}
#### Foreign Keys
{{#each foreignKeys}}
- {{this}}
{{/each}}
{{/if}}

{{#if indexes}}
#### Indexes
{{#each indexes}}
- {{name}}: {{description}}
{{/each}}
{{/if}}

{{/each}}
{{/if}}

{{#if views}}
## Views

{{#each views}}
### <a name="view-{{slugify name}}"></a>{{name}}

{{description}}

#### Definition
```sql
{{definition}}
```

{{/each}}
{{/if}}

{{#if storedProcedures}}
## Stored Procedures

{{#each storedProcedures}}
### <a name="procedure-{{slugify name}}"></a>{{name}}

{{description}}

#### Parameters
{{#if parameters}}
| Name | Data Type | Direction | Description |
|------|-----------|-----------|-------------|
{{#each parameters}}
| {{name}} | {{dataType}} | {{direction}} | {{description}} |
{{/each}}
{{else}}
This procedure does not take any parameters.
{{/if}}

#### Definition
```sql
{{definition}}
```

{{/each}}
{{/if}}

{{#if functions}}
## Functions

{{#each functions}}
### <a name="function-{{slugify name}}"></a>{{name}}

{{description}}

#### Parameters
{{#if parameters}}
| Name | Data Type | Description |
|------|-----------|-------------|
{{#each parameters}}
| {{name}} | {{dataType}} | {{description}} |
{{/each}}
{{else}}
This function does not take any parameters.
{{/if}}

#### Returns
{{returns}}

#### Definition
```sql
{{definition}}
```

{{/each}}
{{/if}}

{{#if triggers}}
## Triggers

{{#each triggers}}
### {{name}}

{{description}}

#### Associated Table
{{table}}

#### Trigger Type
{{type}}

#### Definition
```sql
{{definition}}
```

{{/each}}
{{/if}}
