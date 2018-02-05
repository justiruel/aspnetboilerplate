- *.web.host --> set as startup project
- *.web.host/appsettings.json --> connection string isi :
```
"Default": "Data Source=DESKTOP-C6TIJGA\\SQLEXPRESS; Initial Catalog=projectJalanDB; User ID=devel  oper2018;Password=developer2018;"
```
- Buat model di dalam *.core (otomatis tercipta field Id sebagai primary key dan auto increment, jadi tidak perlu di definisikan di model) jangan lupa pakai "public class nama_table"
- *.EntityframeworkCore/EntityframeworkCore/DemoDbContext.cs ketik:
```
public virtual DbSet<Person> Persons { get; set; } (pastikan class person Public)
```
- pada package manager console --> Default Project pilih "*.EntityframeworkCore" ketik :
```
add-migration "add persons" (log dapat dilihati di *.EntityframeworkCore/migrations)
```
ketik : 
```
update-database (untuk menulis perubahan ke database)
```
