---
title: 包括和排除类型 - EF Core
author: rowanmiller
ms.date: 10/27/2016
ms.assetid: cbe6935e-2679-4b77-8914-a8d772240cf1
uid: core/modeling/included-types
ms.openlocfilehash: ca83b1c432bdf4853dba81e12ec4a739bc8218dc
ms.sourcegitcommit: ec196918691f50cd0b21693515b0549f06d9f39c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/23/2019
ms.locfileid: "71197372"
---
# <a name="including--excluding-types"></a>包含类型和排除类型

将类型包括到模型中意味着，EF 会有该类型的元数据，并且会尝试从数据库读取实例，以及将实例写入到数据库中。

## <a name="conventions"></a>约定

按照约定，在上下文的 `DbSet` 属性中公开的类型会包括在模型中。 此外，在 `OnModelCreating` 方法中提及的类型也会包括模型中。 最后，通过以递归方式浏览已发现类型的导航属性找到的任何类型也会包括在模型中。

**例如，在以下代码中，将发现所有三种类型：**

* `Blog`，因为它是在上下文的 `DbSet` 属性中公开的

* `Post`，因为它是通过 `Blog.Posts` 导航属性发现的

* `AuditEntry`，因为它是在 `OnModelCreating` 中提及的

<!-- [!code-csharp[Main](samples/core/Modeling/Conventions/IncludedTypes.cs?highlight=3,7,16)] -->
``` csharp
class MyContext : DbContext
{
    public DbSet<Blog> Blogs { get; set; }

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        modelBuilder.Entity<AuditEntry>();
    }
}

public class Blog
{
    public int BlogId { get; set; }
    public string Url { get; set; }

    public List<Post> Posts { get; set; }
}

public class Post
{
    public int PostId { get; set; }
    public string Title { get; set; }
    public string Content { get; set; }

    public Blog Blog { get; set; }
}

public class AuditEntry
{
    public int AuditEntryId { get; set; }
    public string Username { get; set; }
    public string Action { get; set; }
}
```

## <a name="data-annotations"></a>数据注释

您可以使用数据批注从模型中排除类型。

[!code-csharp[Main](../../../samples/core/Modeling/DataAnnotations/IgnoreType.cs?highlight=20)]

## <a name="fluent-api"></a>Fluent API

您可以使用熟知的 API 从模型中排除类型。

[!code-csharp[Main](../../../samples/core/Modeling/FluentAPI/IgnoreType.cs?highlight=12)]
