# Mount-Disk

1/ Check ổ đĩa xem phân vùng:

    lsblk

2/ Xoá dữ liệu ổ mới thuê: ở đây là sda

    fdisk /dev/sda

3/ Format ổ sda1:

    mkfs -t ext4 /dev/sda1
    
nhấn y để đồng ý.

4/ Mount ổ bạn muốn cài node: ví dụ .nibid

    mkdir .nibid
    chmod +x nibid
    mount -t ext4 /dev/sda1 /root/.nibid
    
5/ Thêm lưu trữ không mất dữ liệu nếu restart

    nano /etc/fstab
    
    /dev/sda1 /root/.nibid ext4  defaults     0   0
    
