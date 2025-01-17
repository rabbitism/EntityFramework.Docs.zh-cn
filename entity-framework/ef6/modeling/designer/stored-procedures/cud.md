---
title: 设计器 CUD 存储过程-EF6
author: divega
ms.date: 10/23/2016
ms.assetid: 1e773972-2da5-45e0-85a2-3cf3fbcfa5cf
ms.openlocfilehash: bdb0df969c33d5ad3f103bfa9af6002c9c2bb9b3
ms.sourcegitcommit: 6c28926a1e35e392b198a8729fc13c1c1968a27b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2019
ms.locfileid: "71813552"
---
# <a name="designer-cud-stored-procedures"></a>设计器 CUD 存储过程

此分步演练演示如何使用 Entity Framework Designer （EF 设计器）将实体类型的 create @ no__t-0insert、update 和 delete （CUD）操作映射到存储过程。  默认情况下，实体框架会自动为 CUD 操作生成 SQL 语句，但也可以将存储过程映射到这些操作。  

请注意，Code First 不支持映射到存储过程或函数。 但是，可以使用 DbSet. SqlQuery 方法调用存储过程或函数。 例如：

``` csharp
var query = context.Products.SqlQuery("EXECUTE [dbo].[GetAllProducts]");
```

## <a name="considerations-when-mapping-the-cud-operations-to-stored-procedures"></a>将 CUD 操作映射到存储过程时的注意事项

将 CUD 操作映射到存储过程时，请注意以下事项：

- 如果要将其中一个 CUD 操作映射到存储过程，请映射所有这些操作。 如果不映射这三个，则未映射的操作将失败（如果执行了）并引发了 **UpdateException** will。
- 必须将存储过程的每个参数映射到实体属性。
- 如果服务器为插入的行生成主键值，则必须将此值映射回实体的键属性。 在下面的示例中， **InsertPerson** stored 过程返回新创建的主键作为存储过程的结果集的一部分。 使用 EF 设计器的 **&lt;Add 结果绑定 @ no__t** feature 将主键映射到实体键（**PersonID**）。
- 存储过程调用映射到概念模型中的实体1:1。 例如，如果在概念模型中实现了继承层次结构，然后映射**父级**（base）和**子**（派生）实体的 CUD 存储过程，则保存**子**更改将仅调用**子**"存储过程中，不会触发**父**存储过程调用。

## <a name="prerequisites"></a>先决条件

若要完成此演练，您需要：

- Visual Studio 的最新版本。
- [School 示例数据库](~/ef6/resources/school-database.md)。

## <a name="set-up-the-project"></a>设置项目

- 打开 Visual Studio 2012。
- 选择 "**文件-&gt;" &gt; 项目**
- 在左窗格中，单击 " **Visual C @ no__t**"，然后选择**控制台**模板。
- 在名称中输入 " **CUDSProcsSample** as"。
- 选择 **"确定"** 。

## <a name="create-a-model"></a>创建模型

- 在解决方案资源管理器中右键单击项目名称，然后选择 "**添加-&gt;" "新项**"。
- 从左侧菜单中选择 "**数据**"，然后在 "模板" 窗格中选择 " **ADO.NET 实体数据模型**。
- 输入**CUDSProcs**作为文件名，然后单击 "**添加**"。
- 在 "选择模型内容" 对话框中，选择 " **从数据库生成**"，然后单击 " **下一步**"。
- 单击 " **新建连接**"。 在 "连接属性" 对话框中，输入服务器名称（例如， **（localdb）\\mssqllocaldb**），选择 "身份验证方法"， **键入 School** 作为数据库名称，然后单击 **"确定"** 。
    "选择您的数据连接" 对话框将通过数据库连接设置进行更新。
- 在 "选择数据库对象" 对话框中的 " **表**@no__t" 下，选择 **Person**表。
- 另外，在 "**存储过程和函数**" 节点下选择以下存储过程：**DeletePerson**、 **InsertPerson**和**UpdatePerson**。
- 从 Visual Studio 2012 开始，EF 设计器支持存储过程的大容量导入。 默认情况下，将选中 "将**选定的存储过程和函数导入实体模型**"。 由于在此示例中，我们已存储了用于插入、更新和删除实体类型的存储过程，因此我们不想将它们导入，并将取消选中此复选框。

    ![导入过程](~/ef6/media/importsprocs.jpg)

- 单击 " **完成**"。
    显示了 EF 设计器（提供编辑模型的设计图面）。

