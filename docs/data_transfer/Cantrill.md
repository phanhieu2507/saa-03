
Storage Gateway Volume
virtual machine or hardware on the premise
bridge between storage in premise and aws ( just storage )
![[Screenshot 2025-10-11 at 7.38.42.png]]
store mode: great for doing full disk backup of server
![[Screenshot 2025-10-11 at 7.44.28.png]]
cache mode
![[Screenshot 2025-10-11 at 7.52.18.png]]

TAPE-VTL mode
not easy to modify the data on the tape
![[Screenshot 2025-10-11 at 8.09.00.png]]

- CAPEX (Capital Expenditure) = Chi phí đầu tư vốn
    
    - Là khoản chi để mua sắm, xây dựng, nâng cấp tài sản cố định có giá trị sử dụng dài hạn (máy móc, thiết bị, nhà xưởng, phần mềm triển khai on‑prem, giấy phép vĩnh viễn).
    - Ghi nhận trên bảng cân đối kế toán (tài sản), sau đó khấu hao dần theo thời gian.
    - Ví dụ: mua server, storage, thiết bị mạng, xây data center; mua bản quyền phần mềm vĩnh viễn; đầu tư đường truyền riêng.
- OPEX (Operational Expenditure) = Chi phí vận hành
    
    - Là chi phí cho hoạt động thường xuyên, trả đều theo kỳ (tháng/quý/năm).
    - Ghi nhận trực tiếp vào báo cáo kết quả kinh doanh (chi phí kỳ).
    - Ví dụ: phí thuê cloud hàng tháng, thuê đường truyền Internet, điện nước, lương vận hành IT, bảo trì, support, phần mềm trả theo subscription.
![[Screenshot 2025-10-11 at 8.33.03.png]]![[Screenshot 2025-10-11 at 8.36.59.png]]
backup tape, VTL mode ( virtual tape library) => choose tape gate way


starage gateway - file
![[Screenshot 2025-10-11 at 8.45.45.png]]![[Screenshot 2025-10-11 at 10.31.45.png]]
![[Screenshot 2025-10-11 at 10.53.00.png]]
![[Screenshot 2025-10-11 at 10.52.08.png]]![[Screenshot 2025-10-11 at 10.56.18.png]]

Snow ball and snow mobile
snow ball dont have the albility for compute
![[Screenshot 2025-10-11 at 11.06.32.png]]![[Screenshot 2025-10-11 at 11.08.57.png]]
DC: data center
must have single site + data more than 10 pb to use the snow mobile

![[Screenshot 2025-10-11 at 11.11.50.png]]Directory service

![[Screenshot 2025-10-11 at 11.42.29.png]]![[Screenshot 2025-10-11 at 11.50.17.png]]
open source, samba 4, samba => simple ad
![[Screenshot 2025-10-11 at 11.53.06.png]]![[Screenshot 2025-10-11 at 13.49.36.png]]
ad connector is just a proxy
![[Screenshot 2025-10-11 at 13.51.49.png]]![[Screenshot 2025-10-11 at 14.03.38.png]]
datasync
![[Screenshot 2025-10-11 at 14.16.20.png]]![[Screenshot 2025-10-11 at 14.25.15.png]]![[Screenshot 2025-10-11 at 14.26.44.png]]![[Screenshot 2025-10-11 at 14.30.25.png]]![[Screenshot 2025-10-11 at 14.50.41.png]]

Fsx for Windown file server
![[Screenshot 2025-10-11 at 15.07.46.png]]
![[Screenshot 2025-10-11 at 15.07.12.png]]![[Screenshot 2025-09-10 at 22.09.05.png]]![[Screenshot 2025-10-11 at 15.12.26.png]]
fsx for lustre
![[Screenshot 2025-10-11 at 15.22.53.png]]![[Screenshot 2025-10-11 at 15.42.05.png]]![[Screenshot 2025-10-11 at 15.44.26.png]]![[Screenshot 2025-10-11 at 15.47.28.png]]![[Screenshot 2025-10-11 at 15.49.57.png]]

aws tranfer familly

![[Screenshot 2025-10-11 at 15.58.01.png]]![[Screenshot 2025-10-11 at 16.01.40.png]]![[Screenshot 2025-10-11 at 16.04.59.png]]![[Screenshot 2025-10-11 at 16.06.07.png]]