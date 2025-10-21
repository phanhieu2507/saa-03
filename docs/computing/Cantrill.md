
ec2 
run in private aws zone
az resilent - az fail => instance fails
ondemand billing - per second
local on host storage - ebs

state of instance :
- running ( charge cpu, memory, storage, network) -> stopped ( only charge the ebs ) -> terminated ( non reverve)

AMI:
AMI -> EC2 -> AMI 
AMI contain
1.  permission
- attached permission ( who can acess AMI)
- can be public 
- owner only
- explicit account 
2. root volume
- C drive in window , root volumn in linux
- have at least 1 boot volumn
3. block device mapping
-  mapping the volumn and the operation system
Connect to EC2:
- 3389 port is remote desktop protocol, 22 is ssh for linux
-  linux is connect using ssh key pair, set up when launch instance
- key pair include 2 part: public and private
- with window: use private key to access the remote desktop protocol, then use username and password
- 
Practise EC2:
- key pair only download 1
- when download key pair is shared to all user of the computer => need to expcily permission using command chmod 400 keypair.pem

Virtualization
- Privileged mode = gần như “root trên host”.
- system wide error: loi toan he thong
- 
![[Screenshot 2025-09-15 at 10.36.03.png]]
instance can have multiple network interface, event in difference subnet

![[Screenshot 2025-09-15 at 10.41.12.png]]
specific requirement => ec2
![[Screenshot 2025-09-15 at 10.44.15.png]]

ec2 instance type
![[Screenshot 2025-09-15 at 10.49.21.png]]

![[Screenshot 2025-09-15 at 13.16.10.png]]![[Screenshot 2025-09-15 at 13.19.19.png]]

storage refresher
![[Screenshot 2025-09-15 at 13.32.41.png]]![[Screenshot 2025-09-15 at 13.35.57.png]]

IO size: is the size of the blocks of data that you are writing to disk
want to write 64kb but block size is 16 => use 4 block
IOPS: number of the IO that system can perform in a second
through put: is the rate of data a storage system can store on a particular piece of storage

![[Screenshot 2025-09-15 at 13.43.22.png]]EBS
take snapshot => save to s3 => replicated into different AZ
![[Screenshot 2025-09-15 at 13.48.39.png]]

can copy snapshot to another region
![[Screenshot 2025-09-15 at 13.51.31.png]]

General perpose SSD
- I/O credit là gì?
    
    - Là đơn vị “ngân sách” hiệu năng (thường đo bằng IOPS hoặc throughput) mà một volume/thiết bị tích lũy theo thời gian khi chạy dưới ngưỡng cơ bản, và tiêu khi bạn bùng nổ (burst) vượt ngưỡng đó.
    - Nhờ có credit, hệ thống cho phép “bùng nổ ngắn hạn” để đáp ứng tải đột biến mà không phải trả phí cho mức hiệu năng cao liên tục.
gp2:
base line 3 iops tren 1 gb ( toi thieu 100iops = 300mb)
gp2 burst up to 3000 iops
- Công thức gp2: baseline = max(3 IOPS/GB, 100 IOPS), và bị chụp trần ở 16,000 IOPS.
    - Ví dụ:
        - 1 GB → 3 IOPS theo 3×GB, nhưng vì sàn tối thiểu 100 IOPS, baseline thực tế = 100 IOPS.
        - 100 GB → 300 IOPS.
        - 1,000 GB (≈1 TB) → 3,000 IOPS.
        - 5,334 GB → 16,002 IOPS theo công thức, nhưng bị giới hạn ở 16,000 IOPS.
![[Screenshot 2025-09-15 at 14.04.28.png]]
gp3:
everything above 3000 iops not get automatically => extra cost
with gp2, volumn up => iops up
![[Screenshot 2025-09-15 at 14.10.35.png]]

provisoned iops ssd

per instance performance:   (hiệu năng theo từng instance) là các giới hạn tối đa mà một máy ảo EC2 đơn lẻ có thể nhận được từ EBS, bất kể mỗi volume có thông số cao đến đâu.
use when: low latency, consistent latency ... low volumn but high performance
![[Screenshot 2025-09-15 at 14.33.47.png]]

