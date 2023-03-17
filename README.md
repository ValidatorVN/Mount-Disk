# Mount-Disk

1/ Check ổ đĩa xem phân vùng:

    lsblk

2/ Xoá dữ liệu ổ mới thuê: ở đây là sda

    fdisk /dev/sda

3/ Format ổ sda1:

    mkfs -t ext4 /dev/sda1
    
nhấn y để đồng ý.

4/ Mount ổ bạn muốn cài node: ví dụ .nibid

    mkdir /mnt/sda
    chmod +x /mnt/sda
    mount -t ext4 /dev/sda1 /mnt/sda
    
5/ Thêm lưu trữ không mất dữ liệu nếu restart
Mở file /etc/fstab và thêm dòng sau vào cuối file:

    nano /etc/fstab
    
    /dev/sda1 /mnt/sda ext4  defaults     0   0
    
    
Lưu trữ bằng UUID:

    lsblk -o NAME,UUID,SIZE
    
    UUID=xxx /mnt/sda ext4 defaults 0 0
