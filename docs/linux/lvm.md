# LVM

## Initialize physical volume

Initialize **physical volume** on partition ( so, //partition// should already exists ):

<code>pvcreate /dev/sdb1</code>

## Create / extend volume group

Create **volume group**:

<code>vgcreate vg1 /dev/sdb1</code>


or, add **physical volume** on preexistent volume group:

  vgextend my_volume_group /dev/sdb1


## Create / extend logical volume

Create 10GB **logical volume** on //volume group// vg1:

<code>lvcreate -L 10G -n mylv vg1</code>

or create **logical volume** on //volume group// vg1, using all available space:

<code>lvcreate -l 100%FREE -n mylv vg1</code>


**Extend logical** LOGICVOLUME adding 4GB:

  lvextend -L +4GB /dev/mapper/LOGICVOLUME
  resize2fs /dev/mapper/LOGICVOLUME

**Extend logical** LOGICVOLUME to use all available free space:

  lvextend -l +100%FREE /dev/mapper/LOGICVOLUME
  resize2fs /dev/mapper/LOGICVOLUME