HDD based
IOPS is low but IO size is high ( 1MB ) => throughput high
st1, sc1 have baseline like gp2 => can burst
![[Screenshot 2025-09-15 at 14.42.48.png]]

instance store volumn
![[Screenshot 2025-09-15 at 15.05.26.png]]
size phu thuoc vao instance size
![[Screenshot 2025-09-15 at 15.16.12.png]]

instanstore vs ebs

![[Screenshot 2025-09-15 at 15.18.42.png]]![[Screenshot 2025-09-15 at 15.21.36.png]]

ebs snapshot
perfomance is not affected while snap shot
snapshot can be in another AZ

![[Screenshot 2025-09-15 at 15.25.46.png]]
full and incremental snap shot is linked
![[Screenshot 2025-09-15 at 15.35.39.png]]

restore from snapshot => get data from snapshot in s3 => slow
per region can create 50 fast snapshot restore
![[Screenshot 2025-09-15 at 15.41.15.png]]

charge: ebs allocated size, snapshot: the size used
![[Screenshot 2025-09-15 at 15.43.59.png]]

ebs practise: 
tag: indentify from other volumn
device name : how the volume is going to exposed to the ec2 instance
raw block device => need to create a file system => mount 

instance store practice
choose the instance type => have instance volumn or not
after reboot => the file still in the instance store, meaning that reboot doesnt change the ec2 host
after stop and start => public ip is changed, ec2 move to another ec2 host, data is cleared

EBS enscription
![[Screenshot 2025-09-15 at 16.47.47.png]]
![[Screenshot 2025-09-15 at 16.50.31.png]]


Network interface, Instance IPs and DNS
ENI: elastic network interface, any instance has atleast one. ( primary interface ). can have more than 1 ENI
security group is attach to ENI, not the instance
Mac visible in the OS
elastic IP address is different to the public IP address
secondary ENI can attach to another ec2 instance
“Source/destination check” trên `ENI` (Elastic Network Interface) là một thuộc tính của card mạng ảo trong EC2 dùng để kiểm tra rằng gói tin do instance gửi ra có nguồn là địa chỉ IP của chính ENI đó, và gói tin đi vào có đích là địa chỉ IP của ENI đó.

- Khi bật source/destination check (mặc định bật):
    
    - Instance/ENI chỉ được phép gửi gói có địa chỉ nguồn là IP của mình và chỉ nhận gói có địa chỉ đích là IP của mình.
    - Điều này đúng cho hầu hết máy chủ thông thường vì chúng chỉ xử lý lưu lượng của chính nó.
- Khi tắt source/destination check:
    
    - ENI có thể chuyển tiếp lưu lượng không phải của chính nó (IP khác IP của ENI).
    - Cần thiết cho các trường hợp instance đóng vai trò router/NAT/Firewall/Load balancer tự quản trị, VPN appliance, IDS/IPS, hoặc khi làm bastion/forwarder Layer 3.
    - Ví dụ phổ biến: NAT instance (không phải NAT Gateway) cần tắt source/dest check để chuyển tiếp lưu lượng từ subnet private ra Internet.
![[Screenshot 2025-09-15 at 21.24.07.png]]
elastic IP remove the public IP v4 replace with the elastic IP
![[Screenshot 2025-09-15 at 21.31.55.png]]

can detach and attach secondary instance to new instance, => move licence
alway config eni with private ipv4
![[Screenshot 2025-09-15 at 21.46.34.png]]

AMI
Market place: can have extra cost ( instance cost + commercial cost)
default that only your account can access ami
create ami => create snap shot of all ebs attach to it
when copy ami to another region => bring the snapshot too
can not use one AMI to many region
can change the AMI permission to snapshot
if share to people in the org => check the " ". 
create instance => need boot volumn => need create volumn from snapshot => grant permisstion bcs the snap shot is your
can share to accoutn in ORG, share to OU ...
![[Screenshot 2025-09-18 at 7.51.29.png]]
![[Screenshot 2025-09-15 at 21.54.34.png]]

