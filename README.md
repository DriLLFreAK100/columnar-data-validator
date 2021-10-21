# Columnar Data Validator

This mini project is aimed at consolidating a generic Data Validation specification for columnar data, e.g. CSV, Xlsx, etc., open to be implemented in any language.

Below are the areas of emphasis:

- Validation Engine Pipeline
- Validation Rules
- Input Spec
- Output Spec

### Validation Engine Pipeline

---

Find it in *./Validation_Engine_Pipeline.drawio*


### Validation Rules

---

| Name       | Description                        | Params                               |
| ---------- | ---------------------------------- | ------------------------------------ |
| NotEmpty   | Check for value. Cannot be empty   |                                      |
| IsLong     | Check if data can be long type     |                                      |
| IsShort    | Check if data can be short type    |                                      |
| IsInt      | Check if data can be int type      |                                      |
| IsByte     | Check if data can be byte type     |                                      |
| IsDecimal  | Check if data can be decimal type  | - precision<br />- scale             |
| IsDouble   | Check if data can be double type   |                                      |
| IsFloat    | Check if data can be float type    |                                      |
| IsString   | Check if data can be string type   | - size<br />- minSize<br />- maxSize |
| IsBoolean  | Check if data can be boolean type  |                                      |
| IsDateTime | Check if data can be datetime type |                                      |


### Input Spec

---

**rulesets.json**

The file that defines the entire process.

> ```
> {
>   "id": string | Guid,
>   "name": string,
>   "rulesets": [
>     {
>       "ordinal": number,
>       "rules": [
>         {
>           "rule": ValidationRuleName [NotEmpty | IsNumber | IsString | IsBoolean | IsDateTime...],
> 	  "severity": "Warning" | "Error",
> 	  "params"?: ValidationRuleParams
>         },
>         ...
>       ]
>     },
>     ...
>   ]
> }
> ```

**Data Source**

Define the source of data. Application should then handle the ingestion accordingly

- Remote
  - Protocol - FTP, SFTP, HTTP, etc.
  - Url
- Stream

### Output Spec

---

> ```
> {
>   "status": "Success" | "Warning" | "Error",
>   "detail": [
>     {
>       "field": string,
>       "rules": [
>         {
>           "rule": ValidationRuleName [NotEmpty | IsNumber | IsString | IsBoolean | IsDateTime...],
>           "status": "Success" | "Warning" | "Error"
>         },
>         ...
>       ]
>     },
>     ...
>   ]
> }
> ```
