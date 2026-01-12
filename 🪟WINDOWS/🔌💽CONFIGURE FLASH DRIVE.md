==USB Management Commands==
diskpart
list disk
select disk X
clean
create partition primary
select partition 1
format fs=ntfs quick   # o fs=fat32 quick
assign letter=H
exit

