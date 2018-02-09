- pengganti edmx -> Irepository
- kalau ada error ceknya di : D:\PROJECT\RISET\aspnetboilerplate\be-dotnetcore\src\VDI.Demo.Web.Host\App_Data\Logs
- di swagger (http://localhost:22742/swagger/) ada judul <b>MSBelajar</b> itu diambil dari  <b>MsBelajarAppService</b>
- check default user login (userID = 2,"userNameOrEmailAddress": "admin", pass = 123qwe): <br/>
VDI.Demo.EntityFrameworkCore\Migrations\Seed\Host --> HostRoleAndUserCreator.cs 
- Contoh CRUD ambil dari => D:\PROJECT\RISET\aspnetboilerplate\MobileEmployeeServicesAdministrator\src\VDI.Demo.Application\EmployeeServices\MS_BisnisUnits
- DELETE /api/services/app/Vehicle/DeleteVehicle --> jika diberi nama DeleteVehicle maka rest methodnya akan menjadi "DELETE" <br/> jika diberi nama GETVehicle rest methodnya akan menjadi "GET" dan seterusnya, jika tidak ada identifikasi kusus misal TestVehicle maka akan menjadi "POST"

- menambah field "Description" ke table Roles, caranya : <br/>
lakukan seperti biasanya, hanya saja saat ingin create/update ada tambahan kode di RoleAppService.cs
```
var role = new Role(AbpSession.TenantId, input.Role.DisplayName) { IsDefault = input.Role.IsDefault, Description = input.Role.Description };
```

- misalkan kita main  multi tenant maka setiap kita mau create, ambil TenantId dari session lalu create, caranya :
```
input.TenantId = AbpSession.TenantId 
```