block device mapping: table of data, link the snapshot ID to ỏiginal volumn
![[Screenshot 2025-09-15 at 22.16.02.png]]
AMI baking:  ![[Screenshot 2025-09-15 at 22.19.46.png]]

charge: AMI contain snapshot => being charged

EC2 Purchase Options
![[Screenshot 2025-09-16 at 21.47.26.png]]
![[Screenshot 2025-09-16 at 21.51.28.png]]
những cái gì có thể chia nhỏ , khởi động lại => dùng spot được 

reserved
matching instance => reserved
purchase for a particular type of instance, and locked to an AZ specifically or to a region
lock to AZ: only get benefit when launching instance into that AZ, but it also reserve capacity
purchase reservation for a region: doesnt reserve capacity, but any instance in that region can have benefit
reserve capacity: 

parrtial coverage of larger instance
nếu bạn có RI cho size nhỏ hơn, nó vẫn giúp giảm giá một phần cho instance lớn hơn trong cùng family, theo tỉ lệ normalized units; phần chưa được cover vẫn tính giá on-demand trừ khi có thêm RI/SP khác bù vào.
All Upfront và No Upfront là hai tùy chọn thanh toán cho EC2 Reserved Instances (RI) hoặc Savings Plans. Khác nhau chính:

- All Upfront
    
    - Bạn trả toàn bộ chi phí cam kết cho kỳ hạn (1 năm hoặc 3 năm) ngay khi mua.
    - Không hoặc gần như không có khoản phải trả theo giờ sau đó (đối với RI chuẩn/convertible, phần lớn là 0$/giờ; với Savings Plans All Upfront thì tiền đã trả bao phủ toàn bộ cam kết).
    - Tổng chi phí hiệu dụng (effective hourly) thường thấp nhất trong các tùy chọn thanh toán, tức mức giảm giá cao nhất so với On-Demand.
    - Ưu điểm: tiết kiệm tối đa, không phát sinh chi phí theo giờ ngoài phần vượt cam kết (nếu là Savings Plans).
    - Nhược điểm: yêu cầu dòng tiền lớn ban đầu, ít linh hoạt tài chính.
- No Upfront
    
    - Không trả trước khi mua; bạn sẽ bị tính phí theo giờ trong suốt thời hạn cam kết.
    - Tổng chi phí hiệu dụng cao hơn so với All Upfront (giảm giá thấp hơn), nhưng không cần vốn trả ngay.
    - Dễ quản trị dòng tiền, phù hợp nếu bạn muốn trải chi phí theo thời gian.
    - Lưu ý: bạn vẫn bị ràng buộc cam kết toàn kỳ hạn (1/3 năm); không hủy giữa chừng.![[Screenshot 2025-09-18 at 6.46.14.png]]

Dedicated host:
for license base
![[Screenshot 2025-09-18 at 6.52.01.png]]
![[Screenshot 2025-09-19 at 7.34.07.png]]

![[Screenshot 2025-09-19 at 21.35.28.png]]![[Screenshot 2025-09-19 at 21.38.54.png]]

capacity reservations dont have any billing benefit

saving plan
reservation of general compute: ec2, fargate, lambda![[Screenshot 2025-09-19 at 21.42.52.png]]

instance status checks and autorecovery

2 status check: system status, instance status
![[Screenshot 2025-09-19 at 22.06.55.png]]
instan recover only work with the instance which have ebs attached, dont work with instance volumn
shutdown, terminate & termination:
instance setting => termination protection, need grand role for disable termination protection

![[Screenshot 2025-09-20 at 6.43.50.png]]

off host session: session save on another place
![[Screenshot 2025-09-20 at 6.58.02.png]]


Instance Metadata
![[Screenshot 2025-09-20 at 8.08.22.png]]
ipv6 is public => can see in the instance
Bootstrapping EC2 using user data
![[Screenshot 2025-09-21 at 14.14.30.png]]

![[Screenshot 2025-09-21 at 14.15.58.png]]

if can not run userdata => instance still available

![[Screenshot 2025-09-21 at 14.18.17.png]]

