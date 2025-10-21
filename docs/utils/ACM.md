# AWS Certificate Manager
- manage, provision and deployu SSL Certs
- certs creaded by ACM are automaticly renewed


## IAM certificate Store
- used for regions where ACM is not available
- can be used via cli
![[Screenshot 2025-10-19 at 15.48.17.png]]![[Screenshot 2025-10-19 at 15.49.34.png]]
can not use ACM with the EC2
![[Screenshot 2025-10-19 at 15.51.11.png]]![[Screenshot 2025-10-19 at 15.55.14.png]]![[Screenshot 2025-10-19 at 15.57.09.png]]
self signed cert will not be accepted in cloudfront
![[Screenshot 2025-10-19 at 16.06.20.png]]![[Screenshot 2025-10-19 at 20.13.31.png]]
if old browsers => choose dedicated IP = being charged
![[Screenshot 2025-10-19 at 20.18.43.png]]

origin patch: append to the origin  domainname for domain request
can add custom header to thecustom origin to check that from cloudfront

cloudfront secure

![[Screenshot 2025-10-19 at 20.39.11.png]]![[Screenshot 2025-10-19 at 20.42.24.png]]
![[Screenshot 2025-10-19 at 20.52.41.png]]

create trusted key grou dont need the root user
![[Screenshot 2025-10-19 at 21.17.53.png]]![[Screenshot 2025-10-19 at 21.26.40.png]]
![[Screenshot 2025-10-19 at 21.40.12.png]]![[Screenshot 2025-10-19 at 21.41.57.png]]![[Screenshot 2025-10-19 at 21.43.28.png]]![[Screenshot 2025-10-19 at 21.50.14.png]]