## <a name="map-the-person-entity-to-stored-procedures"></a>将 Person 实体映射到存储过程

- 右键单击 " **人员**" @no__t 类型，然后选择 " **存储过程映射**"。
- 存储过程映射显示在 **映射详细信息**@no__t 1window 中。
- 单击 **&lt;Select Insert Function @ no__t-2**。
    该字段变成一个下拉列表，该列表中包含存储模型中可以映射到概念模型中的实体类型的存储过程。
    在下拉列表中选择 " **InsertPerson** from"。
- 此时将显示存储过程参数和实体属性之间的默认映射。 请注意，箭头指示映射方向：属性值是提供给存储过程参数的。
- 单击 " **@no__t" 1Add Result no__t-2**"。
- 键入 **NewPersonID**， **InsertPerson** stored 过程返回的参数的名称。 请确保不要键入前导空格或尾随空格。
- 按 **enter**。
- 默认情况下， **NewPersonID**  映射到实体键 **PersonID**。 请注意，箭头指示映射方向：结果列的值是提供给属性的。

    ![映射详细信息](~/ef6/media/mappingdetails.png)

- 单击 " **&lt;Select Update Function @ no__t-2** And select **UpdatePerson** from 生成的下拉列表。
- 此时将显示存储过程参数和实体属性之间的默认映射。
- 单击 **@no__t 删除函数 @ no__t-2** And select **DeletePerson** from 生成的下拉列表。
- 此时将显示存储过程参数和实体属性之间的默认映射。

@No__t 类型的 **用户**的插入、更新和删除操作现已映射到存储过程。

如果要在使用存储过程更新或删除实体时启用并发检查，请使用下列选项之一：

- 使用**OUTPUT**参数从存储过程中返回受影响的行数，并在参数名称旁  Checkbox 检查**受影响的行参数**。 如果调用操作时返回的值为零，则将引发  [**OptimisticConcurrencyException**](https://msdn.microsoft.com/library/system.data.optimisticconcurrencyexception.aspx) will。
- 选中要用于并发检查的属性旁边的 "**使用原始值**" 复选框。 尝试更新时，在将数据写回数据库时，将使用最初从数据库读取的属性的值。 如果值与数据库中的值不匹配，则会引发**OptimisticConcurrencyException** will。

## <a name="use-the-model"></a>使用模型

打开**Program.cs**文件，其中定义了**Main**方法。 将以下代码添加到 Main 函数中。

此代码创建一个新的**Person**对象，然后更新该对象，最后删除该对象。

``` csharp
    using (var context = new SchoolEntities())
    {
        var newInstructor = new Person
        {
            FirstName = "Robyn",
            LastName = "Martin",
            HireDate = DateTime.Now,
            Discriminator = "Instructor"
        }

        // Add the new object to the context.
        context.People.Add(newInstructor);

        Console.WriteLine("Added {0} {1} to the context.",
            newInstructor.FirstName, newInstructor.LastName);

        Console.WriteLine("Before SaveChanges, the PersonID is: {0}",
            newInstructor.PersonID);

        // SaveChanges will call the InsertPerson sproc.  
        // The PersonID property will be assigned the value
        // returned by the sproc.
        context.SaveChanges();

        Console.WriteLine("After SaveChanges, the PersonID is: {0}",
            newInstructor.PersonID);

        // Modify the object and call SaveChanges.
        // This time, the UpdatePerson will be called.
        newInstructor.FirstName = "Rachel";
        context.SaveChanges();

        // Remove the object from the context and call SaveChanges.
        // The DeletePerson sproc will be called.
        context.People.Remove(newInstructor);
        context.SaveChanges();

        Person deletedInstructor = context.People.
            Where(p => p.PersonID == newInstructor.PersonID).
            FirstOrDefault();

        if (deletedInstructor == null)
            Console.WriteLine("A person with PersonID {0} was deleted.",
                newInstructor.PersonID);
    }
```

- 编译并运行该应用程序。 该程序生成以下输出 *

> [!NOTE]
> PersonID 是由服务器自动生成的，因此很可能会看到不同的数字 *

``` Output
Added Robyn Martin to the context.
Before SaveChanges, the PersonID is: 0
After SaveChanges, the PersonID is: 51
A person with PersonID 51 was deleted.
```

如果使用的是 Visual Studio 的旗舰版，则可以将 Intellitrace 与调试器结合使用，以查看执行的 SQL 语句。

![Intellitrace](~/ef6/media/intellitrace.png)