![[Screenshot 2025-09-21 at 14.22.49.png]]
baking: can not change but plus bootstrapping can change some of data
userdata practice:
if user data has been encoded => check the user data has been encoded when create ec2
CloudFormation::init
how you can pass complex bootstrapping instruction into ec2 instance
![[Screenshot 2025-09-21 at 15.16.45.png]]
can work many time
![[Screenshot 2025-09-21 at 15.20.01.png]]
creation policy: set the time out to wait after the instance is complete => run the config success
cfn signal: the signal of the cfn init
ec2 instance role
instanceprofile: is the thing that allow the permissions to get inside the instance
use the CFN, need to define seperately
![[Screenshot 2025-09-21 at 16.21.36.png]]
![[Screenshot 2025-09-21 at 16.25.52.png]]

Container


![[Screenshot 2025-09-21 at 8.47.18.png]]
docker image is how we create docker container
docker container has additional read-write file system layer
each container use the same  image , but r/w layer is different![[Screenshot 2025-09-21 at 8.58.21.png]]

container registry
is a registry or a hub of container images
![[Screenshot 2025-09-21 at 9.03.35.png]]

container and images are super light weight
containers run as a precoss in the host operating system
![[Screenshot 2025-09-21 at 9.14.26.png]]
docker engine: thing that allow docker container run on ec2

ecs
cluster where the container run
task can have one or many container
task definition store the resource used by the task ( cpu, memmory), networking mode, capacity
also store task role: iam role that a task can assume
service definition: config the ecs service. a service definition define a service
service: is how we want a task to scale, how many copies we'd like to run. can add capacity and resilience

![[Screenshot 2025-09-21 at 12.22.49.png]]

![[Screenshot 2025-09-21 at 12.29.04.png]]
ecs cluster types
ec2 mode
ecs management components: handle high level task: scheduling, orchestration, cluster management. exist in both ec2 mode and fargate mode
can use the reserver, and the spot instance
![[Screenshot 2025-09-21 at 12.37.39.png]]
fargate mode
aws maintain a shared fargate infra platform
task and service is run in a shared platform, then injected into VPC
in vpc have eni => use this eni to access the fargate

price conscious co y thuc ve gia ca

![[Screenshot 2025-09-21 at 12.48.25.png]]![[Screenshot 2025-09-21 at 12.48.42.png]]

ecr
tag must be unique inside the repository
![[Screenshot 2025-09-21 at 13.19.01.png]]![[Screenshot 2025-09-21 at 13.20.57.png]]

EKS
![[Screenshot 2025-09-21 at 13.53.19.png]]
one pod can have many container by usually 1
pod are nonpermanent
![[Screenshot 2025-09-21 at 14.00.26.png]]![[Screenshot 2025-09-21 at 14.02.54.png]]
EKS
![[Screenshot 2025-09-21 at 14.06.33.png]]![[Screenshot 2025-09-21 at 14.08.22.png]]

Lambda

![[Screenshot 2025-10-02 at 7.09.55.png]]
lambda is state less 
everytime run, a new environment is created
cpu scale despite on the memory
![[Screenshot 2025-10-02 at 22.12.14.png]]![[Screenshot 2025-10-02 at 22.13.39.png]]![[Screenshot 2025-10-03 at 6.37.00.png]]![[Screenshot 2025-10-03 at 6.42.43.png]]![[Screenshot 2025-10-03 at 6.43.26.png]]

resource policy can not change using console UI![[Screenshot 2025-10-03 at 6.48.10.png]]![[Screenshot 2025-10-03 at 6.50.47.png]]![[Screenshot 2025-10-03 at 7.07.55.png]]![[Screenshot 2025-10-03 at 7.11.03.png]]
lambda doesnt need permissios to the source service, unless it actually wants to read more data from that source

![[Screenshot 2025-10-03 at 7.17.27.png]]![[Screenshot 2025-10-03 at 7.19.33.png]]

can define sth outside lambda to decrease the start time of lambda
![[Screenshot 2025-10-03 at 7.23.33.png]]

Cloudwatch event and event bridge

event bus is a stream of events which occur from any supported service inside that aws account

![[Screenshot 2025-10-04 at 14.22.54.png]]![[Screenshot 2025-10-04 at 14.25.12.png]]
![[Screenshot 2025-10-04 at 14.47.35.png]]
can sche dule event bridge
SNS
![[Screenshot 2025-10-04 at 16.38.39.png]]![[Screenshot 2025-10-04 at 16.39.07.png]]

