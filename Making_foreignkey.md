```
------------------
ms_reserve_parking
------------------
id
ResidentAddressId (foreign key dari MS_residentAddress)
------------------
```

# Penerapan :

- Buat model VDI.DEMO.CORE/ms_reserve_parking

```
[Table("MS_Reserved_Parking")]
    public class MS_Reserved_Parking : FullAuditedEntity
    {
	...	
        [ForeignKey("ResidentAddressId")]
        [Column(Order = 1)]
        public MS_ResidentAddress MS_ResidentAddress { get; set; }
        public int? ResidentAddressId { get; set; }
	...
```

- Pada model VDI.DEMO.CORE/ms_resident_address, tambahkan
```
 [Table("MS_ResidentAddress")]
    public class MS_ResidentAddress : FullAuditedEntity
    {
	...
        public virtual ICollection<MS_Reserved_Parking> MS_Reserved_Parking { get; set; }
    	...
    }
```

- pada  VDI.DEMO.EntityFrameworkCore/AccessControlsDbContext

```
modelBuilder.Entity<MS_Reserved_Parking>()
            .HasOne(c => c.MS_ResidentAddress)
            .WithMany(m => m.MS_Reserved_Parking)
            .HasForeignKey(u => u.ResidentAddressId)
            .OnDelete(DeleteBehavior.Restrict);
```


