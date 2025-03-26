# 🧹 Adding a New HDD to Your Server (LVM + Proxmox)

This guide explains how to add a new hard drive to your home server using **LVM (Logical Volume Manager)** on Proxmox. It includes steps for creating new volumes or expanding existing ones.

> ⚠️ **Backup any important data before formatting drives!**

---

## 📦 Creating a New Logical Volume (LV)

1. **Add New Disk via Proxmox GUI**  
   Format it if needed — this will erase all existing data.

2. **Identify the Disk**
   ```bash
   lsblk
   # or
   fdisk -l
   ```

3. **Create a New Physical Volume**
   ```bash
   pvcreate /dev/sdX
   ```

4. **Create a New Volume Group**
   ```bash
   vgcreate new_volume_group /dev/sdX
   ```

5. **Create a New Logical Volume**
   ```bash
   lvcreate -L 50G -n new_logical_volume new_volume_group
   ```

6. **Create a Filesystem**
   ```bash
   mkfs.ext4 /dev/new_volume_group/new_logical_volume
   ```

7. **Mount the Filesystem**
   ```bash
   mkdir /mnt/new_logical_volume
   mount /dev/new_volume_group/new_logical_volume /mnt/new_logical_volume
   ```

8. **Verify the Setup**
   ```bash
   lvdisplay
   df -h
   ```

---

## 🧠 Resizing an Existing Logical Volume

1. **Add New Disk via Proxmox GUI**  
   Format it if needed.

2. **Create a New Physical Volume**
   ```bash
   pvcreate /dev/sdX
   ```

3. **Extend Existing Volume Group**
   ```bash
   vgextend existing_volume_group /dev/sdX
   ```

4. **Resize the Logical Volume**
   ```bash
   lvextend -l +100%FREE /dev/existing_volume_group/existing_logical_volume
   ```

5. **Resize the Filesystem**
   ```bash
   resize2fs /dev/existing_volume_group/existing_logical_volume
   ```

6. **Verify the Setup**
   ```bash
   lvdisplay
   df -h
   ```

---

## 📟 Notes

- Replace `/dev/sdX`, `new_volume_group`, etc., with your actual names.
- Adjust size flags as needed (`-L 50G`, `+100%FREE`, etc.).
- For persistence across reboots, update `/etc/fstab`.

