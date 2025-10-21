Cloudformation
template to
template structure:
- resource: mandatory, 
- description: free text, if have templateFormatVersion, it must be sam as the templateFormatVersion
-  metadata: control what appear on the AWS console UI
- parameters:  
- mapping: not use much, key/value pair use for look up
- condition: create condition => use condition
- out put: when complete => output sthing 

![[Screenshot 2025-09-07 at 13.07.38.png]]

resource inside template is call logical resourse
stack: contain logical resource
physical resource: the resource that clouformation create from the logical resource
must be sync with the logical resource
delete stack => delete the physiccal resource

cloudformation practise:
it create a s3 bucket with prefix CF to save the template



Cloud Watch
public service
can be used every where
collect data from services are not exposed to AWS is need to install Cloudwatch agent
![[Screenshot 2025-09-07 at 13.51.38.png]]
log: ingest log from all aws product or out side
event: sth like ec2 is terminated, launched,...
![[Screenshot 2025-09-07 at 13.53.39.png]]

 namespace: container , way to seperate things into different areas
 ![[Screenshot 2025-09-07 at 13.57.42.png]]
metric: is a collection of related data points in a time ordered structure

![[Screenshot 2025-09-07 at 14.00.06.png]]
when data point is come from many source => use dimension to separate datapoint
![[Screenshot 2025-09-07 at 14.01.51.png]]

Alarm 
take action based on metric

CLoud Watch Logs
public service
time stamp data
![[Screenshot 2025-09-09 at 7.12.33.png]]
regional service
log stream: ordered set of log events for a specific source of specific thing
log group: containers of multiple log streams, same type of log steam
retention & permisstions apply to log group will be apply into all log steam
metric filter: eg looking for ssh error ...![[Screenshot 2025-09-09 at 7.18.15.png]]

Cloudtrail: 
region serviece
a record of a event of an activity in an AWS account
mng event: mng operations that performed in a AWS resource ( control plane operation ) ( eg : terminate ec2  ) ( on by default )
data event: resource operations that performed in a AWS resource ( control plane operation ) ( eg : obj being uploaded to s3)
![[Screenshot 2025-09-09 at 7.25.09.png]]

global service: log to us east 1
regionl serviec: log to them region
use with the org => log all account in that org
![[Screenshot 2025-09-09 at 7.33.52.png]]

don't have s3 unless config a trail
global serviece => need a trail to log data to us east 1

![[Screenshot 2025-09-10 at 5.28.05.png]]

AWS control tower
lading zone: multi account environment part of control tower
![[Screenshot 2025-09-10 at 6.01.35.png]]
sso: iam identity center
create more account: via control tower console or service catalog
![[Screenshot 2025-09-10 at 6.15.07.png]]![[Screenshot 2025-09-10 at 6.17.45.png

elective: tuỳ chọn
![[Screenshot 2025-09-10 at 6.22.17.png]]

SDLC: software development life cycle
![[Screenshot 2025-09-10 at 6.28.39.png]]
dòng 4: quyền quản trị được give cho 1 user ở iam ic, người đó đăng nhập thông qua iam ic và assume cái role admin đó. k phải root