Step function
![[Screenshot 2025-10-04 at 21.09.32.png]]![[Screenshot 2025-10-05 at 9.17.49.png]]![[Screenshot 2025-10-05 at 9.21.31.png]]
API gate way
![[Screenshot 2025-10-05 at 10.04.50.png]]![[Screenshot 2025-10-05 at 10.16.53.png]]![[Screenshot 2025-10-05 at 10.21.19.png]]![[Screenshot 2025-10-05 at 10.28.22.png]]![[Screenshot 2025-10-05 at 10.32.11.png]]![[Screenshot 2025-10-05 at 10.34.36.png]]![[Screenshot 2025-10-05 at 10.36.10.png]]
SQS 

![[Screenshot 2025-10-05 at 10.45.32.png]]
fifo queue can not scale
![[Screenshot 2025-10-05 at 10.55.20.png]]![[Screenshot 2025-10-05 at 11.00.02.png]]![[Screenshot 2025-10-05 at 11.59.04.png]]![[Screenshot 2025-10-05 at 12.05.44.png]]
one dead letter queue can use for many queue
- “Enqueue timestamp” chính là thời điểm thông điệp được đưa vào hàng đợi lần đầu (trong SQS là attribute hệ thống `SentTimestamp`).
- Khi thông điệp bị chuyển từ source queue sang DLQ, `enqueue timestamp` của thông điệp vẫn giữ nguyên (không tạo lại thời gian mới). Nghĩa là thời gian gốc mà message được gửi vào hệ thống không thay đổi.
- Vì vậy, nếu bạn đo “thời gian chờ trong hàng”, bạn có thể dùng `now - SentTimestamp` ngay cả khi message đã ở DLQ.

Retention (thời gian lưu trữ):

- DLQ thường được cấu hình với thời gian lưu trữ (message retention period) dài hơn so với source queue để bạn có thêm thời gian điều tra, sửa lỗi và xử lý lại.
- Lưu ý: thời gian lưu trữ tính từ `SentTimestamp`. Nếu DLQ có retention 14 ngày và message đã “già” 1 ngày trước khi chuyển sang DLQ, nó còn tối đa 13 ngày trong DLQ.

 Kinessis data stream
-![[Screenshot 2025-10-05 at 12.21.47.png]]
![[Screenshot 2025-10-05 at 12.29.53.png]]![[Screenshot 2025-10-05 at 12.33.11.png]]

Kinesis data firehose
can tranformation data on the fly
![[Screenshot 2025-10-05 at 12.40.43.png]]
delivery each mb 
![[Screenshot 2025-10-05 at 12.50.30.png]]![[Screenshot 2025-10-05 at 13.02.25.png]]![[Screenshot 2025-10-05 at 13.08.44.png]]
can use complex sql data
![[Screenshot 2025-10-05 at 13.10.41.png]]![[Screenshot 2025-10-05 at 13.29.42.png]]![[Screenshot 2025-10-05 at 13.32.36.png]]
Gsstramer, RTSP, video steam => video steam

Cognito
![[Screenshot 2025-10-05 at 13.43.26.png]]![[Screenshot 2025-10-05 at 13.56.09.png]]![[Screenshot 2025-10-05 at 14.00.55.png]]![[Screenshot 2025-10-05 at 14.07.22.png]]

AWS glue
![[Screenshot 2025-10-05 at 14.18.38.png]]
data catalog: data metedata and search tool
![[Screenshot 2025-10-05 at 14.21.07.png]]![[Screenshot 2025-10-05 at 14.30.04.png]]
Amazon MQ
![[Screenshot 2025-10-05 at 14.32.49.png]]![[Screenshot 2025-10-05 at 14.36.18.png]]![[Screenshot 2025-10-05 at 14.37.57.png]]![[Screenshot 2025-10-05 at 14.40.11.png]]
App flow
![[Screenshot 2025-10-05 at 14.44.15.png]]![[Screenshot 2025-10-05 at 14.45.51.png]]