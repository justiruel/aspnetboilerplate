
```
using Abp.Domain.Entities.Auditing;
using System.ComponentModel.DataAnnotations;
using System.ComponentModel.DataAnnotations.Schema;

namespace VDI.Demo.Belajar
{
    [Table("MS_Belajar")] //---> define table
    public class MS_Belajar : FullAuditedEntity
    {
        [Required] //---> wajib diisi
        public string nama { get; set; }
        [StringLength(40, ErrorMessage = "Name cannot be longer than 40 characters.")]
        public string umur { get; set; }
        public int? umur { get; set; } // --> means return value can be null or integer.  kalo di database == allow null
        
        //dibawah ini artinya di table MS_belajar kita buat field "PersonId" yang merupakan foreign key dari
        //table Person
        [ForeignKey("PersonId")]
        public virtual Person Person { get; set; }
        public virtual int PersonId { get; set; }
 
    }
}

```
