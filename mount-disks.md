# Mount disks



check disk to mount

```text
sudo fdisk -l | grep T // T 단위의 disk만 보고싶었

// results
Partition 1 does not start on physical sector boundary.
Device           Start        End    Sectors   Size Type
Disk /dev/sdb: 3.7 TiB, 4000787030016 bytes, 7814037168 sectors
Disk /dev/sdc: 5.5 TiB, 6001175126016 bytes, 11721045168 sectors
Device      Start         End     Sectors  Size Type
/dev/sdc2  264192 11721041919 11720777728  5.5T Microsoft basic data
Device     Start        End    Sectors   Size Type
Device     Start        End    Sectors   Size Type

```



create target directory to mount disk

```text
sudo mkdir /media/emjay/fiveT
```



mount disk

```text
sudo mount /dev/sdc /media/emjay/fiveT
```

\(ntfs 타입이라 그런지 이 단계에서 실패하여 부트시 자동 mount단계로 넘어\)



## auto-mount 

check uuid

```text
sudo blkid

// results
/dev/nvme0n1: PTUUID="27308f51-620a-4437-9ef1-ace1016c10ed" PTTYPE="gpt"
/dev/nvme0n1p1: UUID="BCE2-1EEF" TYPE="vfat" PARTLABEL="EFI System Partition" PARTUUID="ffad7675-6f74-4c3b-b9c4-8ecbb374e970"
/dev/nvme0n1p2: UUID="2ee3450b-2d8e-404d-8e79-f77e152b3fd0" TYPE="ext4" PARTUUID="19dd0fb2-c960-4a6c-b197-735d031ce32c"
/dev/sda: UUID="7d40b0e9-ec51-4d80-bee1-b1bf27ec2417" TYPE="ext4"
/dev/sdb: LABEL="Workspace" UUID="46c2f148-aed1-4de8-8b30-0454e8c22441" TYPE="ext4"

// what I want to add -------------
/dev/sdc1: PARTLABEL="Microsoft reserved partition" PARTUUID="154acc44-6451-4ad4-8bda-ebb3444c46bc"
/dev/sdc2: LABEL="M-lM-^CM-^H M-kM-3M-<M-kM-%M-(" UUID="642E9C372E9C0468" TYPE="ntfs" PARTLABEL="Backup Data - Ubuntu" PARTUUID="72ed7035-b7d2-403f-b9d5-98b6da67669c"
// --------------------------------

/dev/sdd1: LABEL="MyPassport2" UUID="f83ace50-ea76-4c92-ae2b-a9563a045e3f" TYPE="ext4" PARTLABEL="MyPassport2" PARTUUID="e0d80129-ce9c-4ad6-9a14-c27fa0f65cca"

```

add a partition to fstab file

```text
sudo vim /etc/fstab


UUID=2ee3450b-2d8e-404d-8e79-f77e152b3fd0 /               ext4    errors=remount-ro 0       1
UUID=BCE2-1EEF  /boot/efi       vfat    umask=0077      0       1
/swapfile                                 none            swap    sw              0       0
/dev/disk/by-uuid/46c2f148-aed1-4de8-8b30-0454e8c22441 /media/emjay/Workspace auto nosuid,nodev,nofail,x-gvfs-show,x-gvfs-name=Workspace 0 0
/dev/disk/by-uuid/d1d702c5-144a-423b-8bf8-3e7c888358b1 /media/emjay/DB_001 auto nosuid,nodev,nofail,x-gvfs-show,x-gvfs-name=DB_001,x-gvfs-icon=DB_001,x-gvfs-symbolic-icon=DB_001 0 0

// newly added
UUID=642E9C372E9C0468 /media/emjay/fiveT ntfs defaults 0 0

```

reload fstab

```text
mount -a
```



## mount check

```text
(base) emjay@emjay-PC:/media/emjay/fiveT$ df -h | grep /media
/dev/sdb        3.6T  2.0T  1.5T  58% /media/emjay/Workspace
/dev/sdc2       5.5T  4.0T  1.5T  73% /media/emjay/fiveT
```

## Ref

{% embed url="https://bluexmas.tistory.com/632" %}

{% embed url="https://chrisschuld.com/2007/08/reload-fstab-etcfstab/" %}



