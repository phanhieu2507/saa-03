high availablity
- maximize the online time as possible
faults tolerance
- là đặc tính cho phép một hệ thống tiếp tục hoạt động bình thường ngay cả khi một số (một hoặc nhiều) thành phần của nó gặp sự cố
- ft > ha
disaster recorery:
- - một tập hợp các chính sách, công cụ và quy trình nhằm cho phép khôi phục hoặc duy trì liên tục các hạ tầng và hệ thống công nghệ trọng yếu sau một thảm họa do tự nhiên hoặc con người gây ra.
- tap trung vao rpo va rto
- use when thes don't work

Regional and Global aws arcchitecture

ELB ![[Screenshot 2025-09-28 at 13.21.19.png]]![[Screenshot 2025-09-28 at 13.50.11.png]]
cross zone lb not enabled by default
![[Screenshot 2025-09-28 at 15.37.33.png]]
![[Screenshot 2025-09-28 at 15.41.07.png]]![[Screenshot 2025-09-28 at 15.44.54.png]]![[Screenshot 2025-09-28 at 15.46.49.png]]
doesnot want to terminate the ssl => use nlb
![[Screenshot 2025-09-28 at 15.52.37.png]]![[Screenshot 2025-09-28 at 15.53.18.png]]
Launch Configurations and Launch Templates
![[Screenshot 2025-09-28 at 15.56.51.png]]![[Screenshot 2025-09-28 at 15.57.50.png]]![[Screenshot 2025-09-28 at 16.08.05.png]]
asg can span to many subnet
![[Screenshot 2025-09-28 at 16.09.18.png]]
cooldown: wait until the next period
![[Screenshot 2025-09-28 at 16.16.49.png]]

![[Screenshot 2025-09-28 at 16.18.01.png]]

need to define the health check for the asg: use health check of elb or instance 
![[Screenshot 2025-09-28 at 16.20.37.png]]![[Screenshot 2025-09-28 at 16.23.55.png]]![[Screenshot 2025-09-28 at 16.24.38.png]]

ASG lifecycle hooks

![[Screenshot 2025-09-28 at 16.51.25.png]]![[Screenshot 2025-09-28 at 16.53.45.png]]![[Screenshot 2025-09-28 at 17.05.33.png]]
if not set suitable health check grace period: instance chưa khởi động xong đã bị check => unhealthy => bị terminate

SSL offload
![[Screenshot 2025-09-29 at 22.10.40.png]]![[Screenshot 2025-09-30 at 6.40.16.png]]

GWLB
![[Screenshot 2025-09-30 at 6.58.44.png]]
endpoint can add to the route table as the next hop
![[Screenshot 2025-09-30 at 7.01.46.png]]![[Screenshot 2025-09-30 at 7.07.24.png]]