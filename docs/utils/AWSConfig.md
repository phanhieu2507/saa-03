# AWS Config
- detailed view of the config of aws ressources ( change config => shot )
- used for audit and compliance
- relations over time
- changes over time
- can stream changes and rules notifications to SNS
- per region service but can agreate ( tổng hợp )
## Rules
- run when have new snap shot or scheduled
- check if the system is compliant or not -compliant ? => sent noti to sns
- 
- predefined and customizable
- did i import a bad cert?
### Remediations ( tự sửa)
-  when find a object is non compliant ( by aws config) 
- -> call SSM Automation Document ( runbook) to find how to fix
- runbook is have by default but can custom ( call lambda ....)
- **remediations retries** : number of retry while using run book to fix 
