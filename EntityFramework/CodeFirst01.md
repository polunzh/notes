# Code First 笔记(一)
---
## [Code First Conventions](http://www.entityframeworktutorial.net/code-first/code-first-conventions.aspx)
### 1. 类型探索(Type Convention)

> * Code-First includes types defined as a DbSet property in context class.
> * Code-First includes reference types included in entity types even if they are defined in different assembly.
> * Code-First includes derived classes even if only the base class is defined as DbSet property.

### 2. Primary Key Conventions
> * In the previous section, we have seen that Code-First automatically creates a Primary Key in each table. The default convention for primary key is that Code-First would create a primary key for a property if the property name is Id or <class name>Id (NOT case sensitive). The data type of a primary key property can be anything, but if the type of the primary key property is numeric or GUID, it will be configured as an identity column.
> * If you have defined key property other than Id or &lt;ClassName>Id then ModelValidationException will be thrown.

### 3.Relationship Convention:
> Code First infer the relationship between the two entities using
navigation property. This navigation property can be simple
reference type or collection type.The default code first convention
for relationship automatically inserted a foreign key with
&lt;navigation property Name>_&lt;primary key property name of navigation property type>

### 4.Foreign key Convention:
> It is recommended to include a foreign key property on the
dependent end of a relationship:

```C#
    public class Student
    {
        public int StudentId { get; set; }
        public string Name { get; set; }
        public int Age { get; set; }

        public int StandardId { get; set; }
        public Standard Standard { get; set; }
    }
    public class Standard
    {
        public int StandardId { get; set; }
        public string StandardName { get; set; }
        public IList<Student> Students { get; set; }
    }
```
### 5.Complex type Convention:
> Code First creates complex type for the class which does not
include key property and also primary key is not registered using
DataAnnotation or Fluent API.（备注：``这点儿不是很理解``）