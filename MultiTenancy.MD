bagaimana register user ? POST /api/services/app/User/CreateOrUpdateUser
bagaimana cara setting user host? engga usah diregister di tenant
bagaimana register tenant ? POST /api/services/app/Tenant/CreateTenant
bagaimana meregister user ke suatu tenant? POST /api/services/app/UserLink/LinkToUser => kok ga bisa pakai user admin
bagaimana user login ngakses apa ya ing web, bagaimana otentikasi membedakan yang login berdasarkan tenant ?
user register?
need brp role ??
nengok role di web yang nampil brp banyak?
coba create role dari web ????





skenario
- buat 2 role => user dan admin
- buad 2 user dengan role yang beda
- buat tenant
- meregister user ke suatu tenant tertentu
- membuat method yang mengakses table  yang sudah memiliki yang namanya tenant id menggunakan abpsession
- gimana jika user dan password sama tapi beda tenant





# saat meregister user, field tenant terisi berdasarkan tenantID yang dimiliki user yang meregister, jika ingin meregister user sekalian tenant modif method CreateUserAsync dengan memasukkan tenantID sebagai input
```
user.TenantId = AbpSession.TenantId;
```

# MultiTenancy
-  Buat "Configuration.MultiTenancy.IsEnabled = true;",  caranya  buka VDI.Demo.Core.Shared\DemoConsts.cs 
```
public const bool MultiTenancyEnabled = true;
``` 
- Tambahkan interface IMayHaveTenant/IMustHaveTenant pada Model yang ditentukan (beda IMayHaveTenant/IMustHaveTenant => https://aspnetboilerplate.com/Pages/Documents/Multi-Tenancy#host-vs-tenant)
```
	public class MS_Coverage : FullAuditedEntity, IMayHaveTenant
    {
        public int? TenantId { get; set; }
    }
```
- Migrasi database
- Maka semua table yang mengimplementasikan IMayHaveTenant/IMustHaveTenant (termasuk model bawaan boilerplate seperti user, role) query standard hanya akan menampilkan data yang mempunyai idTenant yang sama dengan user yang login
- jika ingin membuat method yang menampilkan semua isi record nya (tidak berdasarkan tenant saja) maka gunakan DisableFilter
```
using (CurrentUnitOfWork.DisableFilter(AbpDataFilters.MayHaveTenant))
{
	var people2 = _personRepository.GetAllList();                
}
```
- saat sedang login (http://localhost:7000/api/TokenAuth/Authenticate) tambahkan header Abp.TenantId dengan value TenantId sesuai user yang login, kecuali tidak mempunyai TenantID (TenantID == null)

# Mengambil IdTenant dari Session
```
user.TenantId = AbpSession.TenantId;
```


# links
- https://aspnetboilerplate.com/Pages/Documents/Zero/User-Management
- https://stackoverflow.com/questions/47670680/multi-tenant-authentication-imusthavetenant-entity-in-asp-net-boilerplate-modul
- https://aspnetboilerplate.com/Pages/Documents/Data-Filters#disable-filters
- https://aspnetboilerplate.com/Pages/Documents/Multi-Tenancy
- https://aspnetboilerplate.com/Pages/Documents/Zero/Tenant-Management
