
```
using Abp.Domain.Entities.Auditing;
using System.ComponentModel.DataAnnotations;
using System.ComponentModel.DataAnnotations.Schema;

namespace VDI.Demo.Belajar
{
    [Table("MS_Belajar")] //---> define table
    public class MS_Belajar : FullAuditedEntity
    {
        const int umurLength = 40;
    
        [Required] //---> wajib diisi
        public string nama { get; set; }
        [StringLength(umurLength, ErrorMessage = "Name cannot be longer than 40 characters.")]
        public string umur { get; set; }
        public int? umur { get; set; } // --> means return value can be null or integer.  kalo di database == allow null, klo gapake "?" artinya not null
        
        //dibawah ini artinya di table MS_belajar kita buat field "PersonId" yang merupakan foreign key dari
        //table Person
        [ForeignKey("PersonId")]  --> foreign key di table MS_Belajar
        public Person Person { get; set; }
        public int PersonId { get; set; }
 
    }
}

```

## Sample Model Person

```
namespace VDI.Demo.Belajar
{
    [Table("Person")] //---> define table
    public class Person : FullAuditedEntity
    {
        [key]
        public int id_person { get; set; }
         public string data { get; set; }
    }
}

```
