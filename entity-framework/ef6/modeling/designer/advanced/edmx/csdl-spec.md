---
title: CSDL 规范的 EF6
author: divega
ms.date: 2016-10-23
ms.prod: entity-framework
ms.author: divega
ms.manager: avickers
ms.technology: entity-framework-6
ms.topic: article
ms.assetid: c54255f4-253f-49eb-bec8-ad7927ac2fa3
caps.latest.revision: 3
ms.openlocfilehash: 0ece73a19fe7ea244905bccb728ab2a104c5179f
ms.sourcegitcommit: f05e7b62584cf228f17390bb086a61d505712e1b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/08/2018
ms.locfileid: "39120377"
---
# <a name="csdl-specification"></a><span data-ttu-id="9a003-102">CSDL 规范</span><span class="sxs-lookup"><span data-stu-id="9a003-102">CSDL Specification</span></span>
<span data-ttu-id="9a003-103">概念架构定义语言 (CSDL) 是一种基于 XML 的语言，它描述构成数据驱动应用程序的概念模型的实体、关系和函数。</span><span class="sxs-lookup"><span data-stu-id="9a003-103">Conceptual schema definition language (CSDL) is an XML-based language that describes the entities, relationships, and functions that make up a conceptual model of a data-driven application.</span></span> <span data-ttu-id="9a003-104">实体框架或 WCF 数据服务可以使用此概念模型。</span><span class="sxs-lookup"><span data-stu-id="9a003-104">This conceptual model can be used by the Entity Framework or WCF Data Services.</span></span> <span data-ttu-id="9a003-105">实体框架使用通过 CSDL 描述的元数据实体和关系数据源的概念模型中定义的映射。</span><span class="sxs-lookup"><span data-stu-id="9a003-105">The metadata that is described with CSDL is used by the Entity Framework to map entities and relationships that are defined in a conceptual model to a data source.</span></span> <span data-ttu-id="9a003-106">有关详细信息，请参阅[SSDL 规范](~/ef6/modeling/designer/advanced/edmx/ssdl-spec.md)并[MSL 规范](~/ef6/modeling/designer/advanced/edmx/msl-spec.md)。</span><span class="sxs-lookup"><span data-stu-id="9a003-106">For more information, see [SSDL Specification](~/ef6/modeling/designer/advanced/edmx/ssdl-spec.md) and [MSL Specification](~/ef6/modeling/designer/advanced/edmx/msl-spec.md).</span></span>

<span data-ttu-id="9a003-107">CSDL 是实体数据模型的实体框架的实现。</span><span class="sxs-lookup"><span data-stu-id="9a003-107">CSDL is the Entity Framework's implementation of the Entity Data Model.</span></span>

<span data-ttu-id="9a003-108">在实体框架应用程序，概念模型元数据是加载从.csdl 文件 （用 CSDL 编写） 到 System.Data.Metadata.Edm.EdmItemCollection 的实例，是可访问通过使用中的方法System.Data.Metadata.Edm.MetadataWorkspace 类。</span><span class="sxs-lookup"><span data-stu-id="9a003-108">In an Entity Framework application, conceptual model metadata is loaded from a .csdl file (written in CSDL) into an instance of the System.Data.Metadata.Edm.EdmItemCollection and is accessible by using methods in the System.Data.Metadata.Edm.MetadataWorkspace class.</span></span> <span data-ttu-id="9a003-109">实体框架使用概念模型元数据将针对数据源特定的命令对概念模型的查询。</span><span class="sxs-lookup"><span data-stu-id="9a003-109">Entity Framework uses conceptual model metadata to translate queries against the conceptual model to data source-specific commands.</span></span>

<span data-ttu-id="9a003-110">在 EF 设计器将概念模型信息.edmx 文件中存储在设计时。</span><span class="sxs-lookup"><span data-stu-id="9a003-110">The EF Designer stores conceptual model information in an .edmx file at design time.</span></span> <span data-ttu-id="9a003-111">在生成时，EF 设计器使用.edmx 文件中的信息创建在运行时所需的实体框架的.csdl 文件。</span><span class="sxs-lookup"><span data-stu-id="9a003-111">At build time, the EF Designer uses information in an .edmx file to create the .csdl file that is needed by Entity Framework at runtime.</span></span>

<span data-ttu-id="9a003-112">CSDL 的版本按 XML 命名空间进行区分。</span><span class="sxs-lookup"><span data-stu-id="9a003-112">Versions of CSDL are differentiated by XML namespaces.</span></span>

| <span data-ttu-id="9a003-113">CSDL 版本</span><span class="sxs-lookup"><span data-stu-id="9a003-113">CSDL Version</span></span> | <span data-ttu-id="9a003-114">XML Namespace</span><span class="sxs-lookup"><span data-stu-id="9a003-114">XML Namespace</span></span>                                |
|:-------------|:---------------------------------------------|
| <span data-ttu-id="9a003-115">CSDL v1</span><span class="sxs-lookup"><span data-stu-id="9a003-115">CSDL v1</span></span>      | http://schemas.microsoft.com/ado/2006/04/edm |
| <span data-ttu-id="9a003-116">CSDL v2</span><span class="sxs-lookup"><span data-stu-id="9a003-116">CSDL v2</span></span>      | http://schemas.microsoft.com/ado/2008/09/edm |
| <span data-ttu-id="9a003-117">CSDL v3</span><span class="sxs-lookup"><span data-stu-id="9a003-117">CSDL v3</span></span>      | http://schemas.microsoft.com/ado/2009/11/edm |

 
## <a name="association-element-csdl"></a><span data-ttu-id="9a003-118">Association 元素 (CSDL)</span><span class="sxs-lookup"><span data-stu-id="9a003-118">Association Element (CSDL)</span></span>

<span data-ttu-id="9a003-119">**关联**元素定义两个实体类型之间的关系。</span><span class="sxs-lookup"><span data-stu-id="9a003-119">An **Association** element defines a relationship between two entity types.</span></span> <span data-ttu-id="9a003-120">关联必须指定关系中涉及的实体类型和关系的每一端可能的实体类型数量（也称为重数）。</span><span class="sxs-lookup"><span data-stu-id="9a003-120">An association must specify the entity types that are involved in the relationship and the possible number of entity types at each end of the relationship, which is known as the multiplicity.</span></span> <span data-ttu-id="9a003-121">关联端的多重性可以具有的一 (1)、 零个或一个值 (0..1) 或许多 (\*)。</span><span class="sxs-lookup"><span data-stu-id="9a003-121">The multiplicity of an association end can have a value of one (1), zero or one (0..1), or many (\*).</span></span> <span data-ttu-id="9a003-122">在两个的子 End 元素中指定此信息。</span><span class="sxs-lookup"><span data-stu-id="9a003-122">This information is specified in two child End elements.</span></span>

<span data-ttu-id="9a003-123">通过导航属性或外键（如果在实体类型上公开了外键）可以访问关联一端的实体类型实例。</span><span class="sxs-lookup"><span data-stu-id="9a003-123">Entity type instances at one end of an association can be accessed through navigation properties or foreign keys, if they are exposed on an entity type.</span></span>

<span data-ttu-id="9a003-124">在应用程序中，关联的实例表示实体类型的实例之间的特定关联。</span><span class="sxs-lookup"><span data-stu-id="9a003-124">In an application, an instance of an association represents a specific association between instances of entity types.</span></span> <span data-ttu-id="9a003-125">关联实例按逻辑分组在关联集中。</span><span class="sxs-lookup"><span data-stu-id="9a003-125">Association instances are logically grouped in an association set.</span></span>

<span data-ttu-id="9a003-126">**关联**元素可以具有下列子元素 （按所列顺序）：</span><span class="sxs-lookup"><span data-stu-id="9a003-126">An **Association** element can have the following child elements (in the order listed):</span></span>

-   <span data-ttu-id="9a003-127">文档 （零个或一个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-127">Documentation (zero or one element)</span></span>
-   <span data-ttu-id="9a003-128">结束 （正好两个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-128">End (exactly 2 elements)</span></span>
-   <span data-ttu-id="9a003-129">ReferentialConstraint （零个或一个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-129">ReferentialConstraint (zero or one element)</span></span>
-   <span data-ttu-id="9a003-130">批注元素 （零个或多个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-130">Annotation elements (zero or more elements)</span></span>

### <a name="applicable-attributes"></a><span data-ttu-id="9a003-131">适用的特性</span><span class="sxs-lookup"><span data-stu-id="9a003-131">Applicable Attributes</span></span>

<span data-ttu-id="9a003-132">下表描述了可应用于的特性**关联**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-132">The table below describes the attributes that can be applied to the **Association** element.</span></span>

| <span data-ttu-id="9a003-133">特性名</span><span class="sxs-lookup"><span data-stu-id="9a003-133">Attribute Name</span></span> | <span data-ttu-id="9a003-134">是否必需</span><span class="sxs-lookup"><span data-stu-id="9a003-134">Is Required</span></span> | <span data-ttu-id="9a003-135">“值”</span><span class="sxs-lookup"><span data-stu-id="9a003-135">Value</span></span>                        |
|:---------------|:------------|:-----------------------------|
| <span data-ttu-id="9a003-136">**名称**</span><span class="sxs-lookup"><span data-stu-id="9a003-136">**Name**</span></span>       | <span data-ttu-id="9a003-137">是</span><span class="sxs-lookup"><span data-stu-id="9a003-137">Yes</span></span>         | <span data-ttu-id="9a003-138">关联的名称。</span><span class="sxs-lookup"><span data-stu-id="9a003-138">The name of the association.</span></span> |

 

> [!NOTE]
> <span data-ttu-id="9a003-139">可以将任意数量的 （自定义 XML 特性） 的批注特性应用于**关联**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-139">Any number of annotation attributes (custom XML attributes) may be applied to the **Association** element.</span></span> <span data-ttu-id="9a003-140">然而，自定义特性可能不属于为 CSDL 保留的任何 XML 命名空间。</span><span class="sxs-lookup"><span data-stu-id="9a003-140">However, custom attributes may not belong to any XML namespace that is reserved for CSDL.</span></span> <span data-ttu-id="9a003-141">任何两个自定义特性的完全限定名称都不能相同。</span><span class="sxs-lookup"><span data-stu-id="9a003-141">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

 

### <a name="example"></a><span data-ttu-id="9a003-142">示例</span><span class="sxs-lookup"><span data-stu-id="9a003-142">Example</span></span>

<span data-ttu-id="9a003-143">下面的示例演示**关联**定义的元素**CustomerOrders**关联的外键不上公开时**客户**和**顺序**实体类型。</span><span class="sxs-lookup"><span data-stu-id="9a003-143">The following example shows an **Association** element that defines the **CustomerOrders** association when foreign keys have not been exposed on the **Customer** and **Order** entity types.</span></span> <span data-ttu-id="9a003-144">**多重性**值为每个**最终**关联的指示，许多**订单**可以关联**客户**，但只有一个**客户**可以关联**顺序**。</span><span class="sxs-lookup"><span data-stu-id="9a003-144">The **Multiplicity** values for each **End** of the association indicate that many **Orders** can be associated with a **Customer**, but only one **Customer** can be associated with an **Order**.</span></span> <span data-ttu-id="9a003-145">此外， **OnDelete**元素指示所有**订单**与特定相关的**客户**和已加载到 ObjectContext 将被删除如果**客户**被删除。</span><span class="sxs-lookup"><span data-stu-id="9a003-145">Additionally, the **OnDelete** element indicates that all **Orders** that are related to a particular **Customer** and have been loaded into the ObjectContext will be deleted if the **Customer** is deleted.</span></span>

``` xml
 <Association Name="CustomerOrders">
   <End Type="ExampleModel.Customer" Role="Customer" Multiplicity="1" >
         <OnDelete Action="Cascade" />
   </End>
   <End Type="ExampleModel.Order" Role="Order" Multiplicity="*" />
 </Association>
```
 

<span data-ttu-id="9a003-146">下面的示例演示**关联**定义的元素**CustomerOrders**关联时已上公开外键**客户**并**顺序**实体类型。</span><span class="sxs-lookup"><span data-stu-id="9a003-146">The following example shows an **Association** element that defines the **CustomerOrders** association when foreign keys have been exposed on the **Customer** and **Order** entity types.</span></span> <span data-ttu-id="9a003-147">通过公开的外键，实体之间的关系进行管理**ReferentialConstraint**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-147">With foreign keys exposed, the relationship between the entities is managed with a **ReferentialConstraint** element.</span></span> <span data-ttu-id="9a003-148">相应的 AssociationSetMapping 元素不需要将此关联映射到数据源。</span><span class="sxs-lookup"><span data-stu-id="9a003-148">A corresponding AssociationSetMapping element is not necessary to map this association to the data source.</span></span>

``` xml
 <Association Name="CustomerOrders">
   <End Type="ExampleModel.Customer" Role="Customer" Multiplicity="1" >
         <OnDelete Action="Cascade" />
   </End>
   <End Type="ExampleModel.Order" Role="Order" Multiplicity="*" />
   <ReferentialConstraint>
        <Principal Role="Customer">
            <PropertyRef Name="Id" />
        </Principal>
        <Dependent Role="Order">
             <PropertyRef Name="CustomerId" />
         </Dependent>
   </ReferentialConstraint>
 </Association>
```
 

 

## <a name="associationset-element-csdl"></a><span data-ttu-id="9a003-149">AssociationSet 元素 (CSDL)</span><span class="sxs-lookup"><span data-stu-id="9a003-149">AssociationSet Element (CSDL)</span></span>

<span data-ttu-id="9a003-150">**AssociationSet**概念架构定义语言 (CSDL) 中的元素是相同类型的关联实例的逻辑容器。</span><span class="sxs-lookup"><span data-stu-id="9a003-150">The **AssociationSet** element in conceptual schema definition language (CSDL) is a logical container for association instances of the same type.</span></span> <span data-ttu-id="9a003-151">关联集为对关联实例进行分组提供了定义，以便能够将它们映射到数据源。</span><span class="sxs-lookup"><span data-stu-id="9a003-151">An association set provides a definition for grouping association instances so that they can be mapped to a data source.</span></span>  

<span data-ttu-id="9a003-152">**AssociationSet**元素可以具有下列子元素 （按所列顺序）：</span><span class="sxs-lookup"><span data-stu-id="9a003-152">The **AssociationSet** element can have the following child elements (in the order listed):</span></span>

-   <span data-ttu-id="9a003-153">文档 （允许零个或一个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-153">Documentation (zero or one elements allowed)</span></span>
-   <span data-ttu-id="9a003-154">结束 （所需的两个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-154">End (exactly two elements required)</span></span>
-   <span data-ttu-id="9a003-155">批注元素 （允许零个或多个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-155">Annotation elements (zero or more elements allowed)</span></span>

<span data-ttu-id="9a003-156">**关联**属性指定关联集包含的关联的类型。</span><span class="sxs-lookup"><span data-stu-id="9a003-156">The **Association** attribute specifies the type of association that an association set contains.</span></span> <span data-ttu-id="9a003-157">组成的一个关联集两端的实体集指定具有两个子级**最终**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-157">The entity sets that make up the ends of an association set are specified with exactly two child **End** elements.</span></span>

### <a name="applicable-attributes"></a><span data-ttu-id="9a003-158">适用的特性</span><span class="sxs-lookup"><span data-stu-id="9a003-158">Applicable Attributes</span></span>

<span data-ttu-id="9a003-159">下表描述了可应用于的特性**AssociationSet**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-159">The table below describes the attributes that can be applied to the **AssociationSet** element.</span></span>

| <span data-ttu-id="9a003-160">特性名</span><span class="sxs-lookup"><span data-stu-id="9a003-160">Attribute Name</span></span>  | <span data-ttu-id="9a003-161">是否必需</span><span class="sxs-lookup"><span data-stu-id="9a003-161">Is Required</span></span> | <span data-ttu-id="9a003-162">“值”</span><span class="sxs-lookup"><span data-stu-id="9a003-162">Value</span></span>                                                                                                                                                             |
|:----------------|:------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9a003-163">**名称**</span><span class="sxs-lookup"><span data-stu-id="9a003-163">**Name**</span></span>        | <span data-ttu-id="9a003-164">是</span><span class="sxs-lookup"><span data-stu-id="9a003-164">Yes</span></span>         | <span data-ttu-id="9a003-165">实体集的名称。</span><span class="sxs-lookup"><span data-stu-id="9a003-165">The name of the entity set.</span></span> <span data-ttu-id="9a003-166">值**名称**属性不能为的值相同**关联**属性。</span><span class="sxs-lookup"><span data-stu-id="9a003-166">The value of the **Name** attribute cannot be the same as the value of the **Association** attribute.</span></span>                                 |
| <span data-ttu-id="9a003-167">**关联**</span><span class="sxs-lookup"><span data-stu-id="9a003-167">**Association**</span></span> | <span data-ttu-id="9a003-168">是</span><span class="sxs-lookup"><span data-stu-id="9a003-168">Yes</span></span>         | <span data-ttu-id="9a003-169">关联集包含其实例的关联的完全限定名称。</span><span class="sxs-lookup"><span data-stu-id="9a003-169">The fully-qualified name of the association that the association set contains instances of.</span></span> <span data-ttu-id="9a003-170">关联必须与关联集位于同一个命名空间中。</span><span class="sxs-lookup"><span data-stu-id="9a003-170">The association must be in the same namespace as the association set.</span></span> |

 

> [!NOTE]
> <span data-ttu-id="9a003-171">可以将任意数量的 （自定义 XML 特性） 的批注特性应用于**AssociationSet**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-171">Any number of annotation attributes (custom XML attributes) may be applied to the **AssociationSet** element.</span></span> <span data-ttu-id="9a003-172">然而，自定义特性可能不属于为 CSDL 保留的任何 XML 命名空间。</span><span class="sxs-lookup"><span data-stu-id="9a003-172">However, custom attributes may not belong to any XML namespace that is reserved for CSDL.</span></span> <span data-ttu-id="9a003-173">任何两个自定义特性的完全限定名称都不能相同。</span><span class="sxs-lookup"><span data-stu-id="9a003-173">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

 

### <a name="example"></a><span data-ttu-id="9a003-174">示例</span><span class="sxs-lookup"><span data-stu-id="9a003-174">Example</span></span>

<span data-ttu-id="9a003-175">下面的示例演示**EntityContainer**元素具有两个**AssociationSet**元素：</span><span class="sxs-lookup"><span data-stu-id="9a003-175">The following example shows an **EntityContainer** element with two **AssociationSet** elements:</span></span>

``` xml
 <EntityContainer Name="BooksContainer" >
   <EntitySet Name="Books" EntityType="BooksModel.Book" />
   <EntitySet Name="Publishers" EntityType="BooksModel.Publisher" />
   <EntitySet Name="Authors" EntityType="BooksModel.Author" />
   <AssociationSet Name="PublishedBy" Association="BooksModel.PublishedBy">
     <End Role="Book" EntitySet="Books" />
     <End Role="Publisher" EntitySet="Publishers" />
   </AssociationSet>
   <AssociationSet Name="WrittenBy" Association="BooksModel.WrittenBy">
     <End Role="Book" EntitySet="Books" />
     <End Role="Author" EntitySet="Authors" />
   </AssociationSet>
 </EntityContainer>
```
 

 

## <a name="collectiontype-element-csdl"></a><span data-ttu-id="9a003-176">CollectionType 元素 (CSDL)</span><span class="sxs-lookup"><span data-stu-id="9a003-176">CollectionType Element (CSDL)</span></span>

<span data-ttu-id="9a003-177">**CollectionType**概念架构定义语言 (CSDL) 中的元素指定的函数参数或函数返回类型是一个集合。</span><span class="sxs-lookup"><span data-stu-id="9a003-177">The **CollectionType** element in conceptual schema definition language (CSDL) specifies that a function parameter or function return type is a collection.</span></span> <span data-ttu-id="9a003-178">**CollectionType**元素可以是参数元素或 ReturnType （函数） 元素的子级。</span><span class="sxs-lookup"><span data-stu-id="9a003-178">The **CollectionType** element can be a child of the Parameter element or the ReturnType (Function) element.</span></span> <span data-ttu-id="9a003-179">可以通过使用指定的集合类型**类型**特性或以下子元素之一：</span><span class="sxs-lookup"><span data-stu-id="9a003-179">The type of collection can be specified by using either the **Type** attribute or one of the following child elements:</span></span>

-   <span data-ttu-id="9a003-180">**CollectionType**</span><span class="sxs-lookup"><span data-stu-id="9a003-180">**CollectionType**</span></span>
-   <span data-ttu-id="9a003-181">ReferenceType</span><span class="sxs-lookup"><span data-stu-id="9a003-181">ReferenceType</span></span>
-   <span data-ttu-id="9a003-182">RowType</span><span class="sxs-lookup"><span data-stu-id="9a003-182">RowType</span></span>
-   <span data-ttu-id="9a003-183">TypeRef</span><span class="sxs-lookup"><span data-stu-id="9a003-183">TypeRef</span></span>

> [!NOTE]
> <span data-ttu-id="9a003-184">如果两个指定集合的类型，不会验证模型**类型**属性和子元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-184">A model will not validate if the type of a collection is specified with both the **Type** attribute and a child element.</span></span>

 

### <a name="applicable-attributes"></a><span data-ttu-id="9a003-185">适用的特性</span><span class="sxs-lookup"><span data-stu-id="9a003-185">Applicable Attributes</span></span>

<span data-ttu-id="9a003-186">下表介绍可应用于的特性**CollectionType**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-186">The following table describes the attributes that can be applied to the **CollectionType** element.</span></span> <span data-ttu-id="9a003-187">请注意， **DefaultValue**， **MaxLength**， **FixedLength**，**精度**，**规模**， **Unicode**，并**排序规则**属性都只适用于集合的**Edmsimpletype**。</span><span class="sxs-lookup"><span data-stu-id="9a003-187">Note that the **DefaultValue**, **MaxLength**, **FixedLength**, **Precision**, **Scale**, **Unicode**, and **Collation** attributes are only applicable to collections of **EDMSimpleTypes**.</span></span>

| <span data-ttu-id="9a003-188">特性名</span><span class="sxs-lookup"><span data-stu-id="9a003-188">Attribute Name</span></span>                                                          | <span data-ttu-id="9a003-189">是否必需</span><span class="sxs-lookup"><span data-stu-id="9a003-189">Is Required</span></span> | <span data-ttu-id="9a003-190">“值”</span><span class="sxs-lookup"><span data-stu-id="9a003-190">Value</span></span>                                                                                                                                                                                                                            |
|:------------------------------------------------------------------------|:------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9a003-191">**Type**</span><span class="sxs-lookup"><span data-stu-id="9a003-191">**Type**</span></span>                                                                | <span data-ttu-id="9a003-192">否</span><span class="sxs-lookup"><span data-stu-id="9a003-192">No</span></span>          | <span data-ttu-id="9a003-193">集合的类型。</span><span class="sxs-lookup"><span data-stu-id="9a003-193">The type of the collection.</span></span>                                                                                                                                                                                                      |
| <span data-ttu-id="9a003-194">**可以为 null**</span><span class="sxs-lookup"><span data-stu-id="9a003-194">**Nullable**</span></span>                                                            | <span data-ttu-id="9a003-195">否</span><span class="sxs-lookup"><span data-stu-id="9a003-195">No</span></span>          | <span data-ttu-id="9a003-196">**True** （默认值） 或**False**具体取决于属性是否可以具有 null 值。</span><span class="sxs-lookup"><span data-stu-id="9a003-196">**True** (the default value) or **False** depending on whether the property can have a null value.</span></span> <br/> [!NOTE]                                                                                                                 |
| <span data-ttu-id="9a003-197">> 在 CSDL v1 中，复杂类型属性必须具有`Nullable="False"`。</span><span class="sxs-lookup"><span data-stu-id="9a003-197">> In the CSDL v1, a complex type property must have `Nullable="False"`.</span></span> |             |                                                                                                                                                                                                                                  |
| <span data-ttu-id="9a003-198">**DefaultValue**</span><span class="sxs-lookup"><span data-stu-id="9a003-198">**DefaultValue**</span></span>                                                        | <span data-ttu-id="9a003-199">否</span><span class="sxs-lookup"><span data-stu-id="9a003-199">No</span></span>          | <span data-ttu-id="9a003-200">属性的默认值。</span><span class="sxs-lookup"><span data-stu-id="9a003-200">The default value of the property.</span></span>                                                                                                                                                                                               |
| <span data-ttu-id="9a003-201">**MaxLength**</span><span class="sxs-lookup"><span data-stu-id="9a003-201">**MaxLength**</span></span>                                                           | <span data-ttu-id="9a003-202">否</span><span class="sxs-lookup"><span data-stu-id="9a003-202">No</span></span>          | <span data-ttu-id="9a003-203">属性值的最大长度。</span><span class="sxs-lookup"><span data-stu-id="9a003-203">The maximum length of the property value.</span></span>                                                                                                                                                                                        |
| <span data-ttu-id="9a003-204">**FixedLength**</span><span class="sxs-lookup"><span data-stu-id="9a003-204">**FixedLength**</span></span>                                                         | <span data-ttu-id="9a003-205">否</span><span class="sxs-lookup"><span data-stu-id="9a003-205">No</span></span>          | <span data-ttu-id="9a003-206">**True**或**False**具体取决于属性值是否将作为固定的长度字符串存储。</span><span class="sxs-lookup"><span data-stu-id="9a003-206">**True** or **False** depending on whether the property value will be stored as a fixed length string.</span></span>                                                                                                                           |
| <span data-ttu-id="9a003-207">**精度**</span><span class="sxs-lookup"><span data-stu-id="9a003-207">**Precision**</span></span>                                                           | <span data-ttu-id="9a003-208">否</span><span class="sxs-lookup"><span data-stu-id="9a003-208">No</span></span>          | <span data-ttu-id="9a003-209">属性值的精度。</span><span class="sxs-lookup"><span data-stu-id="9a003-209">The precision of the property value.</span></span>                                                                                                                                                                                             |
| <span data-ttu-id="9a003-210">缩放</span><span class="sxs-lookup"><span data-stu-id="9a003-210">**Scale**</span></span>                                                               | <span data-ttu-id="9a003-211">否</span><span class="sxs-lookup"><span data-stu-id="9a003-211">No</span></span>          | <span data-ttu-id="9a003-212">属性值的刻度。</span><span class="sxs-lookup"><span data-stu-id="9a003-212">The scale of the property value.</span></span>                                                                                                                                                                                                 |
| <span data-ttu-id="9a003-213">**SRID**</span><span class="sxs-lookup"><span data-stu-id="9a003-213">**SRID**</span></span>                                                                | <span data-ttu-id="9a003-214">否</span><span class="sxs-lookup"><span data-stu-id="9a003-214">No</span></span>          | <span data-ttu-id="9a003-215">系统的空间引用标识符。</span><span class="sxs-lookup"><span data-stu-id="9a003-215">Spatial System Reference Identifier.</span></span> <span data-ttu-id="9a003-216">仅对空间类型的属性有效。</span><span class="sxs-lookup"><span data-stu-id="9a003-216">Valid only for properties of spatial types.</span></span>   <span data-ttu-id="9a003-217">有关详细信息，请参阅[SRID](http://en.wikipedia.org/wiki/SRID)和[SRID (SQL Server)](https://msdn.microsoft.com/library/bb964707.aspx)</span><span class="sxs-lookup"><span data-stu-id="9a003-217">For more information, see [SRID](http://en.wikipedia.org/wiki/SRID) and [SRID (SQL Server)](https://msdn.microsoft.com/library/bb964707.aspx)</span></span> |
| <span data-ttu-id="9a003-218">**Unicode**</span><span class="sxs-lookup"><span data-stu-id="9a003-218">**Unicode**</span></span>                                                             | <span data-ttu-id="9a003-219">否</span><span class="sxs-lookup"><span data-stu-id="9a003-219">No</span></span>          | <span data-ttu-id="9a003-220">**True**或**False**具体取决于是否在属性值将存储为 Unicode 字符串。</span><span class="sxs-lookup"><span data-stu-id="9a003-220">**True** or **False** depending on whether the property value will be stored as a Unicode string.</span></span>                                                                                                                                |
| <span data-ttu-id="9a003-221">**排序规则**</span><span class="sxs-lookup"><span data-stu-id="9a003-221">**Collation**</span></span>                                                           | <span data-ttu-id="9a003-222">否</span><span class="sxs-lookup"><span data-stu-id="9a003-222">No</span></span>          | <span data-ttu-id="9a003-223">指定要在数据源中使用的排序序列的字符串。</span><span class="sxs-lookup"><span data-stu-id="9a003-223">A string that specifies the collating sequence to be used in the data source.</span></span>                                                                                                                                                    |

 

> [!NOTE]
> <span data-ttu-id="9a003-224">可以将任意数量的 （自定义 XML 特性） 的批注特性应用于**CollectionType**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-224">Any number of annotation attributes (custom XML attributes) may be applied to the **CollectionType** element.</span></span> <span data-ttu-id="9a003-225">然而，自定义特性可能不属于为 CSDL 保留的任何 XML 命名空间。</span><span class="sxs-lookup"><span data-stu-id="9a003-225">However, custom attributes may not belong to any XML namespace that is reserved for CSDL.</span></span> <span data-ttu-id="9a003-226">任何两个自定义特性的完全限定名称都不能相同。</span><span class="sxs-lookup"><span data-stu-id="9a003-226">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

 

### <a name="example"></a><span data-ttu-id="9a003-227">示例</span><span class="sxs-lookup"><span data-stu-id="9a003-227">Example</span></span>

<span data-ttu-id="9a003-228">下面的示例演示使用的模型定义函数**CollectionType**元素来指定该函数返回一系列**人员**实体类型 (指定与**ElementType**属性)。</span><span class="sxs-lookup"><span data-stu-id="9a003-228">The following example shows a model-defined function that that uses a **CollectionType** element to specify that the function returns a collection of **Person** entity types (as specified with the **ElementType** attribute).</span></span>

``` xml
 <Function Name="LastNamesAfter">
        <Parameter Name="someString" Type="Edm.String"/>
        <ReturnType>
             <CollectionType  ElementType="SchoolModel.Person"/>
        </ReturnType>
        <DefiningExpression>
             SELECT VALUE p
             FROM SchoolEntities.People AS p
             WHERE p.LastName >= someString
        </DefiningExpression>
 </Function>
```
 

<span data-ttu-id="9a003-229">下面的示例演示使用的模型定义函数**CollectionType**元素来指定该函数返回的行集合 (中指定的那样**RowType**元素)。</span><span class="sxs-lookup"><span data-stu-id="9a003-229">The following example shows a model-defined function that uses a **CollectionType** element to specify that the function returns a collection of rows (as specified in the **RowType** element).</span></span>

``` xml
 <Function Name="LastNamesAfter">
   <Parameter Name="someString" Type="Edm.String" />
   <ReturnType>
    <CollectionType>
      <RowType>
        <Property Name="FirstName" Type="Edm.String" Nullable="false" />
        <Property Name="LastName" Type="Edm.String" Nullable="false" />
      </RowType>
    </CollectionType>
   </ReturnType>
   <DefiningExpression>
             SELECT VALUE ROW(p.FirstName, p.LastName)
             FROM SchoolEntities.People AS p
             WHERE p.LastName &gt;= somestring
   </DefiningExpression>
 </Function>
```
 

<span data-ttu-id="9a003-230">下面的示例演示使用的模型定义函数**CollectionType**元素来指定该函数接受作为参数的集合**部门**实体类型。</span><span class="sxs-lookup"><span data-stu-id="9a003-230">The following example shows a model-defined function that uses the **CollectionType** element to specify that the function accepts as a parameter a collection of **Department** entity types.</span></span>

``` xml
 <Function Name="GetAvgBudget">
      <Parameter Name="Departments">
          <CollectionType>
             <TypeRef Type="SchoolModel.Department"/>
          </CollectionType>
           </Parameter>
       <ReturnType Type="Collection(Edm.Decimal)"/>
       <DefiningExpression>
             SELECT VALUE AVG(d.Budget) FROM Departments AS d
       </DefiningExpression>
 </Function>
```
 

 

## <a name="complextype-element-csdl"></a><span data-ttu-id="9a003-231">ComplexType 元素 (CSDL)</span><span class="sxs-lookup"><span data-stu-id="9a003-231">ComplexType Element (CSDL)</span></span>

<span data-ttu-id="9a003-232">一个**ComplexType**元素定义组成的数据结构**EdmSimpleType**属性或其他复杂类型。</span><span class="sxs-lookup"><span data-stu-id="9a003-232">A **ComplexType** element defines a data structure composed of **EdmSimpleType** properties or other complex types.</span></span>  <span data-ttu-id="9a003-233">复杂类型可以是实体类型的属性或其他复杂类型的属性。</span><span class="sxs-lookup"><span data-stu-id="9a003-233">A complex type can be a property of an entity type or another complex type.</span></span> <span data-ttu-id="9a003-234">复杂类型类似于复杂类型定义数据中的实体类型。</span><span class="sxs-lookup"><span data-stu-id="9a003-234">A complex type is similar to an entity type in that a complex type defines data.</span></span> <span data-ttu-id="9a003-235">但是，在复杂类型与实体类型之间仍存在着一些重要区别：</span><span class="sxs-lookup"><span data-stu-id="9a003-235">However, there are some key differences between complex types and entity types:</span></span>

-   <span data-ttu-id="9a003-236">复杂类型没有标识（或键），因此不能独立存在。</span><span class="sxs-lookup"><span data-stu-id="9a003-236">Complex types do not have identities (or keys) and therefore cannot exist independently.</span></span> <span data-ttu-id="9a003-237">复杂类型只能作为实体类型或其他复杂类型的属性而存在。</span><span class="sxs-lookup"><span data-stu-id="9a003-237">Complex types can only exist as properties of entity types or other complex types.</span></span>
-   <span data-ttu-id="9a003-238">复杂类型不能参与关联。</span><span class="sxs-lookup"><span data-stu-id="9a003-238">Complex types cannot participate in associations.</span></span> <span data-ttu-id="9a003-239">既不关联端可以是复杂类型，并因此不能为复杂类型定义导航属性。</span><span class="sxs-lookup"><span data-stu-id="9a003-239">Neither end of an association can be a complex type, and therefore navigation properties cannot be defined for complex types.</span></span>
-   <span data-ttu-id="9a003-240">复杂类型属性不能具有 null 值，但可以将复杂类型的每个标量属性设置为 null。</span><span class="sxs-lookup"><span data-stu-id="9a003-240">A complex type property cannot have a null value, though the scalar properties of a complex type may each be set to null.</span></span>

<span data-ttu-id="9a003-241">一个**ComplexType**元素可以具有下列子元素 （按所列顺序）：</span><span class="sxs-lookup"><span data-stu-id="9a003-241">A **ComplexType** element can have the following child elements (in the order listed):</span></span>

-   <span data-ttu-id="9a003-242">文档 （零个或一个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-242">Documentation (zero or one element)</span></span>
-   <span data-ttu-id="9a003-243">属性 （零个或多个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-243">Property (zero or more elements)</span></span>
-   <span data-ttu-id="9a003-244">批注元素 （零个或多个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-244">Annotation elements (zero or more elements)</span></span>

<span data-ttu-id="9a003-245">下表描述了可应用于的特性**ComplexType**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-245">The table below describes the attributes that can be applied to the **ComplexType** element.</span></span>

| <span data-ttu-id="9a003-246">特性名</span><span class="sxs-lookup"><span data-stu-id="9a003-246">Attribute Name</span></span>                                                                                                 | <span data-ttu-id="9a003-247">是否必需</span><span class="sxs-lookup"><span data-stu-id="9a003-247">Is Required</span></span> | <span data-ttu-id="9a003-248">“值”</span><span class="sxs-lookup"><span data-stu-id="9a003-248">Value</span></span>                                                                                                                                                                               |
|:---------------------------------------------------------------------------------------------------------------|:------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9a003-249">name</span><span class="sxs-lookup"><span data-stu-id="9a003-249">Name</span></span>                                                                                                           | <span data-ttu-id="9a003-250">是</span><span class="sxs-lookup"><span data-stu-id="9a003-250">Yes</span></span>         | <span data-ttu-id="9a003-251">复杂类型的名称。</span><span class="sxs-lookup"><span data-stu-id="9a003-251">The name of the complex type.</span></span> <span data-ttu-id="9a003-252">复杂类型的名称不能与模型作用域中的其他复杂类型、实体类型或关联的名称相同。</span><span class="sxs-lookup"><span data-stu-id="9a003-252">The name of a complex type cannot be the same as the name of another complex type, entity type, or association that is within the scope of the model.</span></span> |
| <span data-ttu-id="9a003-253">BaseType</span><span class="sxs-lookup"><span data-stu-id="9a003-253">BaseType</span></span>                                                                                                       | <span data-ttu-id="9a003-254">否</span><span class="sxs-lookup"><span data-stu-id="9a003-254">No</span></span>          | <span data-ttu-id="9a003-255">作为所定义的复杂类型的基类型的另一个复杂类型的名称。</span><span class="sxs-lookup"><span data-stu-id="9a003-255">The name of another complex type that is the base type of the complex type that is being defined.</span></span> <br/> [!NOTE]                                                                     |
| <span data-ttu-id="9a003-256">> 此属性不是适用于 CSDL v1。</span><span class="sxs-lookup"><span data-stu-id="9a003-256">> This attribute is not applicable in CSDL v1.</span></span> <span data-ttu-id="9a003-257">在该版本中不支持复杂类型的继承。</span><span class="sxs-lookup"><span data-stu-id="9a003-257">Inheritance for complex types is not supported in that version.</span></span> |             |                                                                                                                                                                                     |
| <span data-ttu-id="9a003-258">抽象</span><span class="sxs-lookup"><span data-stu-id="9a003-258">Abstract</span></span>                                                                                                       | <span data-ttu-id="9a003-259">否</span><span class="sxs-lookup"><span data-stu-id="9a003-259">No</span></span>          | <span data-ttu-id="9a003-260">**True**或**False** （默认值） 具体取决于复杂类型是否为抽象类型。</span><span class="sxs-lookup"><span data-stu-id="9a003-260">**True** or **False** (the default value) depending on whether the complex type is an abstract type.</span></span> <br/> [!NOTE]                                                                  |
| <span data-ttu-id="9a003-261">> 此属性不是适用于 CSDL v1。</span><span class="sxs-lookup"><span data-stu-id="9a003-261">> This attribute is not applicable in CSDL v1.</span></span> <span data-ttu-id="9a003-262">该版本中的复杂类型不能是抽象类型。</span><span class="sxs-lookup"><span data-stu-id="9a003-262">Complex types in that version cannot be abstract types.</span></span>         |             |                                                                                                                                                                                     |

 

> [!NOTE]
> <span data-ttu-id="9a003-263">可以将任意数量的 （自定义 XML 特性） 的批注特性应用于**ComplexType**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-263">Any number of annotation attributes (custom XML attributes) may be applied to the **ComplexType** element.</span></span> <span data-ttu-id="9a003-264">然而，自定义特性可能不属于为 CSDL 保留的任何 XML 命名空间。</span><span class="sxs-lookup"><span data-stu-id="9a003-264">However, custom attributes may not belong to any XML namespace that is reserved for CSDL.</span></span> <span data-ttu-id="9a003-265">任何两个自定义特性的完全限定名称都不能相同。</span><span class="sxs-lookup"><span data-stu-id="9a003-265">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

 

### <a name="example"></a><span data-ttu-id="9a003-266">示例</span><span class="sxs-lookup"><span data-stu-id="9a003-266">Example</span></span>

<span data-ttu-id="9a003-267">下面的示例演示一个复杂类型，**地址**，使用**EdmSimpleType**属性**StreetAddress**，**城市**， **StateOrProvince**，**国家/地区**，和**PostalCode**。</span><span class="sxs-lookup"><span data-stu-id="9a003-267">The following example shows a complex type, **Address**, with the **EdmSimpleType** properties **StreetAddress**, **City**, **StateOrProvince**, **Country**, and **PostalCode**.</span></span>

``` xml
 <ComplexType Name="Address" >
   <Property Type="String" Name="StreetAddress" Nullable="false" />
   <Property Type="String" Name="City" Nullable="false" />
   <Property Type="String" Name="StateOrProvince" Nullable="false" />
   <Property Type="String" Name="Country" Nullable="false" />
   <Property Type="String" Name="PostalCode" Nullable="false" />
 </ComplexType>
```
 

<span data-ttu-id="9a003-268">若要将复杂类型定义**地址**（如上所示） 作为实体类型的属性必须声明实体类型定义中的属性类型。</span><span class="sxs-lookup"><span data-stu-id="9a003-268">To define the complex type **Address** (above) as a property of an entity type, you must declare the property type in the entity type definition.</span></span> <span data-ttu-id="9a003-269">下面的示例演示**地址**实体类型上的复杂类型属性 (**发布服务器**):</span><span class="sxs-lookup"><span data-stu-id="9a003-269">The following example shows the **Address** property as a complex type on an entity type (**Publisher**):</span></span>

``` xml
 <EntityType Name="Publisher">
       <Key>
         <PropertyRef Name="Id" />
       </Key>
       <Property Type="Int32" Name="Id" Nullable="false" />
       <Property Type="String" Name="Name" Nullable="false" />
       <Property Type="BooksModel.Address" Name="Address" Nullable="false" />
       <NavigationProperty Name="Books" Relationship="BooksModel.PublishedBy"
                           FromRole="Publisher" ToRole="Book" />
     </EntityType>
```
 

 

## <a name="definingexpression-element-csdl"></a><span data-ttu-id="9a003-270">DefiningExpression 元素 (CSDL)</span><span class="sxs-lookup"><span data-stu-id="9a003-270">DefiningExpression Element (CSDL)</span></span>

<span data-ttu-id="9a003-271">**DefiningExpression**概念架构定义语言 (CSDL) 中的元素包含在概念模型中定义了一个函数的 Entity SQL 表达式。</span><span class="sxs-lookup"><span data-stu-id="9a003-271">The **DefiningExpression** element in conceptual schema definition language (CSDL) contains an Entity SQL expression that defines a function in the conceptual model.</span></span>  

> [!NOTE]
> <span data-ttu-id="9a003-272">出于验证目的**DefiningExpression**元素可以包含任意内容。</span><span class="sxs-lookup"><span data-stu-id="9a003-272">For validation purposes, a **DefiningExpression** element can contain arbitrary content.</span></span> <span data-ttu-id="9a003-273">但是，实体框架将引发异常在运行时**DefiningExpression**元素不包含有效的实体 SQL。</span><span class="sxs-lookup"><span data-stu-id="9a003-273">However, Entity Framework will throw an exception at runtime if a **DefiningExpression** element does not contain valid Entity SQL.</span></span>

 

### <a name="applicable-attributes"></a><span data-ttu-id="9a003-274">适用的特性</span><span class="sxs-lookup"><span data-stu-id="9a003-274">Applicable Attributes</span></span>

<span data-ttu-id="9a003-275">可以将任意数量的 （自定义 XML 特性） 的批注特性应用于**DefiningExpression**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-275">Any number of annotation attributes (custom XML attributes) may be applied to the **DefiningExpression** element.</span></span> <span data-ttu-id="9a003-276">然而，自定义特性可能不属于为 CSDL 保留的任何 XML 命名空间。</span><span class="sxs-lookup"><span data-stu-id="9a003-276">However, custom attributes may not belong to any XML namespace that is reserved for CSDL.</span></span> <span data-ttu-id="9a003-277">任何两个自定义特性的完全限定名称都不能相同。</span><span class="sxs-lookup"><span data-stu-id="9a003-277">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

### <a name="example"></a><span data-ttu-id="9a003-278">示例</span><span class="sxs-lookup"><span data-stu-id="9a003-278">Example</span></span>

<span data-ttu-id="9a003-279">下面的示例使用**DefiningExpression**元素来定义返回的年数，因为已发表一本书的函数。</span><span class="sxs-lookup"><span data-stu-id="9a003-279">The following example uses a **DefiningExpression** element to define a function that returns the number of years since a book was published.</span></span> <span data-ttu-id="9a003-280">内容**DefiningExpression**元素编写实体 SQL 中。</span><span class="sxs-lookup"><span data-stu-id="9a003-280">The content of the **DefiningExpression** element is written in Entity SQL.</span></span>

``` xml
 <Function Name="GetYearsInPrint" ReturnType="Edm.Int32" >
       <Parameter Name="book" Type="BooksModel.Book" />
       <DefiningExpression>
         Year(CurrentDateTime()) - Year(cast(book.PublishedDate as DateTime))
       </DefiningExpression>
     </Function>
```
 

 

## <a name="dependent-element-csdl"></a><span data-ttu-id="9a003-281">Dependent 元素 (CSDL)</span><span class="sxs-lookup"><span data-stu-id="9a003-281">Dependent Element (CSDL)</span></span>

<span data-ttu-id="9a003-282">**依赖**概念架构定义语言 (CSDL) 中的元素是 ReferentialConstraint 元素的子元素，定义引用约束的依赖端。</span><span class="sxs-lookup"><span data-stu-id="9a003-282">The **Dependent** element in conceptual schema definition language (CSDL) is a child element to the ReferentialConstraint element and defines the dependent end of a referential constraint.</span></span> <span data-ttu-id="9a003-283">一个**ReferentialConstraint**元素定义的是关系数据库中的引用完整性约束类似的功能。</span><span class="sxs-lookup"><span data-stu-id="9a003-283">A **ReferentialConstraint** element defines functionality that is similar to a referential integrity constraint in a relational database.</span></span> <span data-ttu-id="9a003-284">与数据库表中的一个（或多个）列可以引用另一个表的主键相同，实体类型的一个（或多个）属性可以引用另一个实体类型的实体键。</span><span class="sxs-lookup"><span data-stu-id="9a003-284">In the same way that a column (or columns) from a database table can reference the primary key of another table, a property (or properties) of an entity type can reference the entity key of another entity type.</span></span> <span data-ttu-id="9a003-285">引用的实体类型称为*主体端*的约束。</span><span class="sxs-lookup"><span data-stu-id="9a003-285">The entity type that is referenced is called the *principal end* of the constraint.</span></span> <span data-ttu-id="9a003-286">引用主体端的实体类型称为*依赖端*的约束。</span><span class="sxs-lookup"><span data-stu-id="9a003-286">The entity type that references the principal end is called the *dependent end* of the constraint.</span></span> <span data-ttu-id="9a003-287">**PropertyRef**元素用于指定哪些键引用主体端。</span><span class="sxs-lookup"><span data-stu-id="9a003-287">**PropertyRef** elements are used to specify which keys reference the principal end.</span></span>

<span data-ttu-id="9a003-288">**依赖**元素可以具有下列子元素 （按所列顺序）：</span><span class="sxs-lookup"><span data-stu-id="9a003-288">The **Dependent** element can have the following child elements (in the order listed):</span></span>

-   <span data-ttu-id="9a003-289">PropertyRef （一个或多个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-289">PropertyRef (one or more elements)</span></span>
-   <span data-ttu-id="9a003-290">批注元素 （零个或多个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-290">Annotation elements (zero or more elements)</span></span>

### <a name="applicable-attributes"></a><span data-ttu-id="9a003-291">适用的特性</span><span class="sxs-lookup"><span data-stu-id="9a003-291">Applicable Attributes</span></span>

<span data-ttu-id="9a003-292">下表描述了可应用于的特性**依赖**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-292">The table below describes the attributes that can be applied to the **Dependent** element.</span></span>

| <span data-ttu-id="9a003-293">特性名</span><span class="sxs-lookup"><span data-stu-id="9a003-293">Attribute Name</span></span> | <span data-ttu-id="9a003-294">是否必需</span><span class="sxs-lookup"><span data-stu-id="9a003-294">Is Required</span></span> | <span data-ttu-id="9a003-295">“值”</span><span class="sxs-lookup"><span data-stu-id="9a003-295">Value</span></span>                                                                |
|:---------------|:------------|:---------------------------------------------------------------------|
| <span data-ttu-id="9a003-296">**角色**</span><span class="sxs-lookup"><span data-stu-id="9a003-296">**Role**</span></span>       | <span data-ttu-id="9a003-297">是</span><span class="sxs-lookup"><span data-stu-id="9a003-297">Yes</span></span>         | <span data-ttu-id="9a003-298">关联的依赖端的实体类型的名称。</span><span class="sxs-lookup"><span data-stu-id="9a003-298">The name of the entity type on the dependent end of the association.</span></span> |

 

> [!NOTE]
> <span data-ttu-id="9a003-299">可以将任意数量的 （自定义 XML 特性） 的批注特性应用于**依赖**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-299">Any number of annotation attributes (custom XML attributes) may be applied to the **Dependent** element.</span></span> <span data-ttu-id="9a003-300">然而，自定义特性可能不属于为 CSDL 保留的任何 XML 命名空间。</span><span class="sxs-lookup"><span data-stu-id="9a003-300">However, custom attributes may not belong to any XML namespace that is reserved for CSDL.</span></span> <span data-ttu-id="9a003-301">任何两个自定义特性的完全限定名称都不能相同。</span><span class="sxs-lookup"><span data-stu-id="9a003-301">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

 

### <a name="example"></a><span data-ttu-id="9a003-302">示例</span><span class="sxs-lookup"><span data-stu-id="9a003-302">Example</span></span>

<span data-ttu-id="9a003-303">下面的示例演示**ReferentialConstraint**元素的定义的一部分用作**PublishedBy**关联。</span><span class="sxs-lookup"><span data-stu-id="9a003-303">The following example shows a **ReferentialConstraint** element being used as part of the definition of the **PublishedBy** association.</span></span> <span data-ttu-id="9a003-304">**PublisherId**的属性**书籍**实体类型构成引用约束的依赖端。</span><span class="sxs-lookup"><span data-stu-id="9a003-304">The **PublisherId** property of the **Book** entity type makes up the dependent end of the referential constraint.</span></span>

``` xml
 <Association Name="PublishedBy">
   <End Type="BooksModel.Book" Role="Book" Multiplicity="*" >
   </End>
   <End Type="BooksModel.Publisher" Role="Publisher" Multiplicity="1" />
   <ReferentialConstraint>
     <Principal Role="Publisher">
       <PropertyRef Name="Id" />
     </Principal>
     <Dependent Role="Book">
       <PropertyRef Name="PublisherId" />
     </Dependent>
   </ReferentialConstraint>
 </Association>
```
 

 

## <a name="documentation-element-csdl"></a><span data-ttu-id="9a003-305">Documentation 元素 (CSDL)</span><span class="sxs-lookup"><span data-stu-id="9a003-305">Documentation Element (CSDL)</span></span>

<span data-ttu-id="9a003-306">**文档**概念架构定义语言 (CSDL) 中的元素可以用于提供有关的对象的父元素中定义的信息。</span><span class="sxs-lookup"><span data-stu-id="9a003-306">The **Documentation** element in conceptual schema definition language (CSDL) can be used to provide information about an object that is defined in a parent element.</span></span> <span data-ttu-id="9a003-307">在.edmx 文件中，当**文档**元素是显示为 （如实体、 关联或属性），在 EF 设计器的设计图面上的对象的内容的元素的子级**文档**元素将显示在 Visual Studio**属性**窗口对象。</span><span class="sxs-lookup"><span data-stu-id="9a003-307">In an .edmx file, when the **Documentation** element is a child of an element that appears as an object on the design surface of the EF Designer  (such as an entity, association, or property), the contents of the **Documentation** element will appear in the Visual Studio **Properties** window for the object.</span></span>

<span data-ttu-id="9a003-308">**文档**元素可以具有下列子元素 （按所列顺序）：</span><span class="sxs-lookup"><span data-stu-id="9a003-308">The **Documentation** element can have the following child elements (in the order listed):</span></span>

-   <span data-ttu-id="9a003-309">**摘要**： 父元素的简要说明。</span><span class="sxs-lookup"><span data-stu-id="9a003-309">**Summary**: A brief description of the parent element.</span></span> <span data-ttu-id="9a003-310">（零个或一个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-310">(zero or one element)</span></span>
-   <span data-ttu-id="9a003-311">**LongDescription**： 父元素的详细说明。</span><span class="sxs-lookup"><span data-stu-id="9a003-311">**LongDescription**: An extensive description of the parent element.</span></span> <span data-ttu-id="9a003-312">（零个或一个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-312">(zero or one element)</span></span>
-   <span data-ttu-id="9a003-313">批注元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-313">Annotation elements.</span></span> <span data-ttu-id="9a003-314">（零个或多个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-314">(zero or more elements)</span></span>

### <a name="applicable-attributes"></a><span data-ttu-id="9a003-315">适用的特性</span><span class="sxs-lookup"><span data-stu-id="9a003-315">Applicable Attributes</span></span>

<span data-ttu-id="9a003-316">可以将任意数量的 （自定义 XML 特性） 的批注特性应用于**文档**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-316">Any number of annotation attributes (custom XML attributes) may be applied to the **Documentation** element.</span></span> <span data-ttu-id="9a003-317">然而，自定义特性可能不属于为 CSDL 保留的任何 XML 命名空间。</span><span class="sxs-lookup"><span data-stu-id="9a003-317">However, custom attributes may not belong to any XML namespace that is reserved for CSDL.</span></span> <span data-ttu-id="9a003-318">任何两个自定义特性的完全限定名称都不能相同。</span><span class="sxs-lookup"><span data-stu-id="9a003-318">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

### <a name="example"></a><span data-ttu-id="9a003-319">示例</span><span class="sxs-lookup"><span data-stu-id="9a003-319">Example</span></span>

<span data-ttu-id="9a003-320">下面的示例演示**文档**元素作为 EntityType 元素的子元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-320">The following example shows the **Documentation** element as a child element of an EntityType element.</span></span> <span data-ttu-id="9a003-321">如果下面的代码段是 CSDL 中内容的.edmx 文件的内容**摘要**并**LongDescription**元素会显示在 Visual Studio**属性**窗口上单击时`Customer`实体类型。</span><span class="sxs-lookup"><span data-stu-id="9a003-321">If the snippet below were in the CSDL content of an .edmx file, the contents of the **Summary** and **LongDescription** elements would appear in the Visual Studio **Properties** window when you click on the `Customer` entity type.</span></span>

``` xml
 <EntityType Name="Customer">
    <Documentation>
      <Summary>Summary here.</Summary>
      <LongDescription>Long description here.</LongDescription>
    </Documentation>
    <Key>
      <PropertyRef Name="CustomerId" />
    </Key>
    <Property Type="Int32" Name="CustomerId" Nullable="false" />
    <Property Type="String" Name="Name" Nullable="false" />
 </EntityType>
```
 

 

## <a name="end-element-csdl"></a><span data-ttu-id="9a003-322">End 元素 (CSDL)</span><span class="sxs-lookup"><span data-stu-id="9a003-322">End Element (CSDL)</span></span>

<span data-ttu-id="9a003-323">**最终**概念架构定义语言 (CSDL) 中的元素可以是 Association 元素或 AssociationSet 元素的子级。</span><span class="sxs-lookup"><span data-stu-id="9a003-323">The **End** element in conceptual schema definition language (CSDL) can be a child of the Association element or the AssociationSet element.</span></span> <span data-ttu-id="9a003-324">每种情况下的角色**最终**元素是不同的适用的特性也不同。</span><span class="sxs-lookup"><span data-stu-id="9a003-324">In each case, the role of the **End** element is different and the applicable attributes are different.</span></span>

### <a name="end-element-as-a-child-of-the-association-element"></a><span data-ttu-id="9a003-325">End 元素作为 Association 元素的子元素</span><span class="sxs-lookup"><span data-stu-id="9a003-325">End Element as a Child of the Association Element</span></span>

<span data-ttu-id="9a003-326">**最终**元素 (作为子级**关联**元素) 标识关联的一端可以存在的实体类型实例数，关联的另一端的实体类型。</span><span class="sxs-lookup"><span data-stu-id="9a003-326">An **End** element (as a child of the **Association** element) identifies the entity type on one end of an association and the number of entity type instances that can exist at that end of an association.</span></span> <span data-ttu-id="9a003-327">关联端定义为关联的一部分；关联必须正好有两个关联端。</span><span class="sxs-lookup"><span data-stu-id="9a003-327">Association ends are defined as part of an association; an association must have exactly two association ends.</span></span> <span data-ttu-id="9a003-328">通过导航属性或外键（如果在实体类型上公开了外键）可以访问关联一端的实体类型实例。</span><span class="sxs-lookup"><span data-stu-id="9a003-328">Entity type instances at one end of an association can be accessed through navigation properties or foreign keys if they are exposed on an entity type.</span></span>  

<span data-ttu-id="9a003-329">**最终**元素可以具有下列子元素 （按所列顺序）：</span><span class="sxs-lookup"><span data-stu-id="9a003-329">An **End** element can have the following child elements (in the order listed):</span></span>

-   <span data-ttu-id="9a003-330">文档 （零个或一个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-330">Documentation (zero or one element)</span></span>
-   <span data-ttu-id="9a003-331">OnDelete （零个或一个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-331">OnDelete (zero or one element)</span></span>
-   <span data-ttu-id="9a003-332">批注元素 （零个或多个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-332">Annotation elements (zero or more elements)</span></span>

#### <a name="applicable-attributes"></a><span data-ttu-id="9a003-333">适用的特性</span><span class="sxs-lookup"><span data-stu-id="9a003-333">Applicable Attributes</span></span>

<span data-ttu-id="9a003-334">下表介绍可应用于的特性**最终**时的子元素**关联**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-334">The following table describes the attributes that can be applied to the **End** element when it is the child of an **Association** element.</span></span>

| <span data-ttu-id="9a003-335">特性名</span><span class="sxs-lookup"><span data-stu-id="9a003-335">Attribute Name</span></span>   | <span data-ttu-id="9a003-336">是否必需</span><span class="sxs-lookup"><span data-stu-id="9a003-336">Is Required</span></span> | <span data-ttu-id="9a003-337">“值”</span><span class="sxs-lookup"><span data-stu-id="9a003-337">Value</span></span>                                                                                                                                                                                                                                                                                                                                                                                                              |
|:-----------------|:------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9a003-338">**Type**</span><span class="sxs-lookup"><span data-stu-id="9a003-338">**Type**</span></span>         | <span data-ttu-id="9a003-339">是</span><span class="sxs-lookup"><span data-stu-id="9a003-339">Yes</span></span>         | <span data-ttu-id="9a003-340">关联一端的实体类型的名称。</span><span class="sxs-lookup"><span data-stu-id="9a003-340">The name of the entity type at one end of the association.</span></span>                                                                                                                                                                                                                                                                                                                                                         |
| <span data-ttu-id="9a003-341">**角色**</span><span class="sxs-lookup"><span data-stu-id="9a003-341">**Role**</span></span>         | <span data-ttu-id="9a003-342">否</span><span class="sxs-lookup"><span data-stu-id="9a003-342">No</span></span>          | <span data-ttu-id="9a003-343">关联端的名称。</span><span class="sxs-lookup"><span data-stu-id="9a003-343">A name for the association end.</span></span> <span data-ttu-id="9a003-344">如果不提供名称，将使用关联端的实体类型的名称。</span><span class="sxs-lookup"><span data-stu-id="9a003-344">If no name is provided, the name of the entity type on the association end will be used.</span></span>                                                                                                                                                                                                                                                                                           |
| <span data-ttu-id="9a003-345">**重数**</span><span class="sxs-lookup"><span data-stu-id="9a003-345">**Multiplicity**</span></span> | <span data-ttu-id="9a003-346">是</span><span class="sxs-lookup"><span data-stu-id="9a003-346">Yes</span></span>         | <span data-ttu-id="9a003-347">**1**， **0..1**，或**\*** 具体取决于实体类型实例的关联端处可以存在的数量。</span><span class="sxs-lookup"><span data-stu-id="9a003-347">**1**, **0..1**, or **\*** depending on the number of entity type instances that can be at the end of the association.</span></span> <br/> <span data-ttu-id="9a003-348">**1**指示在关联端存在的一个实体类型实例。</span><span class="sxs-lookup"><span data-stu-id="9a003-348">**1** indicates that exactly one entity type instance exists at the association end.</span></span> <br/> <span data-ttu-id="9a003-349">**0..1**表明在关联端存在零个或一个实体类型实例。</span><span class="sxs-lookup"><span data-stu-id="9a003-349">**0..1** indicates that zero or one entity type instances exist at the association end.</span></span> <br/> <span data-ttu-id="9a003-350">**\*** 指示在关联端存在零行、 一行或多个实体类型实例。</span><span class="sxs-lookup"><span data-stu-id="9a003-350">**\*** indicates that zero, one, or more entity type instances exist at the association end.</span></span> |

 

> [!NOTE]
> <span data-ttu-id="9a003-351">可以将任意数量的 （自定义 XML 特性） 的批注特性应用于**最终**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-351">Any number of annotation attributes (custom XML attributes) may be applied to the **End** element.</span></span> <span data-ttu-id="9a003-352">然而，自定义特性可能不属于为 CSDL 保留的任何 XML 命名空间。</span><span class="sxs-lookup"><span data-stu-id="9a003-352">However, custom attributes may not belong to any XML namespace that is reserved for CSDL.</span></span> <span data-ttu-id="9a003-353">任何两个自定义特性的完全限定名称都不能相同。</span><span class="sxs-lookup"><span data-stu-id="9a003-353">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

 

#### <a name="example"></a><span data-ttu-id="9a003-354">示例</span><span class="sxs-lookup"><span data-stu-id="9a003-354">Example</span></span>

<span data-ttu-id="9a003-355">下面的示例演示**关联**定义的元素**CustomerOrders**关联。</span><span class="sxs-lookup"><span data-stu-id="9a003-355">The following example shows an **Association** element that defines the **CustomerOrders** association.</span></span> <span data-ttu-id="9a003-356">**多重性**值为每个**最终**关联的指示，许多**订单**可以关联**客户**，但只有一个**客户**可以关联**顺序**。</span><span class="sxs-lookup"><span data-stu-id="9a003-356">The **Multiplicity** values for each **End** of the association indicate that many **Orders** can be associated with a **Customer**, but only one **Customer** can be associated with an **Order**.</span></span> <span data-ttu-id="9a003-357">此外， **OnDelete**元素指示所有**订单**与特定相关的**客户**和已加载到 ObjectContext 将如果已删除**客户**被删除。</span><span class="sxs-lookup"><span data-stu-id="9a003-357">Additionally, the **OnDelete** element indicates that all **Orders** that are related to a particular **Customer** and that have been loaded into the ObjectContext will be deleted if the **Customer** is deleted.</span></span>

``` xml
 <Association Name="CustomerOrders">
   <End Type="ExampleModel.Customer" Role="Customer" Multiplicity="1" />
   <End Type="ExampleModel.Order" Role="Order" Multiplicity="*">
         <OnDelete Action="Cascade" />
   </End>
 </Association>
```
 

### <a name="end-element-as-a-child-of-the-associationset-element"></a><span data-ttu-id="9a003-358">End 元素作为 AssociationSet 元素的子元素</span><span class="sxs-lookup"><span data-stu-id="9a003-358">End Element as a Child of the AssociationSet Element</span></span>

<span data-ttu-id="9a003-359">**最终**元素指定关联集的一端。</span><span class="sxs-lookup"><span data-stu-id="9a003-359">The **End** element specifies one end of an association set.</span></span> <span data-ttu-id="9a003-360">**AssociationSet**元素必须包含两个**最终**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-360">The **AssociationSet** element must contain two **End** elements.</span></span> <span data-ttu-id="9a003-361">中包含的信息**最终**元素用于映射到数据源设置的关联。</span><span class="sxs-lookup"><span data-stu-id="9a003-361">The information contained in an **End** element is used in mapping an association set to a data source.</span></span>

<span data-ttu-id="9a003-362">**最终**元素可以具有下列子元素 （按所列顺序）：</span><span class="sxs-lookup"><span data-stu-id="9a003-362">An **End** element can have the following child elements (in the order listed):</span></span>

-   <span data-ttu-id="9a003-363">文档 （零个或一个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-363">Documentation (zero or one element)</span></span>
-   <span data-ttu-id="9a003-364">批注元素 （零个或多个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-364">Annotation elements (zero or more elements)</span></span>

> [!NOTE]
> <span data-ttu-id="9a003-365">Annotation 元素必须出现在所有其他子元素之后。</span><span class="sxs-lookup"><span data-stu-id="9a003-365">Annotation elements must appear after all other child elements.</span></span> <span data-ttu-id="9a003-366">批注元素只能在 CSDL v2 和更高版本。</span><span class="sxs-lookup"><span data-stu-id="9a003-366">Annotation elements are only allowed in CSDL v2 and later.</span></span>

 

#### <a name="applicable-attributes"></a><span data-ttu-id="9a003-367">适用的特性</span><span class="sxs-lookup"><span data-stu-id="9a003-367">Applicable Attributes</span></span>

<span data-ttu-id="9a003-368">下表介绍可应用于的特性**最终**时的子元素**AssociationSet**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-368">The following table describes the attributes that can be applied to the **End** element when it is the child of an **AssociationSet** element.</span></span>

| <span data-ttu-id="9a003-369">特性名</span><span class="sxs-lookup"><span data-stu-id="9a003-369">Attribute Name</span></span> | <span data-ttu-id="9a003-370">是否必需</span><span class="sxs-lookup"><span data-stu-id="9a003-370">Is Required</span></span> | <span data-ttu-id="9a003-371">“值”</span><span class="sxs-lookup"><span data-stu-id="9a003-371">Value</span></span>                                                                                                                                                                                                                 |
|:---------------|:------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9a003-372">**实体集**</span><span class="sxs-lookup"><span data-stu-id="9a003-372">**EntitySet**</span></span>  | <span data-ttu-id="9a003-373">是</span><span class="sxs-lookup"><span data-stu-id="9a003-373">Yes</span></span>         | <span data-ttu-id="9a003-374">名称**EntitySet**元素，用于定义父级的一端**AssociationSet**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-374">The name of the **EntitySet** element that defines one end of the parent **AssociationSet** element.</span></span> <span data-ttu-id="9a003-375">**EntitySet**必须为父级的同一个实体容器定义元素**AssociationSet**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-375">The **EntitySet** element must be defined in the same entity container as the parent **AssociationSet** element.</span></span> |
| <span data-ttu-id="9a003-376">**角色**</span><span class="sxs-lookup"><span data-stu-id="9a003-376">**Role**</span></span>       | <span data-ttu-id="9a003-377">否</span><span class="sxs-lookup"><span data-stu-id="9a003-377">No</span></span>          | <span data-ttu-id="9a003-378">关联集端的名称。</span><span class="sxs-lookup"><span data-stu-id="9a003-378">The name of the association set end.</span></span> <span data-ttu-id="9a003-379">如果**角色**未使用属性、 关联集端的名称将为实体集的名称。</span><span class="sxs-lookup"><span data-stu-id="9a003-379">If the **Role** attribute is not used, the name of the association set end will be the name of the entity set.</span></span>                                                                   |

 

> [!NOTE]
> <span data-ttu-id="9a003-380">可以将任意数量的 （自定义 XML 特性） 的批注特性应用于**最终**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-380">Any number of annotation attributes (custom XML attributes) may be applied to the **End** element.</span></span> <span data-ttu-id="9a003-381">然而，自定义特性可能不属于为 CSDL 保留的任何 XML 命名空间。</span><span class="sxs-lookup"><span data-stu-id="9a003-381">However, custom attributes may not belong to any XML namespace that is reserved for CSDL.</span></span> <span data-ttu-id="9a003-382">任何两个自定义特性的完全限定名称都不能相同。</span><span class="sxs-lookup"><span data-stu-id="9a003-382">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

 

#### <a name="example"></a><span data-ttu-id="9a003-383">示例</span><span class="sxs-lookup"><span data-stu-id="9a003-383">Example</span></span>

<span data-ttu-id="9a003-384">下面的示例演示**EntityContainer**元素具有两个**AssociationSet**元素，每个都有两个**最终**元素：</span><span class="sxs-lookup"><span data-stu-id="9a003-384">The following example shows an **EntityContainer** element with two **AssociationSet** elements, each with two **End** elements:</span></span>

``` xml
 <EntityContainer Name="BooksContainer" >
   <EntitySet Name="Books" EntityType="BooksModel.Book" />
   <EntitySet Name="Publishers" EntityType="BooksModel.Publisher" />
   <EntitySet Name="Authors" EntityType="BooksModel.Author" />
   <AssociationSet Name="PublishedBy" Association="BooksModel.PublishedBy">
     <End Role="Book" EntitySet="Books" />
     <End Role="Publisher" EntitySet="Publishers" />
   </AssociationSet>
   <AssociationSet Name="WrittenBy" Association="BooksModel.WrittenBy">
     <End Role="Book" EntitySet="Books" />
     <End Role="Author" EntitySet="Authors" />
   </AssociationSet>
 </EntityContainer>
```
 

 

## <a name="entitycontainer-element-csdl"></a><span data-ttu-id="9a003-385">EntityContainer 元素 (CSDL)</span><span class="sxs-lookup"><span data-stu-id="9a003-385">EntityContainer Element (CSDL)</span></span>

<span data-ttu-id="9a003-386">**EntityContainer**概念架构定义语言 (CSDL) 中的元素是实体集、 关联集和函数导入的逻辑容器。</span><span class="sxs-lookup"><span data-stu-id="9a003-386">The **EntityContainer** element in conceptual schema definition language (CSDL) is a logical container for entity sets, association sets, and function imports.</span></span> <span data-ttu-id="9a003-387">概念模型实体容器映射到存储模型实体容器通过 EntityContainerMapping 元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-387">A conceptual model entity container maps to a storage model entity container through the EntityContainerMapping element.</span></span> <span data-ttu-id="9a003-388">存储模型实体容器描述数据库的结构：实体集描述表、关联集描述外键约束、函数导入描述数据库中的存储过程。</span><span class="sxs-lookup"><span data-stu-id="9a003-388">A storage model entity container describes the structure of the database: entity sets describe tables, association sets describe foreign key constraints, and function imports describe stored procedures in a database.</span></span>

<span data-ttu-id="9a003-389">**EntityContainer**元素可以具有零个或一个文档元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-389">An **EntityContainer** element can have zero or one Documentation elements.</span></span> <span data-ttu-id="9a003-390">如果**文档**元素存在，则它必须位于所有之前**EntitySet**， **AssociationSet**，以及**FunctionImport**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-390">If a **Documentation** element is present, it must precede all **EntitySet**, **AssociationSet**, and **FunctionImport** elements.</span></span>

<span data-ttu-id="9a003-391">**EntityContainer**元素可以具有零个或多个下列子元素 （按所列顺序）：</span><span class="sxs-lookup"><span data-stu-id="9a003-391">An **EntityContainer** element can have zero or more of the following child elements (in the order listed):</span></span>

-   <span data-ttu-id="9a003-392">EntitySet</span><span class="sxs-lookup"><span data-stu-id="9a003-392">EntitySet</span></span>
-   <span data-ttu-id="9a003-393">AssociationSet</span><span class="sxs-lookup"><span data-stu-id="9a003-393">AssociationSet</span></span>
-   <span data-ttu-id="9a003-394">FunctionImport</span><span class="sxs-lookup"><span data-stu-id="9a003-394">FunctionImport</span></span>
-   <span data-ttu-id="9a003-395">批注元素</span><span class="sxs-lookup"><span data-stu-id="9a003-395">Annotation elements</span></span>

<span data-ttu-id="9a003-396">您可以扩展**EntityContainer**元素包含的另一个内容**EntityContainer**中相同的命名空间。</span><span class="sxs-lookup"><span data-stu-id="9a003-396">You can extend an **EntityContainer** element to include the contents of another **EntityContainer** that is within the same namespace.</span></span> <span data-ttu-id="9a003-397">包含的另一个内容**EntityContainer**，在引用**EntityContainer**元素中，设置的值**扩展**的名称的属性**EntityContainer**想要包括的元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-397">To include the contents of another **EntityContainer**, in the referencing **EntityContainer** element, set the value of the **Extends** attribute to the name of the **EntityContainer** element that you want to include.</span></span> <span data-ttu-id="9a003-398">所包含的所有子元素**EntityContainer**元素将被视为引用的子元素**EntityContainer**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-398">All child elements of the included **EntityContainer** element will be treated as child elements of the referencing **EntityContainer** element.</span></span>

### <a name="applicable-attributes"></a><span data-ttu-id="9a003-399">适用的特性</span><span class="sxs-lookup"><span data-stu-id="9a003-399">Applicable Attributes</span></span>

<span data-ttu-id="9a003-400">下表描述了可应用于的特性**Using**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-400">The table below describes the attributes that can be applied to the **Using** element.</span></span>

| <span data-ttu-id="9a003-401">特性名</span><span class="sxs-lookup"><span data-stu-id="9a003-401">Attribute Name</span></span> | <span data-ttu-id="9a003-402">是否必需</span><span class="sxs-lookup"><span data-stu-id="9a003-402">Is Required</span></span> | <span data-ttu-id="9a003-403">“值”</span><span class="sxs-lookup"><span data-stu-id="9a003-403">Value</span></span>                                                           |
|:---------------|:------------|:----------------------------------------------------------------|
| <span data-ttu-id="9a003-404">**名称**</span><span class="sxs-lookup"><span data-stu-id="9a003-404">**Name**</span></span>       | <span data-ttu-id="9a003-405">是</span><span class="sxs-lookup"><span data-stu-id="9a003-405">Yes</span></span>         | <span data-ttu-id="9a003-406">实体容器的名称。</span><span class="sxs-lookup"><span data-stu-id="9a003-406">The name of the entity container.</span></span>                               |
| <span data-ttu-id="9a003-407">**扩展**</span><span class="sxs-lookup"><span data-stu-id="9a003-407">**Extends**</span></span>    | <span data-ttu-id="9a003-408">否</span><span class="sxs-lookup"><span data-stu-id="9a003-408">No</span></span>          | <span data-ttu-id="9a003-409">同一命名空间中另一实体容器的名称。</span><span class="sxs-lookup"><span data-stu-id="9a003-409">The name of another entity container within the same namespace.</span></span> |

 

> [!NOTE]
> <span data-ttu-id="9a003-410">可以将任意数量的 （自定义 XML 特性） 的批注特性应用于**EntityContainer**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-410">Any number of annotation attributes (custom XML attributes) may be applied to the **EntityContainer** element.</span></span> <span data-ttu-id="9a003-411">然而，自定义特性可能不属于为 CSDL 保留的任何 XML 命名空间。</span><span class="sxs-lookup"><span data-stu-id="9a003-411">However, custom attributes may not belong to any XML namespace that is reserved for CSDL.</span></span> <span data-ttu-id="9a003-412">任何两个自定义特性的完全限定名称都不能相同。</span><span class="sxs-lookup"><span data-stu-id="9a003-412">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

 

### <a name="example"></a><span data-ttu-id="9a003-413">示例</span><span class="sxs-lookup"><span data-stu-id="9a003-413">Example</span></span>

<span data-ttu-id="9a003-414">下面的示例演示**EntityContainer**定义三个实体集和两个关联集的元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-414">The following example shows an **EntityContainer** element that defines three entity sets and two association sets.</span></span>

``` xml
 <EntityContainer Name="BooksContainer" >
   <EntitySet Name="Books" EntityType="BooksModel.Book" />
   <EntitySet Name="Publishers" EntityType="BooksModel.Publisher" />
   <EntitySet Name="Authors" EntityType="BooksModel.Author" />
   <AssociationSet Name="PublishedBy" Association="BooksModel.PublishedBy">
     <End Role="Book" EntitySet="Books" />
     <End Role="Publisher" EntitySet="Publishers" />
   </AssociationSet>
   <AssociationSet Name="WrittenBy" Association="BooksModel.WrittenBy">
     <End Role="Book" EntitySet="Books" />
     <End Role="Author" EntitySet="Authors" />
   </AssociationSet>
 </EntityContainer>
```
 

 

## <a name="entityset-element-csdl"></a><span data-ttu-id="9a003-415">EntitySet 元素 (CSDL)</span><span class="sxs-lookup"><span data-stu-id="9a003-415">EntitySet Element (CSDL)</span></span>

<span data-ttu-id="9a003-416">**EntitySet**以概念架构定义语言元素是实体类型的实例和派生自该实体类型的任何类型的实例的逻辑容器。</span><span class="sxs-lookup"><span data-stu-id="9a003-416">The **EntitySet** element in conceptual schema definition language is a logical container for instances of an entity type and instances of any type that is derived from that entity type.</span></span> <span data-ttu-id="9a003-417">实体类型与实体集之间的关系类似于关系数据库中行与表之间的关系。</span><span class="sxs-lookup"><span data-stu-id="9a003-417">The relationship between an entity type and an entity set is analogous to the relationship between a row and a table in a relational database.</span></span> <span data-ttu-id="9a003-418">实体类型与行类似，它定义一组相关数据；而实体集与表类似，它包含该定义的实例。</span><span class="sxs-lookup"><span data-stu-id="9a003-418">Like a row, an entity type defines a set of related data, and, like a table, an entity set contains instances of that definition.</span></span> <span data-ttu-id="9a003-419">实体集为对实体类型实例分组提供了一个构造，以便能够将它们映射到数据源中的相关数据结构。</span><span class="sxs-lookup"><span data-stu-id="9a003-419">An entity set provides a construct for grouping entity type instances so that they can be mapped to related data structures in a data source.</span></span>  

<span data-ttu-id="9a003-420">可以为特定实体类型定义多个实体集。</span><span class="sxs-lookup"><span data-stu-id="9a003-420">More than one entity set for a particular entity type may be defined.</span></span>

> [!NOTE]
> <span data-ttu-id="9a003-421">在 EF 设计器不支持包含每种类型的多个实体集的概念模型。</span><span class="sxs-lookup"><span data-stu-id="9a003-421">The EF Designer does not support conceptual models that contain multiple entity sets per type.</span></span>

 

<span data-ttu-id="9a003-422">**EntitySet**元素可以具有下列子元素 （按所列顺序）：</span><span class="sxs-lookup"><span data-stu-id="9a003-422">The **EntitySet** element can have the following child elements (in the order listed):</span></span>

-   <span data-ttu-id="9a003-423">Documentation 元素 （允许零个或一个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-423">Documentation Element (zero or one elements allowed)</span></span>
-   <span data-ttu-id="9a003-424">批注元素 （允许零个或多个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-424">Annotation elements (zero or more elements allowed)</span></span>

### <a name="applicable-attributes"></a><span data-ttu-id="9a003-425">适用的特性</span><span class="sxs-lookup"><span data-stu-id="9a003-425">Applicable Attributes</span></span>

<span data-ttu-id="9a003-426">下表描述了可应用于的特性**EntitySet**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-426">The table below describes the attributes that can be applied to the **EntitySet** element.</span></span>

| <span data-ttu-id="9a003-427">特性名</span><span class="sxs-lookup"><span data-stu-id="9a003-427">Attribute Name</span></span> | <span data-ttu-id="9a003-428">是否必需</span><span class="sxs-lookup"><span data-stu-id="9a003-428">Is Required</span></span> | <span data-ttu-id="9a003-429">“值”</span><span class="sxs-lookup"><span data-stu-id="9a003-429">Value</span></span>                                                                                    |
|:---------------|:------------|:-----------------------------------------------------------------------------------------|
| <span data-ttu-id="9a003-430">**名称**</span><span class="sxs-lookup"><span data-stu-id="9a003-430">**Name**</span></span>       | <span data-ttu-id="9a003-431">是</span><span class="sxs-lookup"><span data-stu-id="9a003-431">Yes</span></span>         | <span data-ttu-id="9a003-432">实体集的名称。</span><span class="sxs-lookup"><span data-stu-id="9a003-432">The name of the entity set.</span></span>                                                              |
| <span data-ttu-id="9a003-433">**EntityType**</span><span class="sxs-lookup"><span data-stu-id="9a003-433">**EntityType**</span></span> | <span data-ttu-id="9a003-434">是</span><span class="sxs-lookup"><span data-stu-id="9a003-434">Yes</span></span>         | <span data-ttu-id="9a003-435">实体集包含其实例的实体类型的完全限定名称。</span><span class="sxs-lookup"><span data-stu-id="9a003-435">The fully-qualified name of the entity type for which the entity set contains instances.</span></span> |

 

> [!NOTE]
> <span data-ttu-id="9a003-436">可以将任意数量的 （自定义 XML 特性） 的批注特性应用于**EntitySet**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-436">Any number of annotation attributes (custom XML attributes) may be applied to the **EntitySet** element.</span></span> <span data-ttu-id="9a003-437">然而，自定义特性可能不属于为 CSDL 保留的任何 XML 命名空间。</span><span class="sxs-lookup"><span data-stu-id="9a003-437">However, custom attributes may not belong to any XML namespace that is reserved for CSDL.</span></span> <span data-ttu-id="9a003-438">任何两个自定义特性的完全限定名称都不能相同。</span><span class="sxs-lookup"><span data-stu-id="9a003-438">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

 

### <a name="example"></a><span data-ttu-id="9a003-439">示例</span><span class="sxs-lookup"><span data-stu-id="9a003-439">Example</span></span>

<span data-ttu-id="9a003-440">下面的示例演示**EntityContainer**具有三个元素**EntitySet**元素：</span><span class="sxs-lookup"><span data-stu-id="9a003-440">The following example shows an **EntityContainer** element with three **EntitySet** elements:</span></span>

``` xml
 <EntityContainer Name="BooksContainer" >
   <EntitySet Name="Books" EntityType="BooksModel.Book" />
   <EntitySet Name="Publishers" EntityType="BooksModel.Publisher" />
   <EntitySet Name="Authors" EntityType="BooksModel.Author" />
   <AssociationSet Name="PublishedBy" Association="BooksModel.PublishedBy">
     <End Role="Book" EntitySet="Books" />
     <End Role="Publisher" EntitySet="Publishers" />
   </AssociationSet>
   <AssociationSet Name="WrittenBy" Association="BooksModel.WrittenBy">
     <End Role="Book" EntitySet="Books" />
     <End Role="Author" EntitySet="Authors" />
   </AssociationSet>
 </EntityContainer>
```
 

<span data-ttu-id="9a003-441">每个类型可以定义多个实体集 (MEST)。</span><span class="sxs-lookup"><span data-stu-id="9a003-441">It is possible to define multiple entity sets per type (MEST).</span></span> <span data-ttu-id="9a003-442">下面的示例定义了具有两个实体集的一个实体容器**通讯簿**实体类型：</span><span class="sxs-lookup"><span data-stu-id="9a003-442">The following example defines an entity container with two entity sets for the **Book** entity type:</span></span>

``` xml
 <EntityContainer Name="BooksContainer" >
   <EntitySet Name="Books" EntityType="BooksModel.Book" />
   <EntitySet Name="FictionBooks" EntityType="BooksModel.Book" />
   <EntitySet Name="Publishers" EntityType="BooksModel.Publisher" />
   <EntitySet Name="Authors" EntityType="BooksModel.Author" />
   <AssociationSet Name="PublishedBy" Association="BooksModel.PublishedBy">
     <End Role="Book" EntitySet="Books" />
     <End Role="Publisher" EntitySet="Publishers" />
   </AssociationSet>
   <AssociationSet Name="BookAuthor" Association="BooksModel.BookAuthor">
     <End Role="Book" EntitySet="Books" />
     <End Role="Author" EntitySet="Authors" />
   </AssociationSet>
 </EntityContainer>
```
 

 

## <a name="entitytype-element-csdl"></a><span data-ttu-id="9a003-443">EntityType 元素 (CSDL)</span><span class="sxs-lookup"><span data-stu-id="9a003-443">EntityType Element (CSDL)</span></span>

<span data-ttu-id="9a003-444">**EntityType**元素表示顶级概念，如客户或订单，概念模型中的结构。</span><span class="sxs-lookup"><span data-stu-id="9a003-444">The **EntityType** element represents the structure of a top-level concept, such as a customer or order, in a conceptual model.</span></span> <span data-ttu-id="9a003-445">实体类型是应用程序中实体类型实例的模板。</span><span class="sxs-lookup"><span data-stu-id="9a003-445">An entity type is a template for instances of entity types in an application.</span></span> <span data-ttu-id="9a003-446">每个模板都包含以下信息：</span><span class="sxs-lookup"><span data-stu-id="9a003-446">Each template contains the following information:</span></span>

-   <span data-ttu-id="9a003-447">唯一名称。</span><span class="sxs-lookup"><span data-stu-id="9a003-447">A unique name.</span></span> <span data-ttu-id="9a003-448">（必选。）</span><span class="sxs-lookup"><span data-stu-id="9a003-448">(Required.)</span></span>
-   <span data-ttu-id="9a003-449">由一个或多个属性定义的实体键。</span><span class="sxs-lookup"><span data-stu-id="9a003-449">An entity key that is defined by one or more properties.</span></span> <span data-ttu-id="9a003-450">（必选。）</span><span class="sxs-lookup"><span data-stu-id="9a003-450">(Required.)</span></span>
-   <span data-ttu-id="9a003-451">用于包含数据的属性。</span><span class="sxs-lookup"><span data-stu-id="9a003-451">Properties for containing data.</span></span> <span data-ttu-id="9a003-452">（可选）。</span><span class="sxs-lookup"><span data-stu-id="9a003-452">(Optional.)</span></span>
-   <span data-ttu-id="9a003-453">导航属性，用于从关联的一端导航至另一端。</span><span class="sxs-lookup"><span data-stu-id="9a003-453">Navigation properties that allow for navigation from one end of an association to the other end.</span></span> <span data-ttu-id="9a003-454">（可选）。</span><span class="sxs-lookup"><span data-stu-id="9a003-454">(Optional.)</span></span>

<span data-ttu-id="9a003-455">在应用程序中，实体类型的实例表示一个特定对象（例如特定客户或订单）。</span><span class="sxs-lookup"><span data-stu-id="9a003-455">In an application, an instance of an entity type represents a specific object (such as a specific customer or order).</span></span> <span data-ttu-id="9a003-456">实体类型的每个实例在实体集中都必须具有唯一的实体键。</span><span class="sxs-lookup"><span data-stu-id="9a003-456">Each instance of an entity type must have a unique entity key within an entity set.</span></span>

<span data-ttu-id="9a003-457">只有两个实体类型实例的类型相同且其实体键的值也相同时，才认为它们是相等的。</span><span class="sxs-lookup"><span data-stu-id="9a003-457">Two entity type instances are considered equal only if they are of the same type and the values of their entity keys are the same.</span></span>

<span data-ttu-id="9a003-458">**EntityType**元素可以具有下列子元素 （按所列顺序）：</span><span class="sxs-lookup"><span data-stu-id="9a003-458">An **EntityType** element can have the following child elements (in the order listed):</span></span>

-   <span data-ttu-id="9a003-459">文档 （零个或一个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-459">Documentation (zero or one element)</span></span>
-   <span data-ttu-id="9a003-460">密钥 （零个或一个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-460">Key (zero or one element)</span></span>
-   <span data-ttu-id="9a003-461">属性 （零个或多个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-461">Property (zero or more elements)</span></span>
-   <span data-ttu-id="9a003-462">NavigationProperty （零个或多个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-462">NavigationProperty (zero or more elements)</span></span>
-   <span data-ttu-id="9a003-463">批注元素 （零个或多个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-463">Annotation elements (zero or more elements)</span></span>

### <a name="applicable-attributes"></a><span data-ttu-id="9a003-464">适用的特性</span><span class="sxs-lookup"><span data-stu-id="9a003-464">Applicable Attributes</span></span>

<span data-ttu-id="9a003-465">下表描述了可应用于的特性**EntityType**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-465">The table below describes the attributes that can be applied to the **EntityType** element.</span></span>

| <span data-ttu-id="9a003-466">特性名</span><span class="sxs-lookup"><span data-stu-id="9a003-466">Attribute Name</span></span>                                                                                                                                  | <span data-ttu-id="9a003-467">是否必需</span><span class="sxs-lookup"><span data-stu-id="9a003-467">Is Required</span></span> | <span data-ttu-id="9a003-468">“值”</span><span class="sxs-lookup"><span data-stu-id="9a003-468">Value</span></span>                                                                                            |
|:------------------------------------------------------------------------------------------------------------------------------------------------|:------------|:-------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9a003-469">**名称**</span><span class="sxs-lookup"><span data-stu-id="9a003-469">**Name**</span></span>                                                                                                                                        | <span data-ttu-id="9a003-470">是</span><span class="sxs-lookup"><span data-stu-id="9a003-470">Yes</span></span>         | <span data-ttu-id="9a003-471">实体类型的名称。</span><span class="sxs-lookup"><span data-stu-id="9a003-471">The name of the entity type.</span></span>                                                                     |
| <span data-ttu-id="9a003-472">**BaseType**</span><span class="sxs-lookup"><span data-stu-id="9a003-472">**BaseType**</span></span>                                                                                                                                    | <span data-ttu-id="9a003-473">否</span><span class="sxs-lookup"><span data-stu-id="9a003-473">No</span></span>          | <span data-ttu-id="9a003-474">实体类型的名称，该实体类型是所定义的另一个实体类型的基类型。</span><span class="sxs-lookup"><span data-stu-id="9a003-474">The name of another entity type that is the base type of the entity type that is being defined.</span></span>  |
| <span data-ttu-id="9a003-475">**抽象**</span><span class="sxs-lookup"><span data-stu-id="9a003-475">**Abstract**</span></span>                                                                                                                                    | <span data-ttu-id="9a003-476">否</span><span class="sxs-lookup"><span data-stu-id="9a003-476">No</span></span>          | <span data-ttu-id="9a003-477">**True**或**False**，取决于实体类型是否为抽象类型。</span><span class="sxs-lookup"><span data-stu-id="9a003-477">**True** or **False**, depending on whether the entity type is an abstract type.</span></span>                 |
| <span data-ttu-id="9a003-478">**OpenType**</span><span class="sxs-lookup"><span data-stu-id="9a003-478">**OpenType**</span></span>                                                                                                                                    | <span data-ttu-id="9a003-479">否</span><span class="sxs-lookup"><span data-stu-id="9a003-479">No</span></span>          | <span data-ttu-id="9a003-480">**True**或**False**具体取决于实体类型是否为开放实体类型。</span><span class="sxs-lookup"><span data-stu-id="9a003-480">**True** or **False** depending on whether the entity type is an open entity type.</span></span> <br/> [!NOTE] |
| <span data-ttu-id="9a003-481">> **OpenType**属性特性仅适用于与 ADO.NET Data Services 一起使用的概念模型中定义的实体类型。</span><span class="sxs-lookup"><span data-stu-id="9a003-481">> The **OpenType** attribute is only applicable to entity types that are defined in conceptual models that are used with ADO.NET Data Services.</span></span> |             |                                                                                                  |

 

> [!NOTE]
> <span data-ttu-id="9a003-482">可以将任意数量的 （自定义 XML 特性） 的批注特性应用于**EntityType**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-482">Any number of annotation attributes (custom XML attributes) may be applied to the **EntityType** element.</span></span> <span data-ttu-id="9a003-483">然而，自定义特性可能不属于为 CSDL 保留的任何 XML 命名空间。</span><span class="sxs-lookup"><span data-stu-id="9a003-483">However, custom attributes may not belong to any XML namespace that is reserved for CSDL.</span></span> <span data-ttu-id="9a003-484">任何两个自定义特性的完全限定名称都不能相同。</span><span class="sxs-lookup"><span data-stu-id="9a003-484">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

 

### <a name="example"></a><span data-ttu-id="9a003-485">示例</span><span class="sxs-lookup"><span data-stu-id="9a003-485">Example</span></span>

<span data-ttu-id="9a003-486">下面的示例演示**EntityType**具有三个元素**属性**元素和两个**NavigationProperty**元素：</span><span class="sxs-lookup"><span data-stu-id="9a003-486">The following example shows an **EntityType** element with three **Property** elements and two **NavigationProperty** elements:</span></span>

``` xml
 <EntityType Name="Book">
   <Key>
     <PropertyRef Name="ISBN" />
   </Key>
   <Property Type="String" Name="ISBN" Nullable="false" />
   <Property Type="String" Name="Title" Nullable="false" />
   <Property Type="Decimal" Name="Revision" Nullable="false" Precision="29" Scale="29" />
   <NavigationProperty Name="Publisher" Relationship="BooksModel.PublishedBy"
                       FromRole="Book" ToRole="Publisher" />
   <NavigationProperty Name="Authors" Relationship="BooksModel.WrittenBy"
                       FromRole="Book" ToRole="Author" />
 </EntityType>
```
 

 

## <a name="enumtype-element-csdl"></a><span data-ttu-id="9a003-487">EnumType 元素 (CSDL)</span><span class="sxs-lookup"><span data-stu-id="9a003-487">EnumType Element (CSDL)</span></span>

<span data-ttu-id="9a003-488">**EnumType**元素表示一个枚举的类型。</span><span class="sxs-lookup"><span data-stu-id="9a003-488">The **EnumType** element represents an enumerated type.</span></span>

<span data-ttu-id="9a003-489">**EnumType**元素可以具有下列子元素 （按所列顺序）：</span><span class="sxs-lookup"><span data-stu-id="9a003-489">An **EnumType** element can have the following child elements (in the order listed):</span></span>

-   <span data-ttu-id="9a003-490">文档 （零个或一个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-490">Documentation (zero or one element)</span></span>
-   <span data-ttu-id="9a003-491">成员 （零个或多个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-491">Member (zero or more elements)</span></span>
-   <span data-ttu-id="9a003-492">批注元素 （零个或多个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-492">Annotation elements (zero or more elements)</span></span>

### <a name="applicable-attributes"></a><span data-ttu-id="9a003-493">适用的特性</span><span class="sxs-lookup"><span data-stu-id="9a003-493">Applicable Attributes</span></span>

<span data-ttu-id="9a003-494">下表描述了可应用于的特性**EnumType**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-494">The table below describes the attributes that can be applied to the **EnumType** element.</span></span>

| <span data-ttu-id="9a003-495">特性名</span><span class="sxs-lookup"><span data-stu-id="9a003-495">Attribute Name</span></span>     | <span data-ttu-id="9a003-496">是否必需</span><span class="sxs-lookup"><span data-stu-id="9a003-496">Is Required</span></span> | <span data-ttu-id="9a003-497">“值”</span><span class="sxs-lookup"><span data-stu-id="9a003-497">Value</span></span>                                                                                                                                                                                         |
|:-------------------|:------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9a003-498">**名称**</span><span class="sxs-lookup"><span data-stu-id="9a003-498">**Name**</span></span>           | <span data-ttu-id="9a003-499">是</span><span class="sxs-lookup"><span data-stu-id="9a003-499">Yes</span></span>         | <span data-ttu-id="9a003-500">实体类型的名称。</span><span class="sxs-lookup"><span data-stu-id="9a003-500">The name of the entity type.</span></span>                                                                                                                                                                  |
| <span data-ttu-id="9a003-501">**IsFlags**</span><span class="sxs-lookup"><span data-stu-id="9a003-501">**IsFlags**</span></span>        | <span data-ttu-id="9a003-502">否</span><span class="sxs-lookup"><span data-stu-id="9a003-502">No</span></span>          | <span data-ttu-id="9a003-503">**True**或**False**，取决于是否枚举类型可以用作一组标志。</span><span class="sxs-lookup"><span data-stu-id="9a003-503">**True** or **False**, depending on whether the enum type can be used as a set of flags.</span></span> <span data-ttu-id="9a003-504">默认值是**False**。</span><span class="sxs-lookup"><span data-stu-id="9a003-504">The default value is **False.**.</span></span>                                                                     |
| <span data-ttu-id="9a003-505">**UnderlyingType**</span><span class="sxs-lookup"><span data-stu-id="9a003-505">**UnderlyingType**</span></span> | <span data-ttu-id="9a003-506">否</span><span class="sxs-lookup"><span data-stu-id="9a003-506">No</span></span>          | <span data-ttu-id="9a003-507">**Edm.Byte**， **Edm.Int16**， **Edm.Int32**， **Edm.Int64**或**Edm.SByte**定义类型的值的范围。</span><span class="sxs-lookup"><span data-stu-id="9a003-507">**Edm.Byte**, **Edm.Int16**, **Edm.Int32**, **Edm.Int64** or **Edm.SByte** defining the range of values of the type.</span></span>   <span data-ttu-id="9a003-508">默认基础枚举元素的类型是**Edm.Int32**。</span><span class="sxs-lookup"><span data-stu-id="9a003-508">The default underlying type of enumeration elements is **Edm.Int32.**.</span></span> |

 

> [!NOTE]
> <span data-ttu-id="9a003-509">可以将任意数量的 （自定义 XML 特性） 的批注特性应用于**EnumType**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-509">Any number of annotation attributes (custom XML attributes) may be applied to the **EnumType** element.</span></span> <span data-ttu-id="9a003-510">然而，自定义特性可能不属于为 CSDL 保留的任何 XML 命名空间。</span><span class="sxs-lookup"><span data-stu-id="9a003-510">However, custom attributes may not belong to any XML namespace that is reserved for CSDL.</span></span> <span data-ttu-id="9a003-511">任何两个自定义特性的完全限定名称都不能相同。</span><span class="sxs-lookup"><span data-stu-id="9a003-511">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

 

### <a name="example"></a><span data-ttu-id="9a003-512">示例</span><span class="sxs-lookup"><span data-stu-id="9a003-512">Example</span></span>

<span data-ttu-id="9a003-513">下面的示例演示**EnumType**具有三个元素**成员**元素：</span><span class="sxs-lookup"><span data-stu-id="9a003-513">The following example shows an **EnumType** element with three **Member** elements:</span></span>

``` xml
 <EnumType Name="Color" IsFlags=”false” UnderlyingTyp=”Edm.Byte”>
   <Member Name="Red" />
   <Member Name="Green" />
   <Member Name="Blue" />
 </EntityType>
```
 

 

## <a name="function-element-csdl"></a><span data-ttu-id="9a003-514">Function 元素 (CSDL)</span><span class="sxs-lookup"><span data-stu-id="9a003-514">Function Element (CSDL)</span></span>

<span data-ttu-id="9a003-515">**函数**概念架构定义语言 (CSDL) 中的元素用于定义或声明函数概念模型中的。</span><span class="sxs-lookup"><span data-stu-id="9a003-515">The **Function** element in conceptual schema definition language (CSDL) is used to define or declare functions in the conceptual model.</span></span> <span data-ttu-id="9a003-516">通过使用 DefiningExpression 元素定义一个函数。</span><span class="sxs-lookup"><span data-stu-id="9a003-516">A function is defined by using a DefiningExpression element.</span></span>  

<span data-ttu-id="9a003-517">一个**函数**元素可以具有下列子元素 （按所列顺序）：</span><span class="sxs-lookup"><span data-stu-id="9a003-517">A **Function** element can have the following child elements (in the order listed):</span></span>

-   <span data-ttu-id="9a003-518">文档 （零个或一个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-518">Documentation (zero or one element)</span></span>
-   <span data-ttu-id="9a003-519">参数 （零个或多个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-519">Parameter (zero or more elements)</span></span>
-   <span data-ttu-id="9a003-520">DefiningExpression （零个或一个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-520">DefiningExpression (zero or one element)</span></span>
-   <span data-ttu-id="9a003-521">ReturnType （函数） （零个或一个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-521">ReturnType (Function) (zero or one element)</span></span>
-   <span data-ttu-id="9a003-522">批注元素 （零个或多个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-522">Annotation elements (zero or more elements)</span></span>

<span data-ttu-id="9a003-523">返回类型的函数必须指定与**ReturnType** （函数） 元素或**ReturnType**属性 （见下文），但不可同时使用两者。</span><span class="sxs-lookup"><span data-stu-id="9a003-523">A return type for a function must be specified with either the **ReturnType** (Function) element or the **ReturnType** attribute (see below), but not both.</span></span> <span data-ttu-id="9a003-524">可能的返回类型为任何 EdmSimpleType、实体类型、复杂类型、行类型或引用类型（或这些类型之一的集合）。</span><span class="sxs-lookup"><span data-stu-id="9a003-524">The possible return types are any EdmSimpleType, entity type, complex type, row type, or ref type (or a collection of one of these types).</span></span>

### <a name="applicable-attributes"></a><span data-ttu-id="9a003-525">适用的特性</span><span class="sxs-lookup"><span data-stu-id="9a003-525">Applicable Attributes</span></span>

<span data-ttu-id="9a003-526">下表描述了可应用于的特性**函数**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-526">The table below describes the attributes that can be applied to the **Function** element.</span></span>

| <span data-ttu-id="9a003-527">特性名</span><span class="sxs-lookup"><span data-stu-id="9a003-527">Attribute Name</span></span> | <span data-ttu-id="9a003-528">是否必需</span><span class="sxs-lookup"><span data-stu-id="9a003-528">Is Required</span></span> | <span data-ttu-id="9a003-529">“值”</span><span class="sxs-lookup"><span data-stu-id="9a003-529">Value</span></span>                              |
|:---------------|:------------|:-----------------------------------|
| <span data-ttu-id="9a003-530">**名称**</span><span class="sxs-lookup"><span data-stu-id="9a003-530">**Name**</span></span>       | <span data-ttu-id="9a003-531">是</span><span class="sxs-lookup"><span data-stu-id="9a003-531">Yes</span></span>         | <span data-ttu-id="9a003-532">函数名。</span><span class="sxs-lookup"><span data-stu-id="9a003-532">The name of the function.</span></span>          |
| <span data-ttu-id="9a003-533">**ReturnType**</span><span class="sxs-lookup"><span data-stu-id="9a003-533">**ReturnType**</span></span> | <span data-ttu-id="9a003-534">否</span><span class="sxs-lookup"><span data-stu-id="9a003-534">No</span></span>          | <span data-ttu-id="9a003-535">函数返回的类型。</span><span class="sxs-lookup"><span data-stu-id="9a003-535">The type returned by the function.</span></span> |

 

> [!NOTE]
> <span data-ttu-id="9a003-536">可以将任意数量的 （自定义 XML 特性） 的批注特性应用于**函数**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-536">Any number of annotation attributes (custom XML attributes) may be applied to the **Function** element.</span></span> <span data-ttu-id="9a003-537">然而，自定义特性可能不属于为 CSDL 保留的任何 XML 命名空间。</span><span class="sxs-lookup"><span data-stu-id="9a003-537">However, custom attributes may not belong to any XML namespace that is reserved for CSDL.</span></span> <span data-ttu-id="9a003-538">任何两个自定义特性的完全限定名称都不能相同。</span><span class="sxs-lookup"><span data-stu-id="9a003-538">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

 

### <a name="example"></a><span data-ttu-id="9a003-539">示例</span><span class="sxs-lookup"><span data-stu-id="9a003-539">Example</span></span>

<span data-ttu-id="9a003-540">下面的示例使用**函数**元素来定义已聘用一名讲师返回年数的函数。</span><span class="sxs-lookup"><span data-stu-id="9a003-540">The following example uses a **Function** element to define a function that returns the number of years since an instructor was hired.</span></span>

``` xml
 <Function Name="YearsSince" ReturnType="Edm.Int32">
   <Parameter Name="date" Type="Edm.DateTime" />
   <DefiningExpression>
     Year(CurrentDateTime()) - Year(date)
   </DefiningExpression>
 </Function>
```
 

 

## <a name="functionimport-element-csdl"></a><span data-ttu-id="9a003-541">FunctionImport 元素 (CSDL)</span><span class="sxs-lookup"><span data-stu-id="9a003-541">FunctionImport Element (CSDL)</span></span>

<span data-ttu-id="9a003-542">**FunctionImport**概念架构定义语言 (CSDL) 中的元素表示一个函数，则数据源中定义，但通过概念模型的对象可用的。</span><span class="sxs-lookup"><span data-stu-id="9a003-542">The **FunctionImport** element in conceptual schema definition language (CSDL) represents a function that is defined in the data source but available to objects through the conceptual model.</span></span> <span data-ttu-id="9a003-543">例如，在存储模型中的函数元素可以用于表示数据库中的存储的过程。</span><span class="sxs-lookup"><span data-stu-id="9a003-543">For example, a Function element in the storage model can be used to represent a stored procedure in a database.</span></span> <span data-ttu-id="9a003-544">一个**FunctionImport**概念模型中的元素表示的实体框架应用程序中的相应函数，通过使用 FunctionImportMapping 元素映射到存储模型函数。</span><span class="sxs-lookup"><span data-stu-id="9a003-544">A **FunctionImport** element in the conceptual model represents the corresponding function in an Entity Framework application and is mapped to the storage model function by using the FunctionImportMapping element.</span></span> <span data-ttu-id="9a003-545">在应用程序中调用函数时，会在数据库中执行相应的存储过程。</span><span class="sxs-lookup"><span data-stu-id="9a003-545">When the function is called in the application, the corresponding stored procedure is executed in the database.</span></span>

<span data-ttu-id="9a003-546">**FunctionImport**元素可以具有下列子元素 （按所列顺序）：</span><span class="sxs-lookup"><span data-stu-id="9a003-546">The **FunctionImport** element can have the following child elements (in the order listed):</span></span>

-   <span data-ttu-id="9a003-547">文档 （允许零个或一个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-547">Documentation (zero or one elements allowed)</span></span>
-   <span data-ttu-id="9a003-548">参数 （允许零个或多个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-548">Parameter (zero or more elements allowed)</span></span>
-   <span data-ttu-id="9a003-549">批注元素 （允许零个或多个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-549">Annotation elements (zero or more elements allowed)</span></span>
-   <span data-ttu-id="9a003-550">ReturnType (FunctionImport) （允许零个或多个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-550">ReturnType (FunctionImport) (zero or more elements allowed)</span></span>

<span data-ttu-id="9a003-551">一个**参数**元素应为该函数接受每个参数定义。</span><span class="sxs-lookup"><span data-stu-id="9a003-551">One **Parameter** element should be defined for each parameter that the function accepts.</span></span>

<span data-ttu-id="9a003-552">返回类型的函数必须指定与**ReturnType** (FunctionImport) 元素或**ReturnType**属性 （见下文），但不可同时使用两者。</span><span class="sxs-lookup"><span data-stu-id="9a003-552">A return type for a function must be specified with either the **ReturnType** (FunctionImport) element or the **ReturnType** attribute (see below), but not both.</span></span> <span data-ttu-id="9a003-553">返回类型值必须为 EdmSimpleType、 EntityType 或 ComplexType 的集合。</span><span class="sxs-lookup"><span data-stu-id="9a003-553">The return type value must be a  collection of EdmSimpleType, EntityType, or ComplexType.</span></span>

### <a name="applicable-attributes"></a><span data-ttu-id="9a003-554">适用的特性</span><span class="sxs-lookup"><span data-stu-id="9a003-554">Applicable Attributes</span></span>

<span data-ttu-id="9a003-555">下表描述了可应用于的特性**FunctionImport**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-555">The table below describes the attributes that can be applied to the **FunctionImport** element.</span></span>

| <span data-ttu-id="9a003-556">特性名</span><span class="sxs-lookup"><span data-stu-id="9a003-556">Attribute Name</span></span>   | <span data-ttu-id="9a003-557">是否必需</span><span class="sxs-lookup"><span data-stu-id="9a003-557">Is Required</span></span> | <span data-ttu-id="9a003-558">“值”</span><span class="sxs-lookup"><span data-stu-id="9a003-558">Value</span></span>                                                                                                                                                                                                 |
|:-----------------|:------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9a003-559">**名称**</span><span class="sxs-lookup"><span data-stu-id="9a003-559">**Name**</span></span>         | <span data-ttu-id="9a003-560">是</span><span class="sxs-lookup"><span data-stu-id="9a003-560">Yes</span></span>         | <span data-ttu-id="9a003-561">导入的函数的名称。</span><span class="sxs-lookup"><span data-stu-id="9a003-561">The name of the imported function.</span></span>                                                                                                                                                                    |
| <span data-ttu-id="9a003-562">**ReturnType**</span><span class="sxs-lookup"><span data-stu-id="9a003-562">**ReturnType**</span></span>   | <span data-ttu-id="9a003-563">否</span><span class="sxs-lookup"><span data-stu-id="9a003-563">No</span></span>          | <span data-ttu-id="9a003-564">函数返回的类型。</span><span class="sxs-lookup"><span data-stu-id="9a003-564">The type that the function returns.</span></span> <span data-ttu-id="9a003-565">如果函数不返回值，不要使用此特性。</span><span class="sxs-lookup"><span data-stu-id="9a003-565">Do not use this attribute if the function does not return a value.</span></span> <span data-ttu-id="9a003-566">否则，值必须是 ComplexType、 EntityType 或 EDMSimpleType 的集合。</span><span class="sxs-lookup"><span data-stu-id="9a003-566">Otherwise, the value must be a collection of ComplexType, EntityType, or EDMSimpleType.</span></span>        |
| <span data-ttu-id="9a003-567">**实体集**</span><span class="sxs-lookup"><span data-stu-id="9a003-567">**EntitySet**</span></span>    | <span data-ttu-id="9a003-568">否</span><span class="sxs-lookup"><span data-stu-id="9a003-568">No</span></span>          | <span data-ttu-id="9a003-569">如果该函数返回的实体集合类型，值**EntitySet**必须将实体设置为该集合所属。</span><span class="sxs-lookup"><span data-stu-id="9a003-569">If the function returns a collection of entity types, the value of the **EntitySet** must be the entity set to which the collection belongs.</span></span> <span data-ttu-id="9a003-570">否则为**EntitySet**属性不能使用。</span><span class="sxs-lookup"><span data-stu-id="9a003-570">Otherwise, the **EntitySet** attribute must not be used.</span></span> |
| <span data-ttu-id="9a003-571">**IsComposable**</span><span class="sxs-lookup"><span data-stu-id="9a003-571">**IsComposable**</span></span> | <span data-ttu-id="9a003-572">否</span><span class="sxs-lookup"><span data-stu-id="9a003-572">No</span></span>          | <span data-ttu-id="9a003-573">如果值设置为 true，该函数是可组合 （表值函数） 并可以在 LINQ 查询中。</span><span class="sxs-lookup"><span data-stu-id="9a003-573">If the value is set to true, the function is composable (Table-valued Function) and can be used in a LINQ query.</span></span>  <span data-ttu-id="9a003-574">默认值为 false。</span><span class="sxs-lookup"><span data-stu-id="9a003-574">The default is **false**.</span></span>                                                           |

 

> [!NOTE]
> <span data-ttu-id="9a003-575">可以将任意数量的 （自定义 XML 特性） 的批注特性应用于**FunctionImport**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-575">Any number of annotation attributes (custom XML attributes) may be applied to the **FunctionImport** element.</span></span> <span data-ttu-id="9a003-576">然而，自定义特性可能不属于为 CSDL 保留的任何 XML 命名空间。</span><span class="sxs-lookup"><span data-stu-id="9a003-576">However, custom attributes may not belong to any XML namespace that is reserved for CSDL.</span></span> <span data-ttu-id="9a003-577">任何两个自定义特性的完全限定名称都不能相同。</span><span class="sxs-lookup"><span data-stu-id="9a003-577">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

 

### <a name="example"></a><span data-ttu-id="9a003-578">示例</span><span class="sxs-lookup"><span data-stu-id="9a003-578">Example</span></span>

<span data-ttu-id="9a003-579">下面的示例演示**FunctionImport**元素接受一个参数并返回实体类型的集合：</span><span class="sxs-lookup"><span data-stu-id="9a003-579">The following example shows a **FunctionImport** element that accepts one parameter and returns a collection of entity types:</span></span>

``` xml
 <FunctionImport Name="GetStudentGrades"
                 EntitySet="StudentGrade"
                 ReturnType="Collection(SchoolModel.StudentGrade)">
        <Parameter Name="StudentID" Mode="In" Type="Int32" />
 </FunctionImport>
```
 

 

## <a name="key-element-csdl"></a><span data-ttu-id="9a003-580">Key 元素 (CSDL)</span><span class="sxs-lookup"><span data-stu-id="9a003-580">Key Element (CSDL)</span></span>

<span data-ttu-id="9a003-581">**键**元素是 EntityType 元素的子元素，并定义*实体键*（属性或实体类型的属性，用于确定标识一组）。</span><span class="sxs-lookup"><span data-stu-id="9a003-581">The **Key** element is a child element of the EntityType element and defines an *entity key* (a property or a set of properties of an entity type that determine identity).</span></span> <span data-ttu-id="9a003-582">构成实体键的属性是在设计时选择的。</span><span class="sxs-lookup"><span data-stu-id="9a003-582">The properties that make up an entity key are chosen at design time.</span></span> <span data-ttu-id="9a003-583">实体键属性的值必须在运行时唯一标识实体集中的实体类型实例。</span><span class="sxs-lookup"><span data-stu-id="9a003-583">The values of entity key properties must uniquely identify an entity type instance within an entity set at run time.</span></span> <span data-ttu-id="9a003-584">在选择构成实体键的属性时应确保实例在实体集中的唯一性。</span><span class="sxs-lookup"><span data-stu-id="9a003-584">The properties that make up an entity key should be chosen to guarantee uniqueness of instances in an entity set.</span></span> <span data-ttu-id="9a003-585">**密钥**元素定义实体键通过引用一个或多个实体类型的属性。</span><span class="sxs-lookup"><span data-stu-id="9a003-585">The **Key** element defines an entity key by referencing one or more of the properties of an entity type.</span></span>

<span data-ttu-id="9a003-586">**密钥**元素可以具有以下子元素：</span><span class="sxs-lookup"><span data-stu-id="9a003-586">The **Key** element can have the following child elements:</span></span>

-   <span data-ttu-id="9a003-587">PropertyRef （一个或多个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-587">PropertyRef (one or more elements)</span></span>
-   <span data-ttu-id="9a003-588">批注元素 （零个或多个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-588">Annotation elements (zero or more elements)</span></span>

### <a name="applicable-attributes"></a><span data-ttu-id="9a003-589">适用的特性</span><span class="sxs-lookup"><span data-stu-id="9a003-589">Applicable Attributes</span></span>

<span data-ttu-id="9a003-590">可以将任意数量的 （自定义 XML 特性） 的批注特性应用于**密钥**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-590">Any number of annotation attributes (custom XML attributes) may be applied to the **Key** element.</span></span> <span data-ttu-id="9a003-591">然而，自定义特性可能不属于为 CSDL 保留的任何 XML 命名空间。</span><span class="sxs-lookup"><span data-stu-id="9a003-591">However, custom attributes may not belong to any XML namespace that is reserved for CSDL.</span></span> <span data-ttu-id="9a003-592">任何两个自定义特性的完全限定名称都不能相同。</span><span class="sxs-lookup"><span data-stu-id="9a003-592">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

### <a name="example"></a><span data-ttu-id="9a003-593">示例</span><span class="sxs-lookup"><span data-stu-id="9a003-593">Example</span></span>

<span data-ttu-id="9a003-594">下面的示例定义名为的实体类型**通讯簿**。</span><span class="sxs-lookup"><span data-stu-id="9a003-594">The example below defines an entity type named **Book**.</span></span> <span data-ttu-id="9a003-595">通过引用来定义实体键**ISBN**实体类型的属性。</span><span class="sxs-lookup"><span data-stu-id="9a003-595">The entity key is defined by referencing the **ISBN** property of the entity type.</span></span>

``` xml
 <EntityType Name="Book">
   <Key>
     <PropertyRef Name="ISBN" />
   </Key>
   <Property Type="String" Name="ISBN" Nullable="false" />
   <Property Type="String" Name="Title" Nullable="false" />
   <Property Type="Decimal" Name="Revision" Nullable="false" Precision="29" Scale="29" />
   <NavigationProperty Name="Publisher" Relationship="BooksModel.PublishedBy"
                       FromRole="Book" ToRole="Publisher" />
   <NavigationProperty Name="Authors" Relationship="BooksModel.WrittenBy"
                       FromRole="Book" ToRole="Author" />
 </EntityType>
```
 

<span data-ttu-id="9a003-596">**ISBN**属性是实体键的一个好选择，因为国际标准书号 (ISBN) 唯一标识一本书。</span><span class="sxs-lookup"><span data-stu-id="9a003-596">The **ISBN** property is a good choice for the entity key because an International Standard Book Number (ISBN) uniquely identifies a book.</span></span>

<span data-ttu-id="9a003-597">下面的示例演示一个实体类型 (**作者**) 具有两个属性组成的实体键**名称**并**地址**。</span><span class="sxs-lookup"><span data-stu-id="9a003-597">The following example shows an entity type (**Author**) that has an entity key that consists of two properties, **Name** and **Address**.</span></span>

``` xml
 <EntityType Name="Author">
   <Key>
     <PropertyRef Name="Name" />
     <PropertyRef Name="Address" />
   </Key>
   <Property Type="String" Name="Name" Nullable="false" />
   <Property Type="String" Name="Address" Nullable="false" />
   <NavigationProperty Name="Books" Relationship="BooksModel.WrittenBy"
                       FromRole="Author" ToRole="Book" />
 </EntityType>
```
 

<span data-ttu-id="9a003-598">使用**名称**并**地址**的实体键是合理的选择，，因为两个具有相同名称的作者不太可能 live 在相同的地址。</span><span class="sxs-lookup"><span data-stu-id="9a003-598">Using **Name** and **Address** for the entity key is a reasonable choice, because two authors of the same name are unlikely to live at the same address.</span></span> <span data-ttu-id="9a003-599">但是，针对实体键的这种选择并不能绝对确保实体键在实体集中的唯一性。</span><span class="sxs-lookup"><span data-stu-id="9a003-599">However, this choice for an entity key does not absolutely guarantee unique entity keys in an entity set.</span></span> <span data-ttu-id="9a003-600">添加一个属性，如**作者 Id**，可用来唯一地标识将在这种情况下建议的作者。</span><span class="sxs-lookup"><span data-stu-id="9a003-600">Adding a property, such as **AuthorId**, that could be used to uniquely identify an author would be recommended in this case.</span></span>

 

## <a name="member-element-csdl"></a><span data-ttu-id="9a003-601">Member 元素 (CSDL)</span><span class="sxs-lookup"><span data-stu-id="9a003-601">Member Element (CSDL)</span></span>

<span data-ttu-id="9a003-602">**成员**元素是 EnumType 元素的子元素，定义枚举类型的成员。</span><span class="sxs-lookup"><span data-stu-id="9a003-602">The **Member** element is a child element of the EnumType element and defines a member of the enumerated type.</span></span>

### <a name="applicable-attributes"></a><span data-ttu-id="9a003-603">适用的特性</span><span class="sxs-lookup"><span data-stu-id="9a003-603">Applicable Attributes</span></span>

<span data-ttu-id="9a003-604">下表描述了可应用于的特性**FunctionImport**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-604">The table below describes the attributes that can be applied to the **FunctionImport** element.</span></span>

| <span data-ttu-id="9a003-605">特性名</span><span class="sxs-lookup"><span data-stu-id="9a003-605">Attribute Name</span></span> | <span data-ttu-id="9a003-606">是否必需</span><span class="sxs-lookup"><span data-stu-id="9a003-606">Is Required</span></span> | <span data-ttu-id="9a003-607">“值”</span><span class="sxs-lookup"><span data-stu-id="9a003-607">Value</span></span>                                                                                                                                                                                    |
|:---------------|:------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9a003-608">**名称**</span><span class="sxs-lookup"><span data-stu-id="9a003-608">**Name**</span></span>       | <span data-ttu-id="9a003-609">是</span><span class="sxs-lookup"><span data-stu-id="9a003-609">Yes</span></span>         | <span data-ttu-id="9a003-610">成员名。</span><span class="sxs-lookup"><span data-stu-id="9a003-610">The name of the member.</span></span>                                                                                                                                                                  |
| <span data-ttu-id="9a003-611">**值**</span><span class="sxs-lookup"><span data-stu-id="9a003-611">**Value**</span></span>      | <span data-ttu-id="9a003-612">否</span><span class="sxs-lookup"><span data-stu-id="9a003-612">No</span></span>          | <span data-ttu-id="9a003-613">成员的值。</span><span class="sxs-lookup"><span data-stu-id="9a003-613">The value of the member.</span></span> <span data-ttu-id="9a003-614">默认情况下，第一个成员具有值 0，并且每个连续的枚举数的值加 1。</span><span class="sxs-lookup"><span data-stu-id="9a003-614">By default, the first member has the value 0, and the value of each successive enumerator is incremented by 1.</span></span> <span data-ttu-id="9a003-615">可能存在多个具有相同的值成员。</span><span class="sxs-lookup"><span data-stu-id="9a003-615">Multiple members with the same values may exist.</span></span> |

 

> [!NOTE]
> <span data-ttu-id="9a003-616">可以将任意数量的 （自定义 XML 特性） 的批注特性应用于**FunctionImport**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-616">Any number of annotation attributes (custom XML attributes) may be applied to the **FunctionImport** element.</span></span> <span data-ttu-id="9a003-617">然而，自定义特性可能不属于为 CSDL 保留的任何 XML 命名空间。</span><span class="sxs-lookup"><span data-stu-id="9a003-617">However, custom attributes may not belong to any XML namespace that is reserved for CSDL.</span></span> <span data-ttu-id="9a003-618">任何两个自定义特性的完全限定名称都不能相同。</span><span class="sxs-lookup"><span data-stu-id="9a003-618">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

 

### <a name="example"></a><span data-ttu-id="9a003-619">示例</span><span class="sxs-lookup"><span data-stu-id="9a003-619">Example</span></span>

<span data-ttu-id="9a003-620">下面的示例演示**EnumType**具有三个元素**成员**元素：</span><span class="sxs-lookup"><span data-stu-id="9a003-620">The following example shows an **EnumType** element with three **Member** elements:</span></span>

``` xml
 <EnumType Name="Color">
   <Member Name="Red" Value=”1”/>
   <Member Name="Green" Value=”3” />
   <Member Name="Blue" Value=”5”/>
 </EntityType>
```
 

 

## <a name="navigationproperty-element-csdl"></a><span data-ttu-id="9a003-621">NavigationProperty 元素 (CSDL)</span><span class="sxs-lookup"><span data-stu-id="9a003-621">NavigationProperty Element (CSDL)</span></span>

<span data-ttu-id="9a003-622">一个**NavigationProperty**元素定义导航属性，用于提供对关联另一端的引用。</span><span class="sxs-lookup"><span data-stu-id="9a003-622">A **NavigationProperty** element defines a navigation property, which provides a reference to the other end of an association.</span></span> <span data-ttu-id="9a003-623">与属性元素具有定义的属性，不同的形状和特征的数据定义导航属性。</span><span class="sxs-lookup"><span data-stu-id="9a003-623">Unlike properties defined with the Property element, navigation properties do not define the shape and characteristics of data.</span></span> <span data-ttu-id="9a003-624">它们提供了一种在两个实体类型之间导航关联的方法。</span><span class="sxs-lookup"><span data-stu-id="9a003-624">They provide a way to navigate an association between two entity types.</span></span>

<span data-ttu-id="9a003-625">注意，对于关联两端的两种实体类型，导航属性都是可选的。</span><span class="sxs-lookup"><span data-stu-id="9a003-625">Note that navigation properties are optional on both entity types at the ends of an association.</span></span> <span data-ttu-id="9a003-626">如果您对于位于关联一端的实体类型定义一个导航属性，则不需要对于位于关联另一端的实体类型定义导航属性。</span><span class="sxs-lookup"><span data-stu-id="9a003-626">If you define a navigation property on one entity type at the end of an association, you do not have to define a navigation property on the entity type at the other end of the association.</span></span>

<span data-ttu-id="9a003-627">导航属性返回的数据类型是由其远程关联端的重数确定的。</span><span class="sxs-lookup"><span data-stu-id="9a003-627">The data type returned by a navigation property is determined by the multiplicity of its remote association end.</span></span> <span data-ttu-id="9a003-628">例如，假设导航属性， **OrdersNavProp**，位于**客户**实体类型和定位之间的一对多关联**客户**和**顺序**。</span><span class="sxs-lookup"><span data-stu-id="9a003-628">For example, suppose a navigation property, **OrdersNavProp**, exists on a **Customer** entity type and navigates a one-to-many association between **Customer** and **Order**.</span></span> <span data-ttu-id="9a003-629">因为导航属性的远程关联端的重数很多 (\*)，其数据类型是一个集合 (的**顺序**)。</span><span class="sxs-lookup"><span data-stu-id="9a003-629">Because the remote association end for the navigation property has multiplicity many (\*), its data type is a collection (of **Order**).</span></span> <span data-ttu-id="9a003-630">同样，如果导航属性**CustomerNavProp**，位于**顺序**其数据类型应为实体类型**客户**由于远程端的多重性是一 （1)。</span><span class="sxs-lookup"><span data-stu-id="9a003-630">Similarly, if a navigation property, **CustomerNavProp**, exists on the **Order** entity type, its data type would be **Customer** since the multiplicity of the remote end is one (1).</span></span>

<span data-ttu-id="9a003-631">一个**NavigationProperty**元素可以具有下列子元素 （按所列顺序）：</span><span class="sxs-lookup"><span data-stu-id="9a003-631">A **NavigationProperty** element can have the following child elements (in the order listed):</span></span>

-   <span data-ttu-id="9a003-632">文档 （零个或一个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-632">Documentation (zero or one element)</span></span>
-   <span data-ttu-id="9a003-633">批注元素 （零个或多个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-633">Annotation elements (zero or more elements)</span></span>

### <a name="applicable-attributes"></a><span data-ttu-id="9a003-634">适用的特性</span><span class="sxs-lookup"><span data-stu-id="9a003-634">Applicable Attributes</span></span>

<span data-ttu-id="9a003-635">下表描述了可应用于的特性**NavigationProperty**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-635">The table below describes the attributes that can be applied to the **NavigationProperty** element.</span></span>

| <span data-ttu-id="9a003-636">特性名</span><span class="sxs-lookup"><span data-stu-id="9a003-636">Attribute Name</span></span>   | <span data-ttu-id="9a003-637">是否必需</span><span class="sxs-lookup"><span data-stu-id="9a003-637">Is Required</span></span> | <span data-ttu-id="9a003-638">“值”</span><span class="sxs-lookup"><span data-stu-id="9a003-638">Value</span></span>                                                                                                                                                                                                                                            |
|:-----------------|:------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9a003-639">**名称**</span><span class="sxs-lookup"><span data-stu-id="9a003-639">**Name**</span></span>         | <span data-ttu-id="9a003-640">是</span><span class="sxs-lookup"><span data-stu-id="9a003-640">Yes</span></span>         | <span data-ttu-id="9a003-641">导航属性的名称。</span><span class="sxs-lookup"><span data-stu-id="9a003-641">The name of the navigation property.</span></span>                                                                                                                                                                                                             |
| <span data-ttu-id="9a003-642">**关系**</span><span class="sxs-lookup"><span data-stu-id="9a003-642">**Relationship**</span></span> | <span data-ttu-id="9a003-643">是</span><span class="sxs-lookup"><span data-stu-id="9a003-643">Yes</span></span>         | <span data-ttu-id="9a003-644">处于模型的作用域中的关联的名称。</span><span class="sxs-lookup"><span data-stu-id="9a003-644">The name of an association that is within the scope of the model.</span></span>                                                                                                                                                                                |
| <span data-ttu-id="9a003-645">**ToRole**</span><span class="sxs-lookup"><span data-stu-id="9a003-645">**ToRole**</span></span>       | <span data-ttu-id="9a003-646">是</span><span class="sxs-lookup"><span data-stu-id="9a003-646">Yes</span></span>         | <span data-ttu-id="9a003-647">导航在此结束的关联端。</span><span class="sxs-lookup"><span data-stu-id="9a003-647">The end of the association at which navigation ends.</span></span> <span data-ttu-id="9a003-648">值**ToRole**属性必须为之一的值与相同**角色**上一个 （AssociationEnd 元素中定义） 的关联端定义的属性。</span><span class="sxs-lookup"><span data-stu-id="9a003-648">The value of the **ToRole** attribute must be the same as the value of one of the **Role** attributes defined on one of the association ends (defined in the AssociationEnd element).</span></span>       |
| <span data-ttu-id="9a003-649">**FromRole**</span><span class="sxs-lookup"><span data-stu-id="9a003-649">**FromRole**</span></span>     | <span data-ttu-id="9a003-650">是</span><span class="sxs-lookup"><span data-stu-id="9a003-650">Yes</span></span>         | <span data-ttu-id="9a003-651">导航从其开始的关联端。</span><span class="sxs-lookup"><span data-stu-id="9a003-651">The end of the association from which navigation begins.</span></span> <span data-ttu-id="9a003-652">值**FromRole**属性必须为之一的值与相同**角色**上一个 （AssociationEnd 元素中定义） 的关联端定义的属性。</span><span class="sxs-lookup"><span data-stu-id="9a003-652">The value of the **FromRole** attribute must be the same as the value of one of the **Role** attributes defined on one of the association ends (defined in the AssociationEnd element).</span></span> |

 

> [!NOTE]
> <span data-ttu-id="9a003-653">可以将任意数量的 （自定义 XML 特性） 的批注特性应用于**NavigationProperty**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-653">Any number of annotation attributes (custom XML attributes) may be applied to the **NavigationProperty** element.</span></span> <span data-ttu-id="9a003-654">然而，自定义特性可能不属于为 CSDL 保留的任何 XML 命名空间。</span><span class="sxs-lookup"><span data-stu-id="9a003-654">However, custom attributes may not belong to any XML namespace that is reserved for CSDL.</span></span> <span data-ttu-id="9a003-655">任何两个自定义特性的完全限定名称都不能相同。</span><span class="sxs-lookup"><span data-stu-id="9a003-655">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

 

### <a name="example"></a><span data-ttu-id="9a003-656">示例</span><span class="sxs-lookup"><span data-stu-id="9a003-656">Example</span></span>

<span data-ttu-id="9a003-657">下面的示例定义一个实体类型 (**书籍**) 具有两个导航属性 (**PublishedBy**并**WrittenBy**):</span><span class="sxs-lookup"><span data-stu-id="9a003-657">The following example defines an entity type (**Book**) with two navigation properties (**PublishedBy** and **WrittenBy**):</span></span>

``` xml
 <EntityType Name="Book">
   <Key>
     <PropertyRef Name="ISBN" />
   </Key>
   <Property Type="String" Name="ISBN" Nullable="false" />
   <Property Type="String" Name="Title" Nullable="false" />
   <Property Type="Decimal" Name="Revision" Nullable="false" Precision="29" Scale="29" />
   <NavigationProperty Name="Publisher" Relationship="BooksModel.PublishedBy"
                       FromRole="Book" ToRole="Publisher" />
   <NavigationProperty Name="Authors" Relationship="BooksModel.WrittenBy"
                       FromRole="Book" ToRole="Author" />
 </EntityType>
```
 

 

## <a name="ondelete-element-csdl"></a><span data-ttu-id="9a003-658">OnDelete 元素 (CSDL)</span><span class="sxs-lookup"><span data-stu-id="9a003-658">OnDelete Element (CSDL)</span></span>

<span data-ttu-id="9a003-659">**OnDelete**概念架构定义语言 (CSDL) 中的元素定义与关联相关的行为。</span><span class="sxs-lookup"><span data-stu-id="9a003-659">The **OnDelete** element in conceptual schema definition language (CSDL) defines behavior that is connected with an association.</span></span> <span data-ttu-id="9a003-660">如果**操作**属性设置为**Cascade** ，另一端的关联相关的删除第一个一端的实体类型时，会删除关联另一端的实体类型。</span><span class="sxs-lookup"><span data-stu-id="9a003-660">If the **Action** attribute is set to **Cascade** on one end of an association, related entity types on the other end of the association are deleted when the entity type on the first end is deleted.</span></span> <span data-ttu-id="9a003-661">如果两个实体类型之间的关联是主键的键-主键键关系中，则加载的依赖对象删除而不考虑关联另一端上的主体对象时，删除**OnDelete**规范。</span><span class="sxs-lookup"><span data-stu-id="9a003-661">If the association between two entity types is a primary key-to-primary key relationship, then a loaded dependent object is deleted when the principal object on the other end of the association is deleted regardless of the **OnDelete** specification.</span></span>  

> [!NOTE]
> <span data-ttu-id="9a003-662">**OnDelete**元素仅会影响应用程序的运行时行为; 它不会影响数据源中的行为。</span><span class="sxs-lookup"><span data-stu-id="9a003-662">The **OnDelete** element only affects the runtime behavior of an application; it does not affect behavior in the data source.</span></span> <span data-ttu-id="9a003-663">在数据源中定义的行为应与在应用程序中定义的行为相同。</span><span class="sxs-lookup"><span data-stu-id="9a003-663">The behavior defined in the data source should be the same as the behavior defined in the application.</span></span>

 

<span data-ttu-id="9a003-664">**OnDelete**元素可以具有下列子元素 （按所列顺序）：</span><span class="sxs-lookup"><span data-stu-id="9a003-664">An **OnDelete** element can have the following child elements (in the order listed):</span></span>

-   <span data-ttu-id="9a003-665">文档 （零个或一个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-665">Documentation (zero or one element)</span></span>
-   <span data-ttu-id="9a003-666">批注元素 （零个或多个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-666">Annotation elements (zero or more elements)</span></span>

### <a name="applicable-attributes"></a><span data-ttu-id="9a003-667">适用的特性</span><span class="sxs-lookup"><span data-stu-id="9a003-667">Applicable Attributes</span></span>

<span data-ttu-id="9a003-668">下表描述了可应用于的特性**OnDelete**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-668">The table below describes the attributes that can be applied to the **OnDelete** element.</span></span>

| <span data-ttu-id="9a003-669">特性名</span><span class="sxs-lookup"><span data-stu-id="9a003-669">Attribute Name</span></span> | <span data-ttu-id="9a003-670">是否必需</span><span class="sxs-lookup"><span data-stu-id="9a003-670">Is Required</span></span> | <span data-ttu-id="9a003-671">“值”</span><span class="sxs-lookup"><span data-stu-id="9a003-671">Value</span></span>                                                                                                                                                                                                                         |
|:---------------|:------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9a003-672">**操作**</span><span class="sxs-lookup"><span data-stu-id="9a003-672">**Action**</span></span>     | <span data-ttu-id="9a003-673">是</span><span class="sxs-lookup"><span data-stu-id="9a003-673">Yes</span></span>         | <span data-ttu-id="9a003-674">**级联**或**None**。</span><span class="sxs-lookup"><span data-stu-id="9a003-674">**Cascade** or **None**.</span></span> <span data-ttu-id="9a003-675">如果**Cascade**，当删除主体实体类型时，将删除从属实体类型。</span><span class="sxs-lookup"><span data-stu-id="9a003-675">If **Cascade**, dependent entity types will be deleted when the principal entity type is deleted.</span></span> <span data-ttu-id="9a003-676">如果**None**，当删除主体实体类型时，将不会删除从属实体类型。</span><span class="sxs-lookup"><span data-stu-id="9a003-676">If **None**, dependent entity types will not be deleted when the principal entity type is deleted.</span></span> |

 

> [!NOTE]
> <span data-ttu-id="9a003-677">可以将任意数量的 （自定义 XML 特性） 的批注特性应用于**关联**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-677">Any number of annotation attributes (custom XML attributes) may be applied to the **Association** element.</span></span> <span data-ttu-id="9a003-678">然而，自定义特性可能不属于为 CSDL 保留的任何 XML 命名空间。</span><span class="sxs-lookup"><span data-stu-id="9a003-678">However, custom attributes may not belong to any XML namespace that is reserved for CSDL.</span></span> <span data-ttu-id="9a003-679">任何两个自定义特性的完全限定名称都不能相同。</span><span class="sxs-lookup"><span data-stu-id="9a003-679">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

 

### <a name="example"></a><span data-ttu-id="9a003-680">示例</span><span class="sxs-lookup"><span data-stu-id="9a003-680">Example</span></span>

<span data-ttu-id="9a003-681">下面的示例演示**关联**定义的元素**CustomerOrders**关联。</span><span class="sxs-lookup"><span data-stu-id="9a003-681">The following example shows an **Association** element that defines the **CustomerOrders** association.</span></span> <span data-ttu-id="9a003-682">**OnDelete**元素指示所有**订单**与特定相关的**客户**和已加载到 ObjectContext 时，将删除**客户**被删除。</span><span class="sxs-lookup"><span data-stu-id="9a003-682">The **OnDelete** element indicates that all **Orders** that are related to a particular **Customer** and have been loaded into the ObjectContext will be deleted when the **Customer** is deleted.</span></span>

``` xml
 <Association Name="CustomerOrders">
   <End Type="ExampleModel.Customer" Role="Customer" Multiplicity="1">
         <OnDelete Action="Cascade" />
   </End>
   <End Type="ExampleModel.Order" Role="Order" Multiplicity="*" />
 </Association>
```
 

 

## <a name="parameter-element-csdl"></a><span data-ttu-id="9a003-683">Parameter 元素 (CSDL)</span><span class="sxs-lookup"><span data-stu-id="9a003-683">Parameter Element (CSDL)</span></span>

<span data-ttu-id="9a003-684">**参数**概念架构定义语言 (CSDL) 中的元素可以是 FunctionImport 元素或 Function 元素的子级。</span><span class="sxs-lookup"><span data-stu-id="9a003-684">The **Parameter** element in conceptual schema definition language (CSDL) can be a child of the FunctionImport element or the Function element.</span></span>

### <a name="functionimport-element-application"></a><span data-ttu-id="9a003-685">FunctionImport 元素应用程序</span><span class="sxs-lookup"><span data-stu-id="9a003-685">FunctionImport Element Application</span></span>

<span data-ttu-id="9a003-686">一个**参数**元素 (作为子级**FunctionImport**元素) 用于在 CSDL 中定义的函数导入声明输入和输出参数。</span><span class="sxs-lookup"><span data-stu-id="9a003-686">A **Parameter** element (as a child of the **FunctionImport** element) is used to define input and output parameters for function imports that are declared in CSDL.</span></span>

<span data-ttu-id="9a003-687">**参数**元素可以具有下列子元素 （按所列顺序）：</span><span class="sxs-lookup"><span data-stu-id="9a003-687">The **Parameter** element can have the following child elements (in the order listed):</span></span>

-   <span data-ttu-id="9a003-688">文档 （允许零个或一个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-688">Documentation (zero or one elements allowed)</span></span>
-   <span data-ttu-id="9a003-689">批注元素 （允许零个或多个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-689">Annotation elements (zero or more elements allowed)</span></span>

#### <a name="applicable-attributes"></a><span data-ttu-id="9a003-690">适用的特性</span><span class="sxs-lookup"><span data-stu-id="9a003-690">Applicable Attributes</span></span>

<span data-ttu-id="9a003-691">下表介绍可应用于的特性**参数**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-691">The following table describes the attributes that can be applied to the **Parameter** element.</span></span>

| <span data-ttu-id="9a003-692">特性名</span><span class="sxs-lookup"><span data-stu-id="9a003-692">Attribute Name</span></span> | <span data-ttu-id="9a003-693">是否必需</span><span class="sxs-lookup"><span data-stu-id="9a003-693">Is Required</span></span> | <span data-ttu-id="9a003-694">“值”</span><span class="sxs-lookup"><span data-stu-id="9a003-694">Value</span></span>                                                                                                                                                                                                                           |
|:---------------|:------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9a003-695">**名称**</span><span class="sxs-lookup"><span data-stu-id="9a003-695">**Name**</span></span>       | <span data-ttu-id="9a003-696">是</span><span class="sxs-lookup"><span data-stu-id="9a003-696">Yes</span></span>         | <span data-ttu-id="9a003-697">参数的名称。</span><span class="sxs-lookup"><span data-stu-id="9a003-697">The name of the parameter.</span></span>                                                                                                                                                                                                      |
| <span data-ttu-id="9a003-698">**Type**</span><span class="sxs-lookup"><span data-stu-id="9a003-698">**Type**</span></span>       | <span data-ttu-id="9a003-699">是</span><span class="sxs-lookup"><span data-stu-id="9a003-699">Yes</span></span>         | <span data-ttu-id="9a003-700">参数类型。</span><span class="sxs-lookup"><span data-stu-id="9a003-700">The parameter type.</span></span> <span data-ttu-id="9a003-701">该值必须是**EDMSimpleType**或模型的作用域内的复杂类型。</span><span class="sxs-lookup"><span data-stu-id="9a003-701">The value must be an **EDMSimpleType** or a complex type that is within the scope of the model.</span></span>                                                                                                             |
| <span data-ttu-id="9a003-702">**模式**</span><span class="sxs-lookup"><span data-stu-id="9a003-702">**Mode**</span></span>       | <span data-ttu-id="9a003-703">否</span><span class="sxs-lookup"><span data-stu-id="9a003-703">No</span></span>          | <span data-ttu-id="9a003-704">**在中**，**出**，或**InOut**具体取决于参数是输入、 输出或输入/输出参数。</span><span class="sxs-lookup"><span data-stu-id="9a003-704">**In**, **Out**, or **InOut** depending on whether the parameter is an input, output, or input/output parameter.</span></span>                                                                                                                |
| <span data-ttu-id="9a003-705">**MaxLength**</span><span class="sxs-lookup"><span data-stu-id="9a003-705">**MaxLength**</span></span>  | <span data-ttu-id="9a003-706">否</span><span class="sxs-lookup"><span data-stu-id="9a003-706">No</span></span>          | <span data-ttu-id="9a003-707">参数的最大允许长度。</span><span class="sxs-lookup"><span data-stu-id="9a003-707">The maximum allowed length of the parameter.</span></span>                                                                                                                                                                                    |
| <span data-ttu-id="9a003-708">**精度**</span><span class="sxs-lookup"><span data-stu-id="9a003-708">**Precision**</span></span>  | <span data-ttu-id="9a003-709">否</span><span class="sxs-lookup"><span data-stu-id="9a003-709">No</span></span>          | <span data-ttu-id="9a003-710">参数的精度。</span><span class="sxs-lookup"><span data-stu-id="9a003-710">The precision of the parameter.</span></span>                                                                                                                                                                                                 |
| <span data-ttu-id="9a003-711">缩放</span><span class="sxs-lookup"><span data-stu-id="9a003-711">**Scale**</span></span>      | <span data-ttu-id="9a003-712">否</span><span class="sxs-lookup"><span data-stu-id="9a003-712">No</span></span>          | <span data-ttu-id="9a003-713">参数的小数位数。</span><span class="sxs-lookup"><span data-stu-id="9a003-713">The scale of the parameter.</span></span>                                                                                                                                                                                                     |
| <span data-ttu-id="9a003-714">**SRID**</span><span class="sxs-lookup"><span data-stu-id="9a003-714">**SRID**</span></span>       | <span data-ttu-id="9a003-715">否</span><span class="sxs-lookup"><span data-stu-id="9a003-715">No</span></span>          | <span data-ttu-id="9a003-716">系统的空间引用标识符。</span><span class="sxs-lookup"><span data-stu-id="9a003-716">Spatial System Reference Identifier.</span></span> <span data-ttu-id="9a003-717">仅对空间类型的参数有效。</span><span class="sxs-lookup"><span data-stu-id="9a003-717">Valid only for parameters of spatial types.</span></span> <span data-ttu-id="9a003-718">有关详细信息，请参阅[SRID](http://en.wikipedia.org/wiki/SRID)并[SRID (SQL Server)](https://msdn.microsoft.com/library/bb964707.aspx)。</span><span class="sxs-lookup"><span data-stu-id="9a003-718">For more information, see [SRID](http://en.wikipedia.org/wiki/SRID) and [SRID (SQL Server)](https://msdn.microsoft.com/library/bb964707.aspx).</span></span> |

 

> [!NOTE]
> <span data-ttu-id="9a003-719">可以将任意数量的 （自定义 XML 特性） 的批注特性应用于**参数**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-719">Any number of annotation attributes (custom XML attributes) may be applied to the **Parameter** element.</span></span> <span data-ttu-id="9a003-720">然而，自定义特性可能不属于为 CSDL 保留的任何 XML 命名空间。</span><span class="sxs-lookup"><span data-stu-id="9a003-720">However, custom attributes may not belong to any XML namespace that is reserved for CSDL.</span></span> <span data-ttu-id="9a003-721">任何两个自定义特性的完全限定名称都不能相同。</span><span class="sxs-lookup"><span data-stu-id="9a003-721">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

 

#### <a name="example"></a><span data-ttu-id="9a003-722">示例</span><span class="sxs-lookup"><span data-stu-id="9a003-722">Example</span></span>

<span data-ttu-id="9a003-723">下面的示例演示**FunctionImport**具有一个**参数**子元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-723">The following example shows a **FunctionImport** element with one **Parameter** child element.</span></span> <span data-ttu-id="9a003-724">函数接受一个输入参数并返回实体类型的集合。</span><span class="sxs-lookup"><span data-stu-id="9a003-724">The function accepts one input parameter and returns a collection of entity types.</span></span>

``` xml
 <FunctionImport Name="GetStudentGrades"
                 EntitySet="StudentGrade"
                 ReturnType="Collection(SchoolModel.StudentGrade)">
        <Parameter Name="StudentID" Mode="In" Type="Int32" />
 </FunctionImport>
```
 

### <a name="function-element-application"></a><span data-ttu-id="9a003-725">Function 元素应用程序</span><span class="sxs-lookup"><span data-stu-id="9a003-725">Function Element Application</span></span>

<span data-ttu-id="9a003-726">一个**参数**元素 (作为子级**函数**元素) 定义概念模型中的函数的定义或声明的参数。</span><span class="sxs-lookup"><span data-stu-id="9a003-726">A **Parameter** element (as a child of the **Function** element) defines parameters for functions that are defined or declared in a conceptual model.</span></span>

<span data-ttu-id="9a003-727">**参数**元素可以具有下列子元素 （按所列顺序）：</span><span class="sxs-lookup"><span data-stu-id="9a003-727">The **Parameter** element can have the following child elements (in the order listed):</span></span>

-   <span data-ttu-id="9a003-728">文档 （零个或一个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-728">Documentation (zero or one elements)</span></span>
-   <span data-ttu-id="9a003-729">CollectionType （零个或一个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-729">CollectionType (zero or one elements)</span></span>
-   <span data-ttu-id="9a003-730">ReferenceType （零个或一个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-730">ReferenceType (zero or one elements)</span></span>
-   <span data-ttu-id="9a003-731">RowType （零个或一个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-731">RowType (zero or one elements)</span></span>

> [!NOTE]
> <span data-ttu-id="9a003-732">只有一个**CollectionType**， **ReferenceType**，或**RowType**元素的子元素可以**属性**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-732">Only one of the **CollectionType**, **ReferenceType**, or **RowType** elements can be a child element of a **Property** element.</span></span>

 

-   <span data-ttu-id="9a003-733">批注元素 （允许零个或多个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-733">Annotation elements (zero or more elements allowed)</span></span>

> [!NOTE]
> <span data-ttu-id="9a003-734">Annotation 元素必须出现在所有其他子元素之后。</span><span class="sxs-lookup"><span data-stu-id="9a003-734">Annotation elements must appear after all other child elements.</span></span> <span data-ttu-id="9a003-735">批注元素只能在 CSDL v2 和更高版本。</span><span class="sxs-lookup"><span data-stu-id="9a003-735">Annotation elements are only allowed in CSDL v2 and later.</span></span>

 

#### <a name="applicable-attributes"></a><span data-ttu-id="9a003-736">适用的特性</span><span class="sxs-lookup"><span data-stu-id="9a003-736">Applicable Attributes</span></span>

<span data-ttu-id="9a003-737">下表介绍可应用于的特性**参数**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-737">The following table describes the attributes that can be applied to the **Parameter** element.</span></span>

| <span data-ttu-id="9a003-738">特性名</span><span class="sxs-lookup"><span data-stu-id="9a003-738">Attribute Name</span></span>   | <span data-ttu-id="9a003-739">是否必需</span><span class="sxs-lookup"><span data-stu-id="9a003-739">Is Required</span></span> | <span data-ttu-id="9a003-740">“值”</span><span class="sxs-lookup"><span data-stu-id="9a003-740">Value</span></span>                                                                                                                                                                                                                           |
|:-----------------|:------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9a003-741">**名称**</span><span class="sxs-lookup"><span data-stu-id="9a003-741">**Name**</span></span>         | <span data-ttu-id="9a003-742">是</span><span class="sxs-lookup"><span data-stu-id="9a003-742">Yes</span></span>         | <span data-ttu-id="9a003-743">参数的名称。</span><span class="sxs-lookup"><span data-stu-id="9a003-743">The name of the parameter.</span></span>                                                                                                                                                                                                      |
| <span data-ttu-id="9a003-744">**Type**</span><span class="sxs-lookup"><span data-stu-id="9a003-744">**Type**</span></span>         | <span data-ttu-id="9a003-745">否</span><span class="sxs-lookup"><span data-stu-id="9a003-745">No</span></span>          | <span data-ttu-id="9a003-746">参数类型。</span><span class="sxs-lookup"><span data-stu-id="9a003-746">The parameter type.</span></span> <span data-ttu-id="9a003-747">参数可以是以下任意类型（或这些类型的集合）：</span><span class="sxs-lookup"><span data-stu-id="9a003-747">A parameter can be any of the following types (or collections of these types):</span></span> <br/> <span data-ttu-id="9a003-748">**EdmSimpleType**</span><span class="sxs-lookup"><span data-stu-id="9a003-748">**EdmSimpleType**</span></span> <br/> <span data-ttu-id="9a003-749">Entity Type — 实体类型</span><span class="sxs-lookup"><span data-stu-id="9a003-749">entity type</span></span> <br/> <span data-ttu-id="9a003-750">Complex Type — 复杂类型</span><span class="sxs-lookup"><span data-stu-id="9a003-750">complex type</span></span> <br/> <span data-ttu-id="9a003-751">行类型</span><span class="sxs-lookup"><span data-stu-id="9a003-751">row type</span></span> <br/> <span data-ttu-id="9a003-752">Reference Type — 引用类型</span><span class="sxs-lookup"><span data-stu-id="9a003-752">reference type</span></span>                             |
| <span data-ttu-id="9a003-753">**可以为 null**</span><span class="sxs-lookup"><span data-stu-id="9a003-753">**Nullable**</span></span>     | <span data-ttu-id="9a003-754">否</span><span class="sxs-lookup"><span data-stu-id="9a003-754">No</span></span>          | <span data-ttu-id="9a003-755">**True** （默认值） 或**False**具体取决于属性是否可以具有**null**值。</span><span class="sxs-lookup"><span data-stu-id="9a003-755">**True** (the default value) or **False** depending on whether the property can have a **null** value.</span></span>                                                                                                                          |
| <span data-ttu-id="9a003-756">**DefaultValue**</span><span class="sxs-lookup"><span data-stu-id="9a003-756">**DefaultValue**</span></span> | <span data-ttu-id="9a003-757">否</span><span class="sxs-lookup"><span data-stu-id="9a003-757">No</span></span>          | <span data-ttu-id="9a003-758">属性的默认值。</span><span class="sxs-lookup"><span data-stu-id="9a003-758">The default value of the property.</span></span>                                                                                                                                                                                              |
| <span data-ttu-id="9a003-759">**MaxLength**</span><span class="sxs-lookup"><span data-stu-id="9a003-759">**MaxLength**</span></span>    | <span data-ttu-id="9a003-760">否</span><span class="sxs-lookup"><span data-stu-id="9a003-760">No</span></span>          | <span data-ttu-id="9a003-761">属性值的最大长度。</span><span class="sxs-lookup"><span data-stu-id="9a003-761">The maximum length of the property value.</span></span>                                                                                                                                                                                       |
| <span data-ttu-id="9a003-762">**FixedLength**</span><span class="sxs-lookup"><span data-stu-id="9a003-762">**FixedLength**</span></span>  | <span data-ttu-id="9a003-763">否</span><span class="sxs-lookup"><span data-stu-id="9a003-763">No</span></span>          | <span data-ttu-id="9a003-764">**True**或**False**具体取决于属性值是否将作为固定的长度字符串存储。</span><span class="sxs-lookup"><span data-stu-id="9a003-764">**True** or **False** depending on whether the property value will be stored as a fixed length string.</span></span>                                                                                                                          |
| <span data-ttu-id="9a003-765">**精度**</span><span class="sxs-lookup"><span data-stu-id="9a003-765">**Precision**</span></span>    | <span data-ttu-id="9a003-766">否</span><span class="sxs-lookup"><span data-stu-id="9a003-766">No</span></span>          | <span data-ttu-id="9a003-767">属性值的精度。</span><span class="sxs-lookup"><span data-stu-id="9a003-767">The precision of the property value.</span></span>                                                                                                                                                                                            |
| <span data-ttu-id="9a003-768">缩放</span><span class="sxs-lookup"><span data-stu-id="9a003-768">**Scale**</span></span>        | <span data-ttu-id="9a003-769">否</span><span class="sxs-lookup"><span data-stu-id="9a003-769">No</span></span>          | <span data-ttu-id="9a003-770">属性值的刻度。</span><span class="sxs-lookup"><span data-stu-id="9a003-770">The scale of the property value.</span></span>                                                                                                                                                                                                |
| <span data-ttu-id="9a003-771">**SRID**</span><span class="sxs-lookup"><span data-stu-id="9a003-771">**SRID**</span></span>         | <span data-ttu-id="9a003-772">否</span><span class="sxs-lookup"><span data-stu-id="9a003-772">No</span></span>          | <span data-ttu-id="9a003-773">系统的空间引用标识符。</span><span class="sxs-lookup"><span data-stu-id="9a003-773">Spatial System Reference Identifier.</span></span> <span data-ttu-id="9a003-774">仅对空间类型的属性有效。</span><span class="sxs-lookup"><span data-stu-id="9a003-774">Valid only for properties of spatial types.</span></span> <span data-ttu-id="9a003-775">有关详细信息，请参阅[SRID](http://en.wikipedia.org/wiki/SRID)并[SRID (SQL Server)](https://msdn.microsoft.com/library/bb964707.aspx)。</span><span class="sxs-lookup"><span data-stu-id="9a003-775">For more information, see [SRID](http://en.wikipedia.org/wiki/SRID) and [SRID (SQL Server)](https://msdn.microsoft.com/library/bb964707.aspx).</span></span> |
| <span data-ttu-id="9a003-776">**Unicode**</span><span class="sxs-lookup"><span data-stu-id="9a003-776">**Unicode**</span></span>      | <span data-ttu-id="9a003-777">否</span><span class="sxs-lookup"><span data-stu-id="9a003-777">No</span></span>          | <span data-ttu-id="9a003-778">**True**或**False**具体取决于是否在属性值将存储为 Unicode 字符串。</span><span class="sxs-lookup"><span data-stu-id="9a003-778">**True** or **False** depending on whether the property value will be stored as a Unicode string.</span></span>                                                                                                                               |
| <span data-ttu-id="9a003-779">**排序规则**</span><span class="sxs-lookup"><span data-stu-id="9a003-779">**Collation**</span></span>    | <span data-ttu-id="9a003-780">否</span><span class="sxs-lookup"><span data-stu-id="9a003-780">No</span></span>          | <span data-ttu-id="9a003-781">指定要在数据源中使用的排序序列的字符串。</span><span class="sxs-lookup"><span data-stu-id="9a003-781">A string that specifies the collating sequence to be used in the data source.</span></span>                                                                                                                                                   |

 

> [!NOTE]
> <span data-ttu-id="9a003-782">可以将任意数量的 （自定义 XML 特性） 的批注特性应用于**参数**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-782">Any number of annotation attributes (custom XML attributes) may be applied to the **Parameter** element.</span></span> <span data-ttu-id="9a003-783">然而，自定义特性可能不属于为 CSDL 保留的任何 XML 命名空间。</span><span class="sxs-lookup"><span data-stu-id="9a003-783">However, custom attributes may not belong to any XML namespace that is reserved for CSDL.</span></span> <span data-ttu-id="9a003-784">任何两个自定义特性的完全限定名称都不能相同。</span><span class="sxs-lookup"><span data-stu-id="9a003-784">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

 

#### <a name="example"></a><span data-ttu-id="9a003-785">示例</span><span class="sxs-lookup"><span data-stu-id="9a003-785">Example</span></span>

<span data-ttu-id="9a003-786">下面的示例演示**函数**元素使用一个**参数**子元素来定义函数参数。</span><span class="sxs-lookup"><span data-stu-id="9a003-786">The following example shows a **Function** element that uses one **Parameter** child element to define a function parameter.</span></span>

``` xml
 <Function Name="GetYearsEmployed" ReturnType="Edm.Int32">
 <Parameter Name="Instructor" Type="SchoolModel.Person" />
   <DefiningExpression>
   Year(CurrentDateTime()) - Year(cast(Instructor.HireDate as DateTime))
   </DefiningExpression>
 </Function>
``` 

 

## <a name="principal-element-csdl"></a><span data-ttu-id="9a003-787">Principal 元素 (CSDL)</span><span class="sxs-lookup"><span data-stu-id="9a003-787">Principal Element (CSDL)</span></span>

<span data-ttu-id="9a003-788">**主体**概念架构定义语言 (CSDL) 中的元素是定义引用约束的主体端 ReferentialConstraint 元素的子元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-788">The **Principal** element in conceptual schema definition language (CSDL) is a child element to the ReferentialConstraint element that defines the principal end of a referential constraint.</span></span> <span data-ttu-id="9a003-789">一个**ReferentialConstraint**元素定义的是关系数据库中的引用完整性约束类似的功能。</span><span class="sxs-lookup"><span data-stu-id="9a003-789">A **ReferentialConstraint** element defines functionality that is similar to a referential integrity constraint in a relational database.</span></span> <span data-ttu-id="9a003-790">与数据库表中的一个（或多个）列可以引用另一个表的主键相同，实体类型的一个（或多个）属性可以引用另一个实体类型的实体键。</span><span class="sxs-lookup"><span data-stu-id="9a003-790">In the same way that a column (or columns) from a database table can reference the primary key of another table, a property (or properties) of an entity type can reference the entity key of another entity type.</span></span> <span data-ttu-id="9a003-791">引用的实体类型称为*主体端*的约束。</span><span class="sxs-lookup"><span data-stu-id="9a003-791">The entity type that is referenced is called the *principal end* of the constraint.</span></span> <span data-ttu-id="9a003-792">引用主体端的实体类型称为*依赖端*的约束。</span><span class="sxs-lookup"><span data-stu-id="9a003-792">The entity type that references the principal end is called the *dependent end* of the constraint.</span></span> <span data-ttu-id="9a003-793">**PropertyRef**元素用来指定哪些键引用的依赖端。</span><span class="sxs-lookup"><span data-stu-id="9a003-793">**PropertyRef** elements are used to specify which keys are referenced by the dependent end.</span></span>

<span data-ttu-id="9a003-794">**主体**元素可以具有下列子元素 （按所列顺序）：</span><span class="sxs-lookup"><span data-stu-id="9a003-794">The **Principal** element can have the following child elements (in the order listed):</span></span>

-   <span data-ttu-id="9a003-795">PropertyRef （一个或多个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-795">PropertyRef (one or more elements)</span></span>
-   <span data-ttu-id="9a003-796">批注元素 （零个或多个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-796">Annotation elements (zero or more elements)</span></span>

### <a name="applicable-attributes"></a><span data-ttu-id="9a003-797">适用的特性</span><span class="sxs-lookup"><span data-stu-id="9a003-797">Applicable Attributes</span></span>

<span data-ttu-id="9a003-798">下表描述了可应用于的特性**主体**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-798">The table below describes the attributes that can be applied to the **Principal** element.</span></span>

| <span data-ttu-id="9a003-799">特性名</span><span class="sxs-lookup"><span data-stu-id="9a003-799">Attribute Name</span></span> | <span data-ttu-id="9a003-800">是否必需</span><span class="sxs-lookup"><span data-stu-id="9a003-800">Is Required</span></span> | <span data-ttu-id="9a003-801">“值”</span><span class="sxs-lookup"><span data-stu-id="9a003-801">Value</span></span>                                                                |
|:---------------|:------------|:---------------------------------------------------------------------|
| <span data-ttu-id="9a003-802">**角色**</span><span class="sxs-lookup"><span data-stu-id="9a003-802">**Role**</span></span>       | <span data-ttu-id="9a003-803">是</span><span class="sxs-lookup"><span data-stu-id="9a003-803">Yes</span></span>         | <span data-ttu-id="9a003-804">关联的主体端的实体类型的名称。</span><span class="sxs-lookup"><span data-stu-id="9a003-804">The name of the entity type on the principal end of the association.</span></span> |

 

> [!NOTE]
> <span data-ttu-id="9a003-805">可以将任意数量的 （自定义 XML 特性） 的批注特性应用于**主体**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-805">Any number of annotation attributes (custom XML attributes) may be applied to the **Principal** element.</span></span> <span data-ttu-id="9a003-806">然而，自定义特性可能不属于为 CSDL 保留的任何 XML 命名空间。</span><span class="sxs-lookup"><span data-stu-id="9a003-806">However, custom attributes may not belong to any XML namespace that is reserved for CSDL.</span></span> <span data-ttu-id="9a003-807">任何两个自定义特性的完全限定名称都不能相同。</span><span class="sxs-lookup"><span data-stu-id="9a003-807">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

 

### <a name="example"></a><span data-ttu-id="9a003-808">示例</span><span class="sxs-lookup"><span data-stu-id="9a003-808">Example</span></span>

<span data-ttu-id="9a003-809">下面的示例演示**ReferentialConstraint**的定义一部分的元素**PublishedBy**关联。</span><span class="sxs-lookup"><span data-stu-id="9a003-809">The following example shows a **ReferentialConstraint** element that is part of the definition of the **PublishedBy** association.</span></span> <span data-ttu-id="9a003-810">**Id**的属性**发布服务器**实体类型构成引用约束的主体端。</span><span class="sxs-lookup"><span data-stu-id="9a003-810">The **Id** property of the **Publisher** entity type makes up the principal end of the referential constraint.</span></span>

``` xml
 <Association Name="PublishedBy">
   <End Type="BooksModel.Book" Role="Book" Multiplicity="*" >
   </End>
   <End Type="BooksModel.Publisher" Role="Publisher" Multiplicity="1" />
   <ReferentialConstraint>
     <Principal Role="Publisher">
       <PropertyRef Name="Id" />
     </Principal>
     <Dependent Role="Book">
       <PropertyRef Name="PublisherId" />
     </Dependent>
   </ReferentialConstraint>
 </Association>
```
 

 

## <a name="property-element-csdl"></a><span data-ttu-id="9a003-811">Property 元素 (CSDL)</span><span class="sxs-lookup"><span data-stu-id="9a003-811">Property Element (CSDL)</span></span>

<span data-ttu-id="9a003-812">**属性**概念架构定义语言 (CSDL) 中的元素可以是 EntityType 元素、 ComplexType 元素或 RowType 元素的子级。</span><span class="sxs-lookup"><span data-stu-id="9a003-812">The **Property** element in conceptual schema definition language (CSDL) can be a child of the EntityType element, the ComplexType element, or the RowType element.</span></span>

### <a name="entitytype-and-complextype-element-applications"></a><span data-ttu-id="9a003-813">EntityType 和 ComplexType 元素应用程序</span><span class="sxs-lookup"><span data-stu-id="9a003-813">EntityType and ComplexType Element Applications</span></span>

<span data-ttu-id="9a003-814">**属性**元素 (作为子级**EntityType**或**ComplexType**元素) 定义的形状和实体类型实例或复杂类型实例要包含的数据的特征.</span><span class="sxs-lookup"><span data-stu-id="9a003-814">**Property** elements (as children of **EntityType** or **ComplexType** elements) define the shape and characteristics of data that an entity type instance or complex type instance will contain.</span></span> <span data-ttu-id="9a003-815">概念模型中的属性类似于为类定义的属性。</span><span class="sxs-lookup"><span data-stu-id="9a003-815">Properties in a conceptual model are analogous to properties that are defined on a class.</span></span> <span data-ttu-id="9a003-816">正如类的属性定义类的形状和携带有关对象的信息一样，概念模型中的属性也定义实体类型的形状和携带有关实体类型实例的信息。</span><span class="sxs-lookup"><span data-stu-id="9a003-816">In the same way that properties on a class define the shape of the class and carry information about objects, properties in a conceptual model define the shape of an entity type and carry information about entity type instances.</span></span>

<span data-ttu-id="9a003-817">**属性**元素可以具有下列子元素 （按所列顺序）：</span><span class="sxs-lookup"><span data-stu-id="9a003-817">The **Property** element can have the following child elements (in the order listed):</span></span>

-   <span data-ttu-id="9a003-818">Documentation 元素 （允许零个或一个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-818">Documentation Element (zero or one elements allowed)</span></span>
-   <span data-ttu-id="9a003-819">批注元素 （允许零个或多个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-819">Annotation elements (zero or more elements allowed)</span></span>

<span data-ttu-id="9a003-820">以下方面可以应用于**属性**元素： **Nullable**， **DefaultValue**， **MaxLength**， **FixedLength**，**精度**，**规模**， **Unicode**，**排序规则**， **ConcurrencyMode**。</span><span class="sxs-lookup"><span data-stu-id="9a003-820">The following facets can be applied to a **Property** element: **Nullable**, **DefaultValue**, **MaxLength**, **FixedLength**, **Precision**, **Scale**, **Unicode**, **Collation**, **ConcurrencyMode**.</span></span> <span data-ttu-id="9a003-821">方面是一些 XML 特性，它们提供有关如何在数据存储区中存储属性值的信息。</span><span class="sxs-lookup"><span data-stu-id="9a003-821">Facets are XML attributes that provide information about how property values are stored in the data store.</span></span>

> [!NOTE]
> <span data-ttu-id="9a003-822">方面只能应用于类型的属性**EDMSimpleType**。</span><span class="sxs-lookup"><span data-stu-id="9a003-822">Facets can only be applied to properties of type **EDMSimpleType**.</span></span>

 

#### <a name="applicable-attributes"></a><span data-ttu-id="9a003-823">适用的特性</span><span class="sxs-lookup"><span data-stu-id="9a003-823">Applicable Attributes</span></span>

<span data-ttu-id="9a003-824">下表介绍可应用于的特性**属性**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-824">The following table describes the attributes that can be applied to the **Property** element.</span></span>

| <span data-ttu-id="9a003-825">特性名</span><span class="sxs-lookup"><span data-stu-id="9a003-825">Attribute Name</span></span>                                                         | <span data-ttu-id="9a003-826">是否必需</span><span class="sxs-lookup"><span data-stu-id="9a003-826">Is Required</span></span> | <span data-ttu-id="9a003-827">“值”</span><span class="sxs-lookup"><span data-stu-id="9a003-827">Value</span></span>                                                                                                                                                                                                                           |
|:-----------------------------------------------------------------------|:------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9a003-828">**名称**</span><span class="sxs-lookup"><span data-stu-id="9a003-828">**Name**</span></span>                                                               | <span data-ttu-id="9a003-829">是</span><span class="sxs-lookup"><span data-stu-id="9a003-829">Yes</span></span>         | <span data-ttu-id="9a003-830">属性的名称。</span><span class="sxs-lookup"><span data-stu-id="9a003-830">The name of the property.</span></span>                                                                                                                                                                                                       |
| <span data-ttu-id="9a003-831">**Type**</span><span class="sxs-lookup"><span data-stu-id="9a003-831">**Type**</span></span>                                                               | <span data-ttu-id="9a003-832">是</span><span class="sxs-lookup"><span data-stu-id="9a003-832">Yes</span></span>         | <span data-ttu-id="9a003-833">属性值的类型。</span><span class="sxs-lookup"><span data-stu-id="9a003-833">The type of the property value.</span></span> <span data-ttu-id="9a003-834">属性值类型必须是**EDMSimpleType**或复杂类型 （由完全限定名称指示） 范围内的模型。</span><span class="sxs-lookup"><span data-stu-id="9a003-834">The property value type must be an **EDMSimpleType** or a complex type (indicated by a fully-qualified name) that is within scope of the model.</span></span>                                                 |
| <span data-ttu-id="9a003-835">**可以为 null**</span><span class="sxs-lookup"><span data-stu-id="9a003-835">**Nullable**</span></span>                                                           | <span data-ttu-id="9a003-836">否</span><span class="sxs-lookup"><span data-stu-id="9a003-836">No</span></span>          | <span data-ttu-id="9a003-837">**True** （默认值） 或<strong>False</strong>具体取决于属性是否可以具有 null 值。</span><span class="sxs-lookup"><span data-stu-id="9a003-837">**True** (the default value) or <strong>False</strong> depending on whether the property can have a null value.</span></span> <br/> [!NOTE]                                                                                                   |
| <span data-ttu-id="9a003-838">> CSDL v1 中的复杂类型属性必须具有`Nullable="False"`。</span><span class="sxs-lookup"><span data-stu-id="9a003-838">> In the CSDL v1 a complex type property must have `Nullable="False"`.</span></span> |             |                                                                                                                                                                                                                                 |
| <span data-ttu-id="9a003-839">**DefaultValue**</span><span class="sxs-lookup"><span data-stu-id="9a003-839">**DefaultValue**</span></span>                                                       | <span data-ttu-id="9a003-840">否</span><span class="sxs-lookup"><span data-stu-id="9a003-840">No</span></span>          | <span data-ttu-id="9a003-841">属性的默认值。</span><span class="sxs-lookup"><span data-stu-id="9a003-841">The default value of the property.</span></span>                                                                                                                                                                                              |
| <span data-ttu-id="9a003-842">**MaxLength**</span><span class="sxs-lookup"><span data-stu-id="9a003-842">**MaxLength**</span></span>                                                          | <span data-ttu-id="9a003-843">否</span><span class="sxs-lookup"><span data-stu-id="9a003-843">No</span></span>          | <span data-ttu-id="9a003-844">属性值的最大长度。</span><span class="sxs-lookup"><span data-stu-id="9a003-844">The maximum length of the property value.</span></span>                                                                                                                                                                                       |
| <span data-ttu-id="9a003-845">**FixedLength**</span><span class="sxs-lookup"><span data-stu-id="9a003-845">**FixedLength**</span></span>                                                        | <span data-ttu-id="9a003-846">否</span><span class="sxs-lookup"><span data-stu-id="9a003-846">No</span></span>          | <span data-ttu-id="9a003-847">**True**或**False**具体取决于属性值是否将作为固定的长度字符串存储。</span><span class="sxs-lookup"><span data-stu-id="9a003-847">**True** or **False** depending on whether the property value will be stored as a fixed length string.</span></span>                                                                                                                          |
| <span data-ttu-id="9a003-848">**精度**</span><span class="sxs-lookup"><span data-stu-id="9a003-848">**Precision**</span></span>                                                          | <span data-ttu-id="9a003-849">否</span><span class="sxs-lookup"><span data-stu-id="9a003-849">No</span></span>          | <span data-ttu-id="9a003-850">属性值的精度。</span><span class="sxs-lookup"><span data-stu-id="9a003-850">The precision of the property value.</span></span>                                                                                                                                                                                            |
| <span data-ttu-id="9a003-851">缩放</span><span class="sxs-lookup"><span data-stu-id="9a003-851">**Scale**</span></span>                                                              | <span data-ttu-id="9a003-852">否</span><span class="sxs-lookup"><span data-stu-id="9a003-852">No</span></span>          | <span data-ttu-id="9a003-853">属性值的刻度。</span><span class="sxs-lookup"><span data-stu-id="9a003-853">The scale of the property value.</span></span>                                                                                                                                                                                                |
| <span data-ttu-id="9a003-854">**SRID**</span><span class="sxs-lookup"><span data-stu-id="9a003-854">**SRID**</span></span>                                                               | <span data-ttu-id="9a003-855">否</span><span class="sxs-lookup"><span data-stu-id="9a003-855">No</span></span>          | <span data-ttu-id="9a003-856">系统的空间引用标识符。</span><span class="sxs-lookup"><span data-stu-id="9a003-856">Spatial System Reference Identifier.</span></span> <span data-ttu-id="9a003-857">仅对空间类型的属性有效。</span><span class="sxs-lookup"><span data-stu-id="9a003-857">Valid only for properties of spatial types.</span></span> <span data-ttu-id="9a003-858">有关详细信息，请参阅[SRID](http://en.wikipedia.org/wiki/SRID)并[SRID (SQL Server)](https://msdn.microsoft.com/library/bb964707.aspx)。</span><span class="sxs-lookup"><span data-stu-id="9a003-858">For more information, see [SRID](http://en.wikipedia.org/wiki/SRID) and [SRID (SQL Server)](https://msdn.microsoft.com/library/bb964707.aspx).</span></span> |
| <span data-ttu-id="9a003-859">**Unicode**</span><span class="sxs-lookup"><span data-stu-id="9a003-859">**Unicode**</span></span>                                                            | <span data-ttu-id="9a003-860">否</span><span class="sxs-lookup"><span data-stu-id="9a003-860">No</span></span>          | <span data-ttu-id="9a003-861">**True**或**False**具体取决于是否在属性值将存储为 Unicode 字符串。</span><span class="sxs-lookup"><span data-stu-id="9a003-861">**True** or **False** depending on whether the property value will be stored as a Unicode string.</span></span>                                                                                                                               |
| <span data-ttu-id="9a003-862">**排序规则**</span><span class="sxs-lookup"><span data-stu-id="9a003-862">**Collation**</span></span>                                                          | <span data-ttu-id="9a003-863">否</span><span class="sxs-lookup"><span data-stu-id="9a003-863">No</span></span>          | <span data-ttu-id="9a003-864">指定要在数据源中使用的排序序列的字符串。</span><span class="sxs-lookup"><span data-stu-id="9a003-864">A string that specifies the collating sequence to be used in the data source.</span></span>                                                                                                                                                   |
| <span data-ttu-id="9a003-865">**ConcurrencyMode**</span><span class="sxs-lookup"><span data-stu-id="9a003-865">**ConcurrencyMode**</span></span>                                                    | <span data-ttu-id="9a003-866">否</span><span class="sxs-lookup"><span data-stu-id="9a003-866">No</span></span>          | <span data-ttu-id="9a003-867">**无**（默认值） 或**Fixed**。</span><span class="sxs-lookup"><span data-stu-id="9a003-867">**None** (the default value) or **Fixed**.</span></span> <span data-ttu-id="9a003-868">如果值设置为**Fixed**，将开放式并发检查中使用的属性值。</span><span class="sxs-lookup"><span data-stu-id="9a003-868">If the value is set to **Fixed**, the property value will be used in optimistic concurrency checks.</span></span>                                                                                  |

 

> [!NOTE]
> <span data-ttu-id="9a003-869">可以将任意数量的 （自定义 XML 特性） 的批注特性应用于**属性**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-869">Any number of annotation attributes (custom XML attributes) may be applied to the **Property** element.</span></span> <span data-ttu-id="9a003-870">然而，自定义特性可能不属于为 CSDL 保留的任何 XML 命名空间。</span><span class="sxs-lookup"><span data-stu-id="9a003-870">However, custom attributes may not belong to any XML namespace that is reserved for CSDL.</span></span> <span data-ttu-id="9a003-871">任何两个自定义特性的完全限定名称都不能相同。</span><span class="sxs-lookup"><span data-stu-id="9a003-871">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

 

#### <a name="example"></a><span data-ttu-id="9a003-872">示例</span><span class="sxs-lookup"><span data-stu-id="9a003-872">Example</span></span>

<span data-ttu-id="9a003-873">下面的示例演示**EntityType**具有三个元素**属性**元素：</span><span class="sxs-lookup"><span data-stu-id="9a003-873">The following example shows an **EntityType** element with three **Property** elements:</span></span>

``` xml
 <EntityType Name="Book">
   <Key>
     <PropertyRef Name="ISBN" />
   </Key>
   <Property Type="String" Name="ISBN" Nullable="false" />
   <Property Type="String" Name="Title" Nullable="false" />
   <Property Type="Decimal" Name="Revision" Nullable="false" Precision="29" Scale="29" />
   <NavigationProperty Name="Publisher" Relationship="BooksModel.PublishedBy"
                       FromRole="Book" ToRole="Publisher" />
   <NavigationProperty Name="Authors" Relationship="BooksModel.WrittenBy"
                       FromRole="Book" ToRole="Author" />
 </EntityType>
```
 

<span data-ttu-id="9a003-874">下面的示例演示**ComplexType**具有五个元素**属性**元素：</span><span class="sxs-lookup"><span data-stu-id="9a003-874">The following example shows a **ComplexType** element with five **Property** elements:</span></span>

``` xml
 <ComplexType Name="Address" >
   <Property Type="String" Name="StreetAddress" Nullable="false" />
   <Property Type="String" Name="City" Nullable="false" />
   <Property Type="String" Name="StateOrProvince" Nullable="false" />
   <Property Type="String" Name="Country" Nullable="false" />
   <Property Type="String" Name="PostalCode" Nullable="false" />
 </ComplexType>
```
 

### <a name="rowtype-element-application"></a><span data-ttu-id="9a003-875">RowType 元素应用</span><span class="sxs-lookup"><span data-stu-id="9a003-875">RowType Element Application</span></span>

<span data-ttu-id="9a003-876">**属性**元素 (作为的子级**RowType**元素) 定义的形状和特征可以传递到或从模型定义函数返回的数据。</span><span class="sxs-lookup"><span data-stu-id="9a003-876">**Property** elements (as the children of a **RowType** element) define the shape and characteristics of data that can be passed to or returned from a model-defined function.</span></span>  

<span data-ttu-id="9a003-877">**属性**元素可以具有下列子元素之一：</span><span class="sxs-lookup"><span data-stu-id="9a003-877">The **Property** element can have exactly one of the following child elements:</span></span>

-   <span data-ttu-id="9a003-878">CollectionType</span><span class="sxs-lookup"><span data-stu-id="9a003-878">CollectionType</span></span>
-   <span data-ttu-id="9a003-879">ReferenceType</span><span class="sxs-lookup"><span data-stu-id="9a003-879">ReferenceType</span></span>
-   <span data-ttu-id="9a003-880">RowType</span><span class="sxs-lookup"><span data-stu-id="9a003-880">RowType</span></span>

<span data-ttu-id="9a003-881">**属性**元素可以具有任何数字子批注元素的数目。</span><span class="sxs-lookup"><span data-stu-id="9a003-881">The **Property** element can have any number child annotation elements.</span></span>

> [!NOTE]
> <span data-ttu-id="9a003-882">批注元素只能在 CSDL v2 和更高版本。</span><span class="sxs-lookup"><span data-stu-id="9a003-882">Annotation elements are only allowed in CSDL v2 and later.</span></span>

 

#### <a name="applicable-attributes"></a><span data-ttu-id="9a003-883">适用的特性</span><span class="sxs-lookup"><span data-stu-id="9a003-883">Applicable Attributes</span></span>

<span data-ttu-id="9a003-884">下表介绍可应用于的特性**属性**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-884">The following table describes the attributes that can be applied to the **Property** element.</span></span>

| <span data-ttu-id="9a003-885">特性名</span><span class="sxs-lookup"><span data-stu-id="9a003-885">Attribute Name</span></span>                                                     | <span data-ttu-id="9a003-886">是否必需</span><span class="sxs-lookup"><span data-stu-id="9a003-886">Is Required</span></span> | <span data-ttu-id="9a003-887">“值”</span><span class="sxs-lookup"><span data-stu-id="9a003-887">Value</span></span>                                                                                                                                                                                                                           |
|:-------------------------------------------------------------------|:------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9a003-888">**名称**</span><span class="sxs-lookup"><span data-stu-id="9a003-888">**Name**</span></span>                                                           | <span data-ttu-id="9a003-889">是</span><span class="sxs-lookup"><span data-stu-id="9a003-889">Yes</span></span>         | <span data-ttu-id="9a003-890">属性的名称。</span><span class="sxs-lookup"><span data-stu-id="9a003-890">The name of the property.</span></span>                                                                                                                                                                                                       |
| <span data-ttu-id="9a003-891">**Type**</span><span class="sxs-lookup"><span data-stu-id="9a003-891">**Type**</span></span>                                                           | <span data-ttu-id="9a003-892">是</span><span class="sxs-lookup"><span data-stu-id="9a003-892">Yes</span></span>         | <span data-ttu-id="9a003-893">属性值的类型。</span><span class="sxs-lookup"><span data-stu-id="9a003-893">The type of the property value.</span></span>                                                                                                                                                                                                 |
| <span data-ttu-id="9a003-894">**可以为 null**</span><span class="sxs-lookup"><span data-stu-id="9a003-894">**Nullable**</span></span>                                                       | <span data-ttu-id="9a003-895">否</span><span class="sxs-lookup"><span data-stu-id="9a003-895">No</span></span>          | <span data-ttu-id="9a003-896">**True** （默认值） 或**False**具体取决于属性是否可以具有 null 值。</span><span class="sxs-lookup"><span data-stu-id="9a003-896">**True** (the default value) or **False** depending on whether the property can have a null value.</span></span> <br/> [!NOTE]                                                                                                                |
| <span data-ttu-id="9a003-897">> CSDL v1 中的复杂类型属性必须具有`Nullable="False"`。</span><span class="sxs-lookup"><span data-stu-id="9a003-897">> In CSDL v1 a complex type property must have `Nullable="False"`.</span></span> |             |                                                                                                                                                                                                                                 |
| <span data-ttu-id="9a003-898">**DefaultValue**</span><span class="sxs-lookup"><span data-stu-id="9a003-898">**DefaultValue**</span></span>                                                   | <span data-ttu-id="9a003-899">否</span><span class="sxs-lookup"><span data-stu-id="9a003-899">No</span></span>          | <span data-ttu-id="9a003-900">属性的默认值。</span><span class="sxs-lookup"><span data-stu-id="9a003-900">The default value of the property.</span></span>                                                                                                                                                                                              |
| <span data-ttu-id="9a003-901">**MaxLength**</span><span class="sxs-lookup"><span data-stu-id="9a003-901">**MaxLength**</span></span>                                                      | <span data-ttu-id="9a003-902">否</span><span class="sxs-lookup"><span data-stu-id="9a003-902">No</span></span>          | <span data-ttu-id="9a003-903">属性值的最大长度。</span><span class="sxs-lookup"><span data-stu-id="9a003-903">The maximum length of the property value.</span></span>                                                                                                                                                                                       |
| <span data-ttu-id="9a003-904">**FixedLength**</span><span class="sxs-lookup"><span data-stu-id="9a003-904">**FixedLength**</span></span>                                                    | <span data-ttu-id="9a003-905">否</span><span class="sxs-lookup"><span data-stu-id="9a003-905">No</span></span>          | <span data-ttu-id="9a003-906">**True**或**False**具体取决于属性值是否将作为固定的长度字符串存储。</span><span class="sxs-lookup"><span data-stu-id="9a003-906">**True** or **False** depending on whether the property value will be stored as a fixed length string.</span></span>                                                                                                                          |
| <span data-ttu-id="9a003-907">**精度**</span><span class="sxs-lookup"><span data-stu-id="9a003-907">**Precision**</span></span>                                                      | <span data-ttu-id="9a003-908">否</span><span class="sxs-lookup"><span data-stu-id="9a003-908">No</span></span>          | <span data-ttu-id="9a003-909">属性值的精度。</span><span class="sxs-lookup"><span data-stu-id="9a003-909">The precision of the property value.</span></span>                                                                                                                                                                                            |
| <span data-ttu-id="9a003-910">缩放</span><span class="sxs-lookup"><span data-stu-id="9a003-910">**Scale**</span></span>                                                          | <span data-ttu-id="9a003-911">否</span><span class="sxs-lookup"><span data-stu-id="9a003-911">No</span></span>          | <span data-ttu-id="9a003-912">属性值的刻度。</span><span class="sxs-lookup"><span data-stu-id="9a003-912">The scale of the property value.</span></span>                                                                                                                                                                                                |
| <span data-ttu-id="9a003-913">**SRID**</span><span class="sxs-lookup"><span data-stu-id="9a003-913">**SRID**</span></span>                                                           | <span data-ttu-id="9a003-914">否</span><span class="sxs-lookup"><span data-stu-id="9a003-914">No</span></span>          | <span data-ttu-id="9a003-915">系统的空间引用标识符。</span><span class="sxs-lookup"><span data-stu-id="9a003-915">Spatial System Reference Identifier.</span></span> <span data-ttu-id="9a003-916">仅对空间类型的属性有效。</span><span class="sxs-lookup"><span data-stu-id="9a003-916">Valid only for properties of spatial types.</span></span> <span data-ttu-id="9a003-917">有关详细信息，请参阅[SRID](http://en.wikipedia.org/wiki/SRID)并[SRID (SQL Server)](https://msdn.microsoft.com/library/bb964707.aspx)。</span><span class="sxs-lookup"><span data-stu-id="9a003-917">For more information, see [SRID](http://en.wikipedia.org/wiki/SRID) and [SRID (SQL Server)](https://msdn.microsoft.com/library/bb964707.aspx).</span></span> |
| <span data-ttu-id="9a003-918">**Unicode**</span><span class="sxs-lookup"><span data-stu-id="9a003-918">**Unicode**</span></span>                                                        | <span data-ttu-id="9a003-919">否</span><span class="sxs-lookup"><span data-stu-id="9a003-919">No</span></span>          | <span data-ttu-id="9a003-920">**True**或**False**具体取决于是否在属性值将存储为 Unicode 字符串。</span><span class="sxs-lookup"><span data-stu-id="9a003-920">**True** or **False** depending on whether the property value will be stored as a Unicode string.</span></span>                                                                                                                               |
| <span data-ttu-id="9a003-921">**排序规则**</span><span class="sxs-lookup"><span data-stu-id="9a003-921">**Collation**</span></span>                                                      | <span data-ttu-id="9a003-922">否</span><span class="sxs-lookup"><span data-stu-id="9a003-922">No</span></span>          | <span data-ttu-id="9a003-923">指定要在数据源中使用的排序序列的字符串。</span><span class="sxs-lookup"><span data-stu-id="9a003-923">A string that specifies the collating sequence to be used in the data source.</span></span>                                                                                                                                                   |

 

> [!NOTE]
> <span data-ttu-id="9a003-924">可以将任意数量的 （自定义 XML 特性） 的批注特性应用于**属性**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-924">Any number of annotation attributes (custom XML attributes) may be applied to the **Property** element.</span></span> <span data-ttu-id="9a003-925">然而，自定义特性可能不属于为 CSDL 保留的任何 XML 命名空间。</span><span class="sxs-lookup"><span data-stu-id="9a003-925">However, custom attributes may not belong to any XML namespace that is reserved for CSDL.</span></span> <span data-ttu-id="9a003-926">任何两个自定义特性的完全限定名称都不能相同。</span><span class="sxs-lookup"><span data-stu-id="9a003-926">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

 

#### <a name="example"></a><span data-ttu-id="9a003-927">示例</span><span class="sxs-lookup"><span data-stu-id="9a003-927">Example</span></span>

<span data-ttu-id="9a003-928">下面的示例演示**属性**使用以定义模型定义函数的返回类型的形状的元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-928">The following example shows **Property** elements used to define the shape of the return type of a model-defined function.</span></span>

``` xml
 <Function Name="LastNamesAfter">
   <Parameter Name="someString" Type="Edm.String" />
   <ReturnType>
    <CollectionType>
      <RowType>
        <Property Name="FirstName" Type="Edm.String" Nullable="false" />
        <Property Name="LastName" Type="Edm.String" Nullable="false" />
      </RowType>
    </CollectionType>
   </ReturnType>
   <DefiningExpression>
             SELECT VALUE ROW(p.FirstName, p.LastName)
             FROM SchoolEntities.People AS p
             WHERE p.LastName &gt;= somestring
   </DefiningExpression>
 </Function>
```
 

 

## <a name="propertyref-element-csdl"></a><span data-ttu-id="9a003-929">PropertyRef 元素 (CSDL)</span><span class="sxs-lookup"><span data-stu-id="9a003-929">PropertyRef Element (CSDL)</span></span>

<span data-ttu-id="9a003-930">**PropertyRef**概念架构定义语言 (CSDL) 中的元素引用的实体类型，以指示该属性将承担以下角色之一的属性：</span><span class="sxs-lookup"><span data-stu-id="9a003-930">The **PropertyRef** element in conceptual schema definition language (CSDL) references a property of an entity type to indicate that the property will perform one of the following roles:</span></span>

-   <span data-ttu-id="9a003-931">实体键的一部分（实体类型的用于确定标识的一个或一组属性）。</span><span class="sxs-lookup"><span data-stu-id="9a003-931">Part of the entity's key (a property or a set of properties of an entity type that determine identity).</span></span> <span data-ttu-id="9a003-932">一个或多个**PropertyRef**元素可用于定义实体键。</span><span class="sxs-lookup"><span data-stu-id="9a003-932">One or more **PropertyRef** elements can be used to define an entity key.</span></span>
-   <span data-ttu-id="9a003-933">引用约束的依赖端或主体端。</span><span class="sxs-lookup"><span data-stu-id="9a003-933">The dependent or principal end of a referential constraint.</span></span>

<span data-ttu-id="9a003-934">**PropertyRef**元素只能具有批注元素 （零个或多个） 作为子元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-934">The **PropertyRef** element can only have annotation elements (zero or more) as child elements.</span></span>

> [!NOTE]
> <span data-ttu-id="9a003-935">批注元素只能在 CSDL v2 和更高版本。</span><span class="sxs-lookup"><span data-stu-id="9a003-935">Annotation elements are only allowed in CSDL v2 and later.</span></span>

 

### <a name="applicable-attributes"></a><span data-ttu-id="9a003-936">适用的特性</span><span class="sxs-lookup"><span data-stu-id="9a003-936">Applicable Attributes</span></span>

<span data-ttu-id="9a003-937">下表描述了可应用于的特性**PropertyRef**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-937">The table below describes the attributes that can be applied to the **PropertyRef** element.</span></span>

| <span data-ttu-id="9a003-938">特性名</span><span class="sxs-lookup"><span data-stu-id="9a003-938">Attribute Name</span></span> | <span data-ttu-id="9a003-939">是否必需</span><span class="sxs-lookup"><span data-stu-id="9a003-939">Is Required</span></span> | <span data-ttu-id="9a003-940">“值”</span><span class="sxs-lookup"><span data-stu-id="9a003-940">Value</span></span>                                |
|:---------------|:------------|:-------------------------------------|
| <span data-ttu-id="9a003-941">**名称**</span><span class="sxs-lookup"><span data-stu-id="9a003-941">**Name**</span></span>       | <span data-ttu-id="9a003-942">是</span><span class="sxs-lookup"><span data-stu-id="9a003-942">Yes</span></span>         | <span data-ttu-id="9a003-943">所引用属性的名称。</span><span class="sxs-lookup"><span data-stu-id="9a003-943">The name of the referenced property.</span></span> |

 

> [!NOTE]
> <span data-ttu-id="9a003-944">可以将任意数量的 （自定义 XML 特性） 的批注特性应用于**PropertyRef**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-944">Any number of annotation attributes (custom XML attributes) may be applied to the **PropertyRef** element.</span></span> <span data-ttu-id="9a003-945">然而，自定义特性可能不属于为 CSDL 保留的任何 XML 命名空间。</span><span class="sxs-lookup"><span data-stu-id="9a003-945">However, custom attributes may not belong to any XML namespace that is reserved for CSDL.</span></span> <span data-ttu-id="9a003-946">任何两个自定义特性的完全限定名称都不能相同。</span><span class="sxs-lookup"><span data-stu-id="9a003-946">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

 

### <a name="example"></a><span data-ttu-id="9a003-947">示例</span><span class="sxs-lookup"><span data-stu-id="9a003-947">Example</span></span>

<span data-ttu-id="9a003-948">下面的示例定义一个实体类型 (**通讯簿**)。</span><span class="sxs-lookup"><span data-stu-id="9a003-948">The example below defines an entity type (**Book**).</span></span> <span data-ttu-id="9a003-949">通过引用来定义实体键**ISBN**实体类型的属性。</span><span class="sxs-lookup"><span data-stu-id="9a003-949">The entity key is defined by referencing the **ISBN** property of the entity type.</span></span>

``` xml
 <EntityType Name="Book">
   <Key>
     <PropertyRef Name="ISBN" />
   </Key>
   <Property Type="String" Name="ISBN" Nullable="false" />
   <Property Type="String" Name="Title" Nullable="false" />
   <Property Type="Decimal" Name="Revision" Nullable="false" Precision="29" Scale="29" />
   <NavigationProperty Name="Publisher" Relationship="BooksModel.PublishedBy"
                       FromRole="Book" ToRole="Publisher" />
   <NavigationProperty Name="Authors" Relationship="BooksModel.WrittenBy"
                       FromRole="Book" ToRole="Author" />
 </EntityType>
```
 

<span data-ttu-id="9a003-950">在下一步的示例中，两个**PropertyRef**元素用于指示两个属性 (**Id**并**PublisherId**) 是主体端和依赖端引用约束。</span><span class="sxs-lookup"><span data-stu-id="9a003-950">In the next example, two **PropertyRef** elements are used to indicate that two properties (**Id** and **PublisherId**) are the principal and dependent ends of a referential constraint.</span></span>

``` xml
 <Association Name="PublishedBy">
   <End Type="BooksModel.Book" Role="Book" Multiplicity="*" >
   </End>
   <End Type="BooksModel.Publisher" Role="Publisher" Multiplicity="1" />
   <ReferentialConstraint>
     <Principal Role="Publisher">
       <PropertyRef Name="Id" />
     </Principal>
     <Dependent Role="Book">
       <PropertyRef Name="PublisherId" />
     </Dependent>
   </ReferentialConstraint>
 </Association>
```
 

 

## <a name="referencetype-element-csdl"></a><span data-ttu-id="9a003-951">ReferenceType 元素 (CSDL)</span><span class="sxs-lookup"><span data-stu-id="9a003-951">ReferenceType Element (CSDL)</span></span>

<span data-ttu-id="9a003-952">**ReferenceType**概念架构定义语言 (CSDL) 中的元素指定对实体类型的引用。</span><span class="sxs-lookup"><span data-stu-id="9a003-952">The **ReferenceType** element in conceptual schema definition language (CSDL) specifies a reference to an entity type.</span></span> <span data-ttu-id="9a003-953">**ReferenceType**元素可以是以下元素的子元素：</span><span class="sxs-lookup"><span data-stu-id="9a003-953">The **ReferenceType** element can be a child of the following elements:</span></span>

-   <span data-ttu-id="9a003-954">ReturnType （函数）</span><span class="sxs-lookup"><span data-stu-id="9a003-954">ReturnType (Function)</span></span>
-   <span data-ttu-id="9a003-955">参数</span><span class="sxs-lookup"><span data-stu-id="9a003-955">Parameter</span></span>
-   <span data-ttu-id="9a003-956">CollectionType</span><span class="sxs-lookup"><span data-stu-id="9a003-956">CollectionType</span></span>

<span data-ttu-id="9a003-957">**ReferenceType**元素定义的函数的参数或返回类型时使用。</span><span class="sxs-lookup"><span data-stu-id="9a003-957">The **ReferenceType** element is used when defining a parameter or return type for a function.</span></span>

<span data-ttu-id="9a003-958">一个**ReferenceType**元素可以具有下列子元素 （按所列顺序）：</span><span class="sxs-lookup"><span data-stu-id="9a003-958">A **ReferenceType** element can have the following child elements (in the order listed):</span></span>

-   <span data-ttu-id="9a003-959">文档 （零个或一个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-959">Documentation (zero or one element)</span></span>
-   <span data-ttu-id="9a003-960">批注元素 （零个或多个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-960">Annotation elements (zero or more elements)</span></span>

### <a name="applicable-attributes"></a><span data-ttu-id="9a003-961">适用的特性</span><span class="sxs-lookup"><span data-stu-id="9a003-961">Applicable Attributes</span></span>

<span data-ttu-id="9a003-962">下表描述了可应用于的特性**ReferenceType**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-962">The table below describes the attributes that can be applied to the **ReferenceType** element.</span></span>

| <span data-ttu-id="9a003-963">特性名</span><span class="sxs-lookup"><span data-stu-id="9a003-963">Attribute Name</span></span> | <span data-ttu-id="9a003-964">是否必需</span><span class="sxs-lookup"><span data-stu-id="9a003-964">Is Required</span></span> | <span data-ttu-id="9a003-965">“值”</span><span class="sxs-lookup"><span data-stu-id="9a003-965">Value</span></span>                                         |
|:---------------|:------------|:----------------------------------------------|
| <span data-ttu-id="9a003-966">**Type**</span><span class="sxs-lookup"><span data-stu-id="9a003-966">**Type**</span></span>       | <span data-ttu-id="9a003-967">是</span><span class="sxs-lookup"><span data-stu-id="9a003-967">Yes</span></span>         | <span data-ttu-id="9a003-968">所引用的实体类型的名称。</span><span class="sxs-lookup"><span data-stu-id="9a003-968">The name of the entity type being referenced.</span></span> |

 

> [!NOTE]
> <span data-ttu-id="9a003-969">可以将任意数量的 （自定义 XML 特性） 的批注特性应用于**ReferenceType**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-969">Any number of annotation attributes (custom XML attributes) may be applied to the **ReferenceType** element.</span></span> <span data-ttu-id="9a003-970">然而，自定义特性可能不属于为 CSDL 保留的任何 XML 命名空间。</span><span class="sxs-lookup"><span data-stu-id="9a003-970">However, custom attributes may not belong to any XML namespace that is reserved for CSDL.</span></span> <span data-ttu-id="9a003-971">任何两个自定义特性的完全限定名称都不能相同。</span><span class="sxs-lookup"><span data-stu-id="9a003-971">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

 

### <a name="example"></a><span data-ttu-id="9a003-972">示例</span><span class="sxs-lookup"><span data-stu-id="9a003-972">Example</span></span>

<span data-ttu-id="9a003-973">下面的示例演示**ReferenceType**元素的小孩在用**参数**接受对引用的模型定义函数中的元素**人员**实体类型：</span><span class="sxs-lookup"><span data-stu-id="9a003-973">The following example shows the **ReferenceType** element used as a child of a **Parameter** element in a model-defined function that accepts a reference to a **Person** entity type:</span></span>

``` xml
 <Function Name="GetYearsEmployed" ReturnType="Edm.Int32">
   <Parameter Name="instructor">
     <ReferenceType Type="SchoolModel.Person" />
   </Parameter>
   <DefiningExpression>
   Year(CurrentDateTime()) - Year(cast(instructor.HireDate as DateTime))
   </DefiningExpression>
 </Function>
```
 

<span data-ttu-id="9a003-974">下面的示例演示**ReferenceType**元素的小孩在用**ReturnType**中返回的引用的模型定义函数 （函数） 元素**人员**实体类型：</span><span class="sxs-lookup"><span data-stu-id="9a003-974">The following example shows the **ReferenceType** element used as a child of a **ReturnType** (Function) element in a model-defined function that returns a reference to a **Person** entity type:</span></span>

``` xml
 <Function Name="GetPersonReference">
     <Parameter Name="p" Type="SchoolModel.Person" />
     <ReturnType>
         <ReferenceType Type="SchoolModel.Person" />
     </ReturnType>
     <DefiningExpression>
           REF(p)
     </DefiningExpression>
 </Function>
```
 

 

## <a name="referentialconstraint-element-csdl"></a><span data-ttu-id="9a003-975">ReferentialConstraint 元素 (CSDL)</span><span class="sxs-lookup"><span data-stu-id="9a003-975">ReferentialConstraint Element (CSDL)</span></span>

<span data-ttu-id="9a003-976">一个**ReferentialConstraint**概念架构定义语言 (CSDL) 中的元素定义的是关系数据库中的引用完整性约束类似的功能。</span><span class="sxs-lookup"><span data-stu-id="9a003-976">A **ReferentialConstraint** element in conceptual schema definition language (CSDL) defines functionality that is similar to a referential integrity constraint in a relational database.</span></span> <span data-ttu-id="9a003-977">与数据库表中的一个（或多个）列可以引用另一个表的主键相同，实体类型的一个（或多个）属性可以引用另一个实体类型的实体键。</span><span class="sxs-lookup"><span data-stu-id="9a003-977">In the same way that a column (or columns) from a database table can reference the primary key of another table, a property (or properties) of an entity type can reference the entity key of another entity type.</span></span> <span data-ttu-id="9a003-978">引用的实体类型称为*主体端*的约束。</span><span class="sxs-lookup"><span data-stu-id="9a003-978">The entity type that is referenced is called the *principal end* of the constraint.</span></span> <span data-ttu-id="9a003-979">引用主体端的实体类型称为*依赖端*的约束。</span><span class="sxs-lookup"><span data-stu-id="9a003-979">The entity type that references the principal end is called the *dependent end* of the constraint.</span></span>

<span data-ttu-id="9a003-980">如果一个实体类型公开的外键引用另一个实体类型上的属性**ReferentialConstraint**元素定义两个实体类型之间的关联。</span><span class="sxs-lookup"><span data-stu-id="9a003-980">If a foreign key that is exposed on one entity type references a property on another entity type, the **ReferentialConstraint** element defines an association between the two entity types.</span></span> <span data-ttu-id="9a003-981">因为**ReferentialConstraint**元素提供了两个实体类型的信息相关的没有相应的 AssociationSetMapping 元素是有必要在映射规范语言 (MSL)。</span><span class="sxs-lookup"><span data-stu-id="9a003-981">Because the **ReferentialConstraint** element provides information about how two entity types are related, no corresponding AssociationSetMapping element is necessary in the mapping specification language (MSL).</span></span> <span data-ttu-id="9a003-982">没有公开外键的两个实体类型之间的关联必须具有相应**AssociationSetMapping**元素中，以便将关联信息映射到数据源。</span><span class="sxs-lookup"><span data-stu-id="9a003-982">An association between two entity types that do not have foreign keys exposed must have a corresponding **AssociationSetMapping** element in order to map association information to the data source.</span></span>

<span data-ttu-id="9a003-983">如果一个实体类型，不会公开的外键**ReferentialConstraint**元素只能定义实体类型与另一个实体类型之间的主要键到主键键约束。</span><span class="sxs-lookup"><span data-stu-id="9a003-983">If a foreign key is not exposed on an entity type, the **ReferentialConstraint** element can only define a primary key-to-primary key constraint between the entity type and another entity type.</span></span>

<span data-ttu-id="9a003-984">一个**ReferentialConstraint**元素可以具有下列子元素 （按所列顺序）：</span><span class="sxs-lookup"><span data-stu-id="9a003-984">A **ReferentialConstraint** element can have the following child elements (in the order listed):</span></span>

-   <span data-ttu-id="9a003-985">文档 （零个或一个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-985">Documentation (zero or one element)</span></span>
-   <span data-ttu-id="9a003-986">主体 （恰好一个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-986">Principal (exactly one element)</span></span>
-   <span data-ttu-id="9a003-987">依赖于 （恰好一个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-987">Dependent (exactly one element)</span></span>
-   <span data-ttu-id="9a003-988">批注元素 （零个或多个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-988">Annotation elements (zero or more elements)</span></span>

### <a name="applicable-attributes"></a><span data-ttu-id="9a003-989">适用的特性</span><span class="sxs-lookup"><span data-stu-id="9a003-989">Applicable Attributes</span></span>

<span data-ttu-id="9a003-990">**ReferentialConstraint**元素可以具有任意数量的批注特性 （自定义 XML 特性）。</span><span class="sxs-lookup"><span data-stu-id="9a003-990">The **ReferentialConstraint** element can have any number of annotation attributes (custom XML attributes).</span></span> <span data-ttu-id="9a003-991">然而，自定义特性可能不属于为 CSDL 保留的任何 XML 命名空间。</span><span class="sxs-lookup"><span data-stu-id="9a003-991">However, custom attributes may not belong to any XML namespace that is reserved for CSDL.</span></span> <span data-ttu-id="9a003-992">任何两个自定义特性的完全限定名称都不能相同。</span><span class="sxs-lookup"><span data-stu-id="9a003-992">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

### <a name="example"></a><span data-ttu-id="9a003-993">示例</span><span class="sxs-lookup"><span data-stu-id="9a003-993">Example</span></span>

<span data-ttu-id="9a003-994">下面的示例演示**ReferentialConstraint**元素的定义的一部分用作**PublishedBy**关联。</span><span class="sxs-lookup"><span data-stu-id="9a003-994">The following example shows a **ReferentialConstraint** element being used as part of the definition of the **PublishedBy** association.</span></span>

``` xml
 <Association Name="PublishedBy">
   <End Type="BooksModel.Book" Role="Book" Multiplicity="*" >
   </End>
   <End Type="BooksModel.Publisher" Role="Publisher" Multiplicity="1" />
   <ReferentialConstraint>
     <Principal Role="Publisher">
       <PropertyRef Name="Id" />
     </Principal>
     <Dependent Role="Book">
       <PropertyRef Name="PublisherId" />
     </Dependent>
   </ReferentialConstraint>
 </Association>
```
 

 

## <a name="returntype-function-element-csdl"></a><span data-ttu-id="9a003-995">ReturnType （函数） 元素 (CSDL)</span><span class="sxs-lookup"><span data-stu-id="9a003-995">ReturnType (Function) Element (CSDL)</span></span>

<span data-ttu-id="9a003-996">**ReturnType** （函数） 在概念性架构定义语言 (CSDL) 中的元素指定函数元素中定义的函数的返回类型。</span><span class="sxs-lookup"><span data-stu-id="9a003-996">The **ReturnType** (Function) element in conceptual schema definition language (CSDL) specifies the return type for a function that is defined in a Function element.</span></span> <span data-ttu-id="9a003-997">此外可以使用指定返回类型的函数**ReturnType**属性。</span><span class="sxs-lookup"><span data-stu-id="9a003-997">A function return type can also be specified with a **ReturnType** attribute.</span></span>

<span data-ttu-id="9a003-998">返回类型可以是任意**EdmSimpleType**，实体类型、 复杂类型、 行类型、 ref 类型或其中一种类型的集合。</span><span class="sxs-lookup"><span data-stu-id="9a003-998">Return types can be any **EdmSimpleType**, entity type, complex type, row type, ref type, or a collection of one of these types.</span></span>

<span data-ttu-id="9a003-999">可以通过指定函数的返回类型**类型**的属性**ReturnType** （函数） 元素，或使用以下子元素之一：</span><span class="sxs-lookup"><span data-stu-id="9a003-999">The return type of a function can be specified with either the **Type** attribute of the **ReturnType** (Function) element, or with one of the following child elements:</span></span>

-   <span data-ttu-id="9a003-1000">CollectionType</span><span class="sxs-lookup"><span data-stu-id="9a003-1000">CollectionType</span></span>
-   <span data-ttu-id="9a003-1001">ReferenceType</span><span class="sxs-lookup"><span data-stu-id="9a003-1001">ReferenceType</span></span>
-   <span data-ttu-id="9a003-1002">RowType</span><span class="sxs-lookup"><span data-stu-id="9a003-1002">RowType</span></span>

> [!NOTE]
> <span data-ttu-id="9a003-1003">如果您指定的函数返回类型同时具有无法验证模型**类型**的属性**ReturnType** （函数） 元素和子元素之一。</span><span class="sxs-lookup"><span data-stu-id="9a003-1003">A model will not validate if you specify a function return type with both the **Type** attribute of the **ReturnType** (Function) element and one of the child elements.</span></span>

 

### <a name="applicable-attributes"></a><span data-ttu-id="9a003-1004">适用的特性</span><span class="sxs-lookup"><span data-stu-id="9a003-1004">Applicable Attributes</span></span>

<span data-ttu-id="9a003-1005">下表介绍可应用于的特性**ReturnType** （函数） 元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-1005">The following table describes the attributes that can be applied to the **ReturnType** (Function) element.</span></span>

| <span data-ttu-id="9a003-1006">特性名</span><span class="sxs-lookup"><span data-stu-id="9a003-1006">Attribute Name</span></span> | <span data-ttu-id="9a003-1007">是否必需</span><span class="sxs-lookup"><span data-stu-id="9a003-1007">Is Required</span></span> | <span data-ttu-id="9a003-1008">“值”</span><span class="sxs-lookup"><span data-stu-id="9a003-1008">Value</span></span>                              |
|:---------------|:------------|:-----------------------------------|
| <span data-ttu-id="9a003-1009">**ReturnType**</span><span class="sxs-lookup"><span data-stu-id="9a003-1009">**ReturnType**</span></span> | <span data-ttu-id="9a003-1010">否</span><span class="sxs-lookup"><span data-stu-id="9a003-1010">No</span></span>          | <span data-ttu-id="9a003-1011">函数返回的类型。</span><span class="sxs-lookup"><span data-stu-id="9a003-1011">The type returned by the function.</span></span> |

 

> [!NOTE]
> <span data-ttu-id="9a003-1012">可以将任意数量的 （自定义 XML 特性） 的批注特性应用于**ReturnType** （函数） 元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-1012">Any number of annotation attributes (custom XML attributes) may be applied to the **ReturnType** (Function) element.</span></span> <span data-ttu-id="9a003-1013">然而，自定义特性可能不属于为 CSDL 保留的任何 XML 命名空间。</span><span class="sxs-lookup"><span data-stu-id="9a003-1013">However, custom attributes may not belong to any XML namespace that is reserved for CSDL.</span></span> <span data-ttu-id="9a003-1014">任何两个自定义特性的完全限定名称都不能相同。</span><span class="sxs-lookup"><span data-stu-id="9a003-1014">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

 

### <a name="example"></a><span data-ttu-id="9a003-1015">示例</span><span class="sxs-lookup"><span data-stu-id="9a003-1015">Example</span></span>

<span data-ttu-id="9a003-1016">下面的示例使用**函数**元素来定义返回某书籍已在打印中的年数的函数。</span><span class="sxs-lookup"><span data-stu-id="9a003-1016">The following example uses a **Function** element to define a function that returns the number of years a book has been in print.</span></span> <span data-ttu-id="9a003-1017">请注意，通过指定的返回类型**类型**的属性**ReturnType** （函数） 元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-1017">Note that the return type is specified by the **Type** attribute of a **ReturnType** (Function) element.</span></span>

``` xml
 <Function Name="GetYearsInPrint">
   <ReturnType Type=="Edm.Int32">
   <Parameter Name="book" Type="BooksModel.Book" />
   <DefiningExpression>
    Year(CurrentDateTime()) - Year(cast(book.PublishedDate as DateTime))
   </DefiningExpression>
 </Function>
```
 

 

## <a name="returntype-functionimport-element-csdl"></a><span data-ttu-id="9a003-1018">ReturnType (FunctionImport) 元素 (CSDL)</span><span class="sxs-lookup"><span data-stu-id="9a003-1018">ReturnType (FunctionImport) Element (CSDL)</span></span>

<span data-ttu-id="9a003-1019">**ReturnType** (FunctionImport) 元素在概念架构定义语言 (CSDL) 中的指定的 FunctionImport 元素中定义的函数的返回类型。</span><span class="sxs-lookup"><span data-stu-id="9a003-1019">The **ReturnType** (FunctionImport) element in conceptual schema definition language (CSDL) specifies the return type for a function that is defined in a FunctionImport element.</span></span> <span data-ttu-id="9a003-1020">此外可以使用指定返回类型的函数**ReturnType**属性。</span><span class="sxs-lookup"><span data-stu-id="9a003-1020">A function return type can also be specified with a **ReturnType** attribute.</span></span>

<span data-ttu-id="9a003-1021">返回类型可以是实体类型、 复杂类型的任何集合或**EdmSimpleType**，</span><span class="sxs-lookup"><span data-stu-id="9a003-1021">Return types can be any collection of entity type, complex type,or **EdmSimpleType**,</span></span>

<span data-ttu-id="9a003-1022">使用指定函数的返回类型**类型**的属性**ReturnType** (FunctionImport) 元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-1022">The return type of a function is specified with the **Type** attribute of the **ReturnType** (FunctionImport) element.</span></span>

### <a name="applicable-attributes"></a><span data-ttu-id="9a003-1023">适用的特性</span><span class="sxs-lookup"><span data-stu-id="9a003-1023">Applicable Attributes</span></span>

<span data-ttu-id="9a003-1024">下表介绍可应用于的特性**ReturnType** (FunctionImport) 元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-1024">The following table describes the attributes that can be applied to the **ReturnType** (FunctionImport) element.</span></span>

| <span data-ttu-id="9a003-1025">特性名</span><span class="sxs-lookup"><span data-stu-id="9a003-1025">Attribute Name</span></span> | <span data-ttu-id="9a003-1026">是否必需</span><span class="sxs-lookup"><span data-stu-id="9a003-1026">Is Required</span></span> | <span data-ttu-id="9a003-1027">“值”</span><span class="sxs-lookup"><span data-stu-id="9a003-1027">Value</span></span>                                                                                                                                                                                                 |
|:---------------|:------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9a003-1028">**Type**</span><span class="sxs-lookup"><span data-stu-id="9a003-1028">**Type**</span></span>       | <span data-ttu-id="9a003-1029">否</span><span class="sxs-lookup"><span data-stu-id="9a003-1029">No</span></span>          | <span data-ttu-id="9a003-1030">函数返回的类型。</span><span class="sxs-lookup"><span data-stu-id="9a003-1030">The type that the function returns.</span></span> <span data-ttu-id="9a003-1031">值必须是 ComplexType、 EntityType 或 EDMSimpleType 的集合。</span><span class="sxs-lookup"><span data-stu-id="9a003-1031">The value must be a collection of ComplexType, EntityType, or EDMSimpleType.</span></span>                                                                                      |
| <span data-ttu-id="9a003-1032">**实体集**</span><span class="sxs-lookup"><span data-stu-id="9a003-1032">**EntitySet**</span></span>  | <span data-ttu-id="9a003-1033">否</span><span class="sxs-lookup"><span data-stu-id="9a003-1033">No</span></span>          | <span data-ttu-id="9a003-1034">如果该函数返回的实体集合类型，值**EntitySet**必须将实体设置为该集合所属。</span><span class="sxs-lookup"><span data-stu-id="9a003-1034">If the function returns a collection of entity types, the value of the **EntitySet** must be the entity set to which the collection belongs.</span></span> <span data-ttu-id="9a003-1035">否则为**EntitySet**属性不能使用。</span><span class="sxs-lookup"><span data-stu-id="9a003-1035">Otherwise, the **EntitySet** attribute must not be used.</span></span> |

 

> [!NOTE]
> <span data-ttu-id="9a003-1036">可以将任意数量的 （自定义 XML 特性） 的批注特性应用于**ReturnType** (FunctionImport) 元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-1036">Any number of annotation attributes (custom XML attributes) may be applied to the **ReturnType** (FunctionImport) element.</span></span> <span data-ttu-id="9a003-1037">然而，自定义特性可能不属于为 CSDL 保留的任何 XML 命名空间。</span><span class="sxs-lookup"><span data-stu-id="9a003-1037">However, custom attributes may not belong to any XML namespace that is reserved for CSDL.</span></span> <span data-ttu-id="9a003-1038">任何两个自定义特性的完全限定名称都不能相同。</span><span class="sxs-lookup"><span data-stu-id="9a003-1038">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

 

### <a name="example"></a><span data-ttu-id="9a003-1039">示例</span><span class="sxs-lookup"><span data-stu-id="9a003-1039">Example</span></span>

<span data-ttu-id="9a003-1040">下面的示例使用**FunctionImport**返回书籍和发布服务器。</span><span class="sxs-lookup"><span data-stu-id="9a003-1040">The following example uses a **FunctionImport** that returns books and publishers.</span></span> <span data-ttu-id="9a003-1041">请注意，该函数返回两个结果集，因此两个**ReturnType**指定了 (FunctionImport) 元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-1041">Note that the function returns two result sets and therefore two **ReturnType** (FunctionImport) elements are specified.</span></span>

``` xml
 <FunctionImport Name="GetBooksAndPublishers">
   <ReturnType Type=="Collection(BooksModel.Book )" EntitySet=”Books”>
   <ReturnType Type=="Collection(BooksModel.Publisher)" EntitySet=”Publishers”>
 </FunctionImport>
```
 

 

## <a name="rowtype-element-csdl"></a><span data-ttu-id="9a003-1042">RowType 元素 (CSDL)</span><span class="sxs-lookup"><span data-stu-id="9a003-1042">RowType Element (CSDL)</span></span>

<span data-ttu-id="9a003-1043">一个**RowType**概念架构定义语言 (CSDL) 中的元素定义未命名的结构作为参数或返回类型的概念模型中定义的函数。</span><span class="sxs-lookup"><span data-stu-id="9a003-1043">A **RowType** element in conceptual schema definition language (CSDL) defines an unnamed structure as a parameter or return type for a function defined in the conceptual model.</span></span>

<span data-ttu-id="9a003-1044">一个**RowType**元素可以是以下元素的子级：</span><span class="sxs-lookup"><span data-stu-id="9a003-1044">A **RowType** element can be the child of the following elements:</span></span>

-   <span data-ttu-id="9a003-1045">CollectionType</span><span class="sxs-lookup"><span data-stu-id="9a003-1045">CollectionType</span></span>
-   <span data-ttu-id="9a003-1046">参数</span><span class="sxs-lookup"><span data-stu-id="9a003-1046">Parameter</span></span>
-   <span data-ttu-id="9a003-1047">ReturnType （函数）</span><span class="sxs-lookup"><span data-stu-id="9a003-1047">ReturnType (Function)</span></span>

<span data-ttu-id="9a003-1048">一个**RowType**元素可以具有下列子元素 （按所列顺序）：</span><span class="sxs-lookup"><span data-stu-id="9a003-1048">A **RowType** element can have the following child elements (in the order listed):</span></span>

-   <span data-ttu-id="9a003-1049">属性 （一个或多个）</span><span class="sxs-lookup"><span data-stu-id="9a003-1049">Property (one or more)</span></span>
-   <span data-ttu-id="9a003-1050">批注元素 （零个或多个）</span><span class="sxs-lookup"><span data-stu-id="9a003-1050">Annotation elements (zero or more)</span></span>

### <a name="applicable-attributes"></a><span data-ttu-id="9a003-1051">适用的特性</span><span class="sxs-lookup"><span data-stu-id="9a003-1051">Applicable Attributes</span></span>

<span data-ttu-id="9a003-1052">可以将任意数量的 （自定义 XML 特性） 的批注特性应用于**RowType**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-1052">Any number of annotation attributes (custom XML attributes) may be applied to the **RowType** element.</span></span> <span data-ttu-id="9a003-1053">然而，自定义特性可能不属于为 CSDL 保留的任何 XML 命名空间。</span><span class="sxs-lookup"><span data-stu-id="9a003-1053">However, custom attributes may not belong to any XML namespace that is reserved for CSDL.</span></span> <span data-ttu-id="9a003-1054">任何两个自定义特性的完全限定名称都不能相同。</span><span class="sxs-lookup"><span data-stu-id="9a003-1054">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

### <a name="example"></a><span data-ttu-id="9a003-1055">示例</span><span class="sxs-lookup"><span data-stu-id="9a003-1055">Example</span></span>

<span data-ttu-id="9a003-1056">下面的示例演示使用的模型定义函数**CollectionType**元素来指定该函数返回的行集合 (中指定的那样**RowType**元素)。</span><span class="sxs-lookup"><span data-stu-id="9a003-1056">The following example shows a model-defined function that uses a **CollectionType** element to specify that the function returns a collection of rows (as specified in the **RowType** element).</span></span>

``` xml
 <Function Name="LastNamesAfter">
   <Parameter Name="someString" Type="Edm.String" />
   <ReturnType>
    <CollectionType>
      <RowType>
        <Property Name="FirstName" Type="Edm.String" Nullable="false" />
        <Property Name="LastName" Type="Edm.String" Nullable="false" />
      </RowType>
    </CollectionType>
   </ReturnType>
   <DefiningExpression>
             SELECT VALUE ROW(p.FirstName, p.LastName)
             FROM SchoolEntities.People AS p
             WHERE p.LastName &gt;= somestring
   </DefiningExpression>
 </Function>
```

## <a name="schema-element-csdl"></a><span data-ttu-id="9a003-1057">Schema 元素 (CSDL)</span><span class="sxs-lookup"><span data-stu-id="9a003-1057">Schema Element (CSDL)</span></span>

<span data-ttu-id="9a003-1058">**架构**元素是概念模型定义的根元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-1058">The **Schema** element is the root element of a conceptual model definition.</span></span> <span data-ttu-id="9a003-1059">它包括构成概念模型的对象、函数和容器的定义。</span><span class="sxs-lookup"><span data-stu-id="9a003-1059">It contains definitions for the objects, functions, and containers that make up a conceptual model.</span></span>

<span data-ttu-id="9a003-1060">**架构**元素可能包含零个或多个下列子元素：</span><span class="sxs-lookup"><span data-stu-id="9a003-1060">The **Schema** element may contain zero or more of the following child elements:</span></span>

-   <span data-ttu-id="9a003-1061">Using</span><span class="sxs-lookup"><span data-stu-id="9a003-1061">Using</span></span>
-   <span data-ttu-id="9a003-1062">EntityContainer</span><span class="sxs-lookup"><span data-stu-id="9a003-1062">EntityContainer</span></span>
-   <span data-ttu-id="9a003-1063">EntityType</span><span class="sxs-lookup"><span data-stu-id="9a003-1063">EntityType</span></span>
-   <span data-ttu-id="9a003-1064">EnumType</span><span class="sxs-lookup"><span data-stu-id="9a003-1064">EnumType</span></span>
-   <span data-ttu-id="9a003-1065">关联</span><span class="sxs-lookup"><span data-stu-id="9a003-1065">Association</span></span>
-   <span data-ttu-id="9a003-1066">ComplexType</span><span class="sxs-lookup"><span data-stu-id="9a003-1066">ComplexType</span></span>
-   <span data-ttu-id="9a003-1067">函数</span><span class="sxs-lookup"><span data-stu-id="9a003-1067">Function</span></span>

<span data-ttu-id="9a003-1068">一个**架构**元素可能包含零个或一个批注元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-1068">A **Schema** element may contain zero or one Annotation elements.</span></span>

> [!NOTE]
> <span data-ttu-id="9a003-1069">**函数**元素和批注元素只能在 CSDL v2 和更高版本。</span><span class="sxs-lookup"><span data-stu-id="9a003-1069">The **Function** element and annotation elements are only allowed in CSDL v2 and later.</span></span>

 

<span data-ttu-id="9a003-1070">**架构**元素使用**Namespace**属性来定义概念模型中的实体类型、 复杂类型和关联对象的命名空间。</span><span class="sxs-lookup"><span data-stu-id="9a003-1070">The **Schema** element uses the **Namespace** attribute to define the namespace for the entity type, complex type, and association objects in a conceptual model.</span></span> <span data-ttu-id="9a003-1071">在命名空间内，任何两个对象都不能同名。</span><span class="sxs-lookup"><span data-stu-id="9a003-1071">Within a namespace, no two objects can have the same name.</span></span> <span data-ttu-id="9a003-1072">命名空间可以跨多个**架构**元素和多个.csdl 文件。</span><span class="sxs-lookup"><span data-stu-id="9a003-1072">Namespaces can span multiple **Schema** elements and multiple .csdl files.</span></span>

<span data-ttu-id="9a003-1073">概念模型命名空间是不同的 XML 命名空间**架构**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-1073">A conceptual model namespace is different from the XML namespace of the **Schema** element.</span></span> <span data-ttu-id="9a003-1074">概念模型命名空间 (由定义**Namespace**属性) 是实体类型、 复杂类型和关联类型的逻辑容器。</span><span class="sxs-lookup"><span data-stu-id="9a003-1074">A conceptual model namespace (as defined by the **Namespace** attribute) is a logical container for entity types, complex types, and association types.</span></span> <span data-ttu-id="9a003-1075">XML 命名空间 (由**xmlns**属性) 的**架构**元素是子元素和属性的默认命名空间**架构**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-1075">The XML namespace (indicated by the **xmlns** attribute) of a **Schema** element is the default namespace for child elements and attributes of the **Schema** element.</span></span> <span data-ttu-id="9a003-1076">窗体的 XML 命名空间 http://schemas.microsoft.com/ado/YYYY/MM/edm （其中 YYYY 和 MM 表示年和月分别） 是为 CSDL 保留。</span><span class="sxs-lookup"><span data-stu-id="9a003-1076">XML namespaces of the form http://schemas.microsoft.com/ado/YYYY/MM/edm (where YYYY and MM represent a year and month respectively) are reserved for CSDL.</span></span> <span data-ttu-id="9a003-1077">自定义元素和特性不能位于具有此格式的命名空间中。</span><span class="sxs-lookup"><span data-stu-id="9a003-1077">Custom elements and attributes cannot be in namespaces that have this form.</span></span>

### <a name="applicable-attributes"></a><span data-ttu-id="9a003-1078">适用的特性</span><span class="sxs-lookup"><span data-stu-id="9a003-1078">Applicable Attributes</span></span>

<span data-ttu-id="9a003-1079">下表描述了特性可应用于**架构**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-1079">The table below describes the attributes can be applied to the **Schema** element.</span></span>

| <span data-ttu-id="9a003-1080">特性名</span><span class="sxs-lookup"><span data-stu-id="9a003-1080">Attribute Name</span></span> | <span data-ttu-id="9a003-1081">是否必需</span><span class="sxs-lookup"><span data-stu-id="9a003-1081">Is Required</span></span> | <span data-ttu-id="9a003-1082">“值”</span><span class="sxs-lookup"><span data-stu-id="9a003-1082">Value</span></span>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
|:---------------|:------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9a003-1083">**命名空间**</span><span class="sxs-lookup"><span data-stu-id="9a003-1083">**Namespace**</span></span>  | <span data-ttu-id="9a003-1084">是</span><span class="sxs-lookup"><span data-stu-id="9a003-1084">Yes</span></span>         | <span data-ttu-id="9a003-1085">概念模型的命名空间。</span><span class="sxs-lookup"><span data-stu-id="9a003-1085">The namespace of the conceptual model.</span></span> <span data-ttu-id="9a003-1086">值**Namespace**特性用于形成一种类型的完全限定的名称。</span><span class="sxs-lookup"><span data-stu-id="9a003-1086">The value of the **Namespace** attribute is used to form the fully qualified name of a type.</span></span> <span data-ttu-id="9a003-1087">例如，如果**EntityType**名为*客户*位于 Simple.Example.Model 命名空间，则完全限定的名称**EntityType**是SimpleExampleModel.Customer。</span><span class="sxs-lookup"><span data-stu-id="9a003-1087">For example, if an **EntityType** named *Customer* is in the Simple.Example.Model namespace, then the fully qualified name of the **EntityType** is SimpleExampleModel.Customer.</span></span> <br/> <span data-ttu-id="9a003-1088">以下字符串不能使用的值作为**Namespace**属性：**系统**，**暂时性**，或者**Edm**。</span><span class="sxs-lookup"><span data-stu-id="9a003-1088">The following strings cannot be used as the value for the **Namespace** attribute: **System**, **Transient**, or **Edm**.</span></span> <span data-ttu-id="9a003-1089">值**Namespace**属性不能与的值相同**Namespace** SSDL 架构元素中的属性。</span><span class="sxs-lookup"><span data-stu-id="9a003-1089">The value for the **Namespace** attribute cannot be the same as the value for the **Namespace** attribute in the SSDL Schema element.</span></span> |
| <span data-ttu-id="9a003-1090">**Alias**</span><span class="sxs-lookup"><span data-stu-id="9a003-1090">**Alias**</span></span>      | <span data-ttu-id="9a003-1091">否</span><span class="sxs-lookup"><span data-stu-id="9a003-1091">No</span></span>          | <span data-ttu-id="9a003-1092">用于取代命名空间名称的标识符。</span><span class="sxs-lookup"><span data-stu-id="9a003-1092">An identifier used in place of the namespace name.</span></span> <span data-ttu-id="9a003-1093">例如，如果**EntityType**名为*客户*位于 Simple.Example.Model 命名空间和值**别名**特性是*模型*，则您可以将 Model.Customer 用作完全限定的名称**EntityType。**</span><span class="sxs-lookup"><span data-stu-id="9a003-1093">For example, if an **EntityType** named *Customer* is in the Simple.Example.Model namespace and the value of the **Alias** attribute is *Model*, then you can use Model.Customer as the fully qualified name of the **EntityType.**</span></span>                                                                                                                                                                                                                                                                                                     |

 

> [!NOTE]
> <span data-ttu-id="9a003-1094">可以将任意数量的 （自定义 XML 特性） 的批注特性应用于**架构**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-1094">Any number of annotation attributes (custom XML attributes) may be applied to the **Schema** element.</span></span> <span data-ttu-id="9a003-1095">然而，自定义特性可能不属于为 CSDL 保留的任何 XML 命名空间。</span><span class="sxs-lookup"><span data-stu-id="9a003-1095">However, custom attributes may not belong to any XML namespace that is reserved for CSDL.</span></span> <span data-ttu-id="9a003-1096">任何两个自定义特性的完全限定名称都不能相同。</span><span class="sxs-lookup"><span data-stu-id="9a003-1096">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

 

### <a name="example"></a><span data-ttu-id="9a003-1097">示例</span><span class="sxs-lookup"><span data-stu-id="9a003-1097">Example</span></span>

<span data-ttu-id="9a003-1098">下面的示例演示**架构**元素，其中包含**EntityContainer**元素、 两个**EntityType**元素，其中一个**关联**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-1098">The following example shows a **Schema** element that contains an **EntityContainer** element, two **EntityType** elements, and one **Association** element.</span></span>

``` xml
 <Schema xmlns="http://schemas.microsoft.com/ado/2009/11/edm"
      xmlns:cg="http://schemas.microsoft.com/ado/2009/11/codegeneration"
      xmlns:store="http://schemas.microsoft.com/ado/2009/11/edm/EntityStoreSchemaGenerator"
       Namespace="ExampleModel" Alias="Self">
         <EntityContainer Name="ExampleModelContainer">
           <EntitySet Name="Customers"
                      EntityType="ExampleModel.Customer" />
           <EntitySet Name="Orders" EntityType="ExampleModel.Order" />
           <AssociationSet
                       Name="CustomerOrder"
                       Association="ExampleModel.CustomerOrders">
             <End Role="Customer" EntitySet="Customers" />
             <End Role="Order" EntitySet="Orders" />
           </AssociationSet>
         </EntityContainer>
         <EntityType Name="Customer">
           <Key>
             <PropertyRef Name="CustomerId" />
           </Key>
           <Property Type="Int32" Name="CustomerId" Nullable="false" />
           <Property Type="String" Name="Name" Nullable="false" />
           <NavigationProperty
                    Name="Orders"
                    Relationship="ExampleModel.CustomerOrders"
                    FromRole="Customer" ToRole="Order" />
         </EntityType>
         <EntityType Name="Order">
           <Key>
             <PropertyRef Name="OrderId" />
           </Key>
           <Property Type="Int32" Name="OrderId" Nullable="false" />
           <Property Type="Int32" Name="ProductId" Nullable="false" />
           <Property Type="Int32" Name="Quantity" Nullable="false" />
           <NavigationProperty
                    Name="Customer"
                    Relationship="ExampleModel.CustomerOrders"
                    FromRole="Order" ToRole="Customer" />
           <Property Type="Int32" Name="CustomerId" Nullable="false" />
         </EntityType>
         <Association Name="CustomerOrders">
           <End Type="ExampleModel.Customer"
                Role="Customer" Multiplicity="1" />
           <End Type="ExampleModel.Order"
                Role="Order" Multiplicity="*" />
           <ReferentialConstraint>
             <Principal Role="Customer">
               <PropertyRef Name="CustomerId" />
             </Principal>
             <Dependent Role="Order">
               <PropertyRef Name="CustomerId" />
             </Dependent>
           </ReferentialConstraint>
         </Association>
       </Schema>
```
 

 

## <a name="typeref-element-csdl"></a><span data-ttu-id="9a003-1099">TypeRef 元素 (CSDL)</span><span class="sxs-lookup"><span data-stu-id="9a003-1099">TypeRef Element (CSDL)</span></span>

<span data-ttu-id="9a003-1100">**TypeRef**概念架构定义语言 (CSDL) 中的元素提供对现有的已命名类型的引用。</span><span class="sxs-lookup"><span data-stu-id="9a003-1100">The **TypeRef** element in conceptual schema definition language (CSDL) provides a reference to an existing named type.</span></span> <span data-ttu-id="9a003-1101">**TypeRef**元素可以是 CollectionType 元素用于指定函数具有集合作为参数或返回类型的子元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-1101">The **TypeRef** element can be a child of the CollectionType element, which is used to specify that a function has a collection as a parameter or return type.</span></span>

<span data-ttu-id="9a003-1102">一个**TypeRef**元素可以具有下列子元素 （按所列顺序）：</span><span class="sxs-lookup"><span data-stu-id="9a003-1102">A **TypeRef** element can have the following child elements (in the order listed):</span></span>

-   <span data-ttu-id="9a003-1103">文档 （零个或一个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-1103">Documentation (zero or one element)</span></span>
-   <span data-ttu-id="9a003-1104">批注元素 （零个或多个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-1104">Annotation elements (zero or more elements)</span></span>

### <a name="applicable-attributes"></a><span data-ttu-id="9a003-1105">适用的特性</span><span class="sxs-lookup"><span data-stu-id="9a003-1105">Applicable Attributes</span></span>

<span data-ttu-id="9a003-1106">下表介绍可应用于的特性**TypeRef**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-1106">The following table describes the attributes that can be applied to the **TypeRef** element.</span></span> <span data-ttu-id="9a003-1107">请注意， **DefaultValue**， **MaxLength**， **FixedLength**，**精度**，**规模**， **Unicode**，并**排序规则**属性都只适用于**Edmsimpletype**。</span><span class="sxs-lookup"><span data-stu-id="9a003-1107">Note that the **DefaultValue**, **MaxLength**, **FixedLength**, **Precision**, **Scale**, **Unicode**, and **Collation** attributes are only applicable to **EDMSimpleTypes**.</span></span>

| <span data-ttu-id="9a003-1108">特性名</span><span class="sxs-lookup"><span data-stu-id="9a003-1108">Attribute Name</span></span>                                                     | <span data-ttu-id="9a003-1109">是否必需</span><span class="sxs-lookup"><span data-stu-id="9a003-1109">Is Required</span></span> | <span data-ttu-id="9a003-1110">“值”</span><span class="sxs-lookup"><span data-stu-id="9a003-1110">Value</span></span>                                                                                                                                                                                                                           |
|:-------------------------------------------------------------------|:------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9a003-1111">**Type**</span><span class="sxs-lookup"><span data-stu-id="9a003-1111">**Type**</span></span>                                                           | <span data-ttu-id="9a003-1112">否</span><span class="sxs-lookup"><span data-stu-id="9a003-1112">No</span></span>          | <span data-ttu-id="9a003-1113">所引用的类型的名称。</span><span class="sxs-lookup"><span data-stu-id="9a003-1113">The name of the type being referenced.</span></span>                                                                                                                                                                                          |
| <span data-ttu-id="9a003-1114">**可以为 null**</span><span class="sxs-lookup"><span data-stu-id="9a003-1114">**Nullable**</span></span>                                                       | <span data-ttu-id="9a003-1115">否</span><span class="sxs-lookup"><span data-stu-id="9a003-1115">No</span></span>          | <span data-ttu-id="9a003-1116">**True** （默认值） 或**False**具体取决于属性是否可以具有 null 值。</span><span class="sxs-lookup"><span data-stu-id="9a003-1116">**True** (the default value) or **False** depending on whether the property can have a null value.</span></span> <br/> [!NOTE]                                                                                                                |
| <span data-ttu-id="9a003-1117">> CSDL v1 中的复杂类型属性必须具有`Nullable="False"`。</span><span class="sxs-lookup"><span data-stu-id="9a003-1117">> In CSDL v1 a complex type property must have `Nullable="False"`.</span></span> |             |                                                                                                                                                                                                                                 |
| <span data-ttu-id="9a003-1118">**DefaultValue**</span><span class="sxs-lookup"><span data-stu-id="9a003-1118">**DefaultValue**</span></span>                                                   | <span data-ttu-id="9a003-1119">否</span><span class="sxs-lookup"><span data-stu-id="9a003-1119">No</span></span>          | <span data-ttu-id="9a003-1120">属性的默认值。</span><span class="sxs-lookup"><span data-stu-id="9a003-1120">The default value of the property.</span></span>                                                                                                                                                                                              |
| <span data-ttu-id="9a003-1121">**MaxLength**</span><span class="sxs-lookup"><span data-stu-id="9a003-1121">**MaxLength**</span></span>                                                      | <span data-ttu-id="9a003-1122">否</span><span class="sxs-lookup"><span data-stu-id="9a003-1122">No</span></span>          | <span data-ttu-id="9a003-1123">属性值的最大长度。</span><span class="sxs-lookup"><span data-stu-id="9a003-1123">The maximum length of the property value.</span></span>                                                                                                                                                                                       |
| <span data-ttu-id="9a003-1124">**FixedLength**</span><span class="sxs-lookup"><span data-stu-id="9a003-1124">**FixedLength**</span></span>                                                    | <span data-ttu-id="9a003-1125">否</span><span class="sxs-lookup"><span data-stu-id="9a003-1125">No</span></span>          | <span data-ttu-id="9a003-1126">**True**或**False**具体取决于属性值是否将作为固定的长度字符串存储。</span><span class="sxs-lookup"><span data-stu-id="9a003-1126">**True** or **False** depending on whether the property value will be stored as a fixed length string.</span></span>                                                                                                                          |
| <span data-ttu-id="9a003-1127">**精度**</span><span class="sxs-lookup"><span data-stu-id="9a003-1127">**Precision**</span></span>                                                      | <span data-ttu-id="9a003-1128">否</span><span class="sxs-lookup"><span data-stu-id="9a003-1128">No</span></span>          | <span data-ttu-id="9a003-1129">属性值的精度。</span><span class="sxs-lookup"><span data-stu-id="9a003-1129">The precision of the property value.</span></span>                                                                                                                                                                                            |
| <span data-ttu-id="9a003-1130">缩放</span><span class="sxs-lookup"><span data-stu-id="9a003-1130">**Scale**</span></span>                                                          | <span data-ttu-id="9a003-1131">否</span><span class="sxs-lookup"><span data-stu-id="9a003-1131">No</span></span>          | <span data-ttu-id="9a003-1132">属性值的刻度。</span><span class="sxs-lookup"><span data-stu-id="9a003-1132">The scale of the property value.</span></span>                                                                                                                                                                                                |
| <span data-ttu-id="9a003-1133">**SRID**</span><span class="sxs-lookup"><span data-stu-id="9a003-1133">**SRID**</span></span>                                                           | <span data-ttu-id="9a003-1134">否</span><span class="sxs-lookup"><span data-stu-id="9a003-1134">No</span></span>          | <span data-ttu-id="9a003-1135">系统的空间引用标识符。</span><span class="sxs-lookup"><span data-stu-id="9a003-1135">Spatial System Reference Identifier.</span></span> <span data-ttu-id="9a003-1136">仅对空间类型的属性有效。</span><span class="sxs-lookup"><span data-stu-id="9a003-1136">Valid only for properties of spatial types.</span></span> <span data-ttu-id="9a003-1137">有关详细信息，请参阅[SRID](http://en.wikipedia.org/wiki/SRID)并[SRID (SQL Server)](https://msdn.microsoft.com/library/bb964707.aspx)。</span><span class="sxs-lookup"><span data-stu-id="9a003-1137">For more information, see [SRID](http://en.wikipedia.org/wiki/SRID) and [SRID (SQL Server)](https://msdn.microsoft.com/library/bb964707.aspx).</span></span> |
| <span data-ttu-id="9a003-1138">**Unicode**</span><span class="sxs-lookup"><span data-stu-id="9a003-1138">**Unicode**</span></span>                                                        | <span data-ttu-id="9a003-1139">否</span><span class="sxs-lookup"><span data-stu-id="9a003-1139">No</span></span>          | <span data-ttu-id="9a003-1140">**True**或**False**具体取决于是否在属性值将存储为 Unicode 字符串。</span><span class="sxs-lookup"><span data-stu-id="9a003-1140">**True** or **False** depending on whether the property value will be stored as a Unicode string.</span></span>                                                                                                                               |
| <span data-ttu-id="9a003-1141">**排序规则**</span><span class="sxs-lookup"><span data-stu-id="9a003-1141">**Collation**</span></span>                                                      | <span data-ttu-id="9a003-1142">否</span><span class="sxs-lookup"><span data-stu-id="9a003-1142">No</span></span>          | <span data-ttu-id="9a003-1143">指定要在数据源中使用的排序序列的字符串。</span><span class="sxs-lookup"><span data-stu-id="9a003-1143">A string that specifies the collating sequence to be used in the data source.</span></span>                                                                                                                                                   |

 

> [!NOTE]
> <span data-ttu-id="9a003-1144">可以将任意数量的 （自定义 XML 特性） 的批注特性应用于**CollectionType**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-1144">Any number of annotation attributes (custom XML attributes) may be applied to the **CollectionType** element.</span></span> <span data-ttu-id="9a003-1145">然而，自定义特性可能不属于为 CSDL 保留的任何 XML 命名空间。</span><span class="sxs-lookup"><span data-stu-id="9a003-1145">However, custom attributes may not belong to any XML namespace that is reserved for CSDL.</span></span> <span data-ttu-id="9a003-1146">任何两个自定义特性的完全限定名称都不能相同。</span><span class="sxs-lookup"><span data-stu-id="9a003-1146">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

 

### <a name="example"></a><span data-ttu-id="9a003-1147">示例</span><span class="sxs-lookup"><span data-stu-id="9a003-1147">Example</span></span>

<span data-ttu-id="9a003-1148">下面的示例演示使用的模型定义函数**TypeRef**元素 (作为子级**CollectionType**元素) 来指定该函数接受一系列**部门**实体类型。</span><span class="sxs-lookup"><span data-stu-id="9a003-1148">The following example shows a model-defined function that uses the **TypeRef** element (as a child of a **CollectionType** element) to specify that the function accepts a collection of **Department** entity types.</span></span>

``` xml
 <Function Name="GetAvgBudget">
      <Parameter Name="Departments">
          <CollectionType>
             <TypeRef Type="SchoolModel.Department"/>
          </CollectionType>
           </Parameter>
       <ReturnType Type="Collection(Edm.Decimal)"/>
       <DefiningExpression>
             SELECT VALUE AVG(d.Budget) FROM Departments AS d
       </DefiningExpression>
 </Function>
```
 

 

## <a name="using-element-csdl"></a><span data-ttu-id="9a003-1149">Using 元素 (CSDL)</span><span class="sxs-lookup"><span data-stu-id="9a003-1149">Using Element (CSDL)</span></span>

<span data-ttu-id="9a003-1150">**Using**元素在概念架构定义语言 (CSDL) 中的导入不同的命名空间中存在的概念模型的内容。</span><span class="sxs-lookup"><span data-stu-id="9a003-1150">The **Using** element in conceptual schema definition language (CSDL) imports the contents of a conceptual model that exists in a different namespace.</span></span> <span data-ttu-id="9a003-1151">通过设置的值**Namespace**属性，您可以引用实体类型、 复杂类型和另一个概念模型中定义的关联类型。</span><span class="sxs-lookup"><span data-stu-id="9a003-1151">By setting the value of the **Namespace** attribute, you can refer to entity types, complex types, and association types that are defined in another conceptual model.</span></span> <span data-ttu-id="9a003-1152">多个**Using**元素可以是子元素的**架构**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-1152">More than one **Using** element can be a child of a **Schema** element.</span></span>

> [!NOTE]
> <span data-ttu-id="9a003-1153">**Using** CSDL 中的元素不能完全相同**使用**编程语言中的语句。</span><span class="sxs-lookup"><span data-stu-id="9a003-1153">The **Using** element in CSDL does not function exactly like a **using** statement in a programming language.</span></span> <span data-ttu-id="9a003-1154">通过导入的命名空间**使用**语句在编程语言中，您不会影响原始命名空间中的对象。</span><span class="sxs-lookup"><span data-stu-id="9a003-1154">By importing a namespace with a **using** statement in a programming language, you do not affect objects in the original namespace.</span></span> <span data-ttu-id="9a003-1155">在 CSDL 中，导入的命名空间可以包含从原始命名空间中的实体类型导出的实体类型。</span><span class="sxs-lookup"><span data-stu-id="9a003-1155">In CSDL, an imported namespace can contain an entity type that is derived from an entity type in the original namespace.</span></span> <span data-ttu-id="9a003-1156">这可能影响在原始命名空间中声明的实体集。</span><span class="sxs-lookup"><span data-stu-id="9a003-1156">This can affect entity sets declared in the original namespace.</span></span>

 

<span data-ttu-id="9a003-1157">**Using**元素可以具有以下子元素：</span><span class="sxs-lookup"><span data-stu-id="9a003-1157">The **Using** element can have the following child elements:</span></span>

-   <span data-ttu-id="9a003-1158">文档 （允许零个或一个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-1158">Documentation (zero or one elements allowed)</span></span>
-   <span data-ttu-id="9a003-1159">批注元素 （允许零个或多个元素）</span><span class="sxs-lookup"><span data-stu-id="9a003-1159">Annotation elements (zero or more elements allowed)</span></span>

### <a name="applicable-attributes"></a><span data-ttu-id="9a003-1160">适用的特性</span><span class="sxs-lookup"><span data-stu-id="9a003-1160">Applicable Attributes</span></span>

<span data-ttu-id="9a003-1161">下表描述了特性可应用于**Using**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-1161">The table below describes the attributes can be applied to the **Using** element.</span></span>

| <span data-ttu-id="9a003-1162">特性名</span><span class="sxs-lookup"><span data-stu-id="9a003-1162">Attribute Name</span></span> | <span data-ttu-id="9a003-1163">是否必需</span><span class="sxs-lookup"><span data-stu-id="9a003-1163">Is Required</span></span> | <span data-ttu-id="9a003-1164">“值”</span><span class="sxs-lookup"><span data-stu-id="9a003-1164">Value</span></span>                                                                                                                                                                              |
|:---------------|:------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9a003-1165">**命名空间**</span><span class="sxs-lookup"><span data-stu-id="9a003-1165">**Namespace**</span></span>  | <span data-ttu-id="9a003-1166">是</span><span class="sxs-lookup"><span data-stu-id="9a003-1166">Yes</span></span>         | <span data-ttu-id="9a003-1167">导入的命名空间的名称。</span><span class="sxs-lookup"><span data-stu-id="9a003-1167">The name of the imported namespace.</span></span>                                                                                                                                                |
| <span data-ttu-id="9a003-1168">**Alias**</span><span class="sxs-lookup"><span data-stu-id="9a003-1168">**Alias**</span></span>      | <span data-ttu-id="9a003-1169">是</span><span class="sxs-lookup"><span data-stu-id="9a003-1169">Yes</span></span>         | <span data-ttu-id="9a003-1170">用于取代命名空间名称的标识符。</span><span class="sxs-lookup"><span data-stu-id="9a003-1170">An identifier used in place of the namespace name.</span></span> <span data-ttu-id="9a003-1171">尽管此特性是必需的，但并不要求使用它来取代命名空间以限定对象名称。</span><span class="sxs-lookup"><span data-stu-id="9a003-1171">Although this attribute is required, it is not required that it be used in place of the namespace name to qualify object names.</span></span> |

 

> [!NOTE]
> <span data-ttu-id="9a003-1172">可以将任意数量的 （自定义 XML 特性） 的批注特性应用于**Using**元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-1172">Any number of annotation attributes (custom XML attributes) may be applied to the **Using** element.</span></span> <span data-ttu-id="9a003-1173">然而，自定义特性可能不属于为 CSDL 保留的任何 XML 命名空间。</span><span class="sxs-lookup"><span data-stu-id="9a003-1173">However, custom attributes may not belong to any XML namespace that is reserved for CSDL.</span></span> <span data-ttu-id="9a003-1174">任何两个自定义特性的完全限定名称都不能相同。</span><span class="sxs-lookup"><span data-stu-id="9a003-1174">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

 

### <a name="example"></a><span data-ttu-id="9a003-1175">示例</span><span class="sxs-lookup"><span data-stu-id="9a003-1175">Example</span></span>

<span data-ttu-id="9a003-1176">下面的示例演示**Using**用于导入的命名空间的元素定义的其他位置。</span><span class="sxs-lookup"><span data-stu-id="9a003-1176">The following example demonstrates the **Using** element being used to import a namespace that is defined elsewhere.</span></span> <span data-ttu-id="9a003-1177">请注意，为命名空间**架构**所示的元素是`BooksModel`。</span><span class="sxs-lookup"><span data-stu-id="9a003-1177">Note that the namespace for the **Schema** element shown is `BooksModel`.</span></span> <span data-ttu-id="9a003-1178">`Address`上的属性`Publisher` **EntityType**是中定义的复杂类型`ExtendedBooksModel`命名空间 (使用导入**Using**元素)。</span><span class="sxs-lookup"><span data-stu-id="9a003-1178">The `Address` property on the `Publisher`**EntityType** is a complex type that is defined in the `ExtendedBooksModel` namespace (imported with the **Using** element).</span></span>

``` xml
 <Schema xmlns="http://schemas.microsoft.com/ado/2009/11/edm"
           xmlns:cg="http://schemas.microsoft.com/ado/2009/11/codegeneration"
           xmlns:store="http://schemas.microsoft.com/ado/2009/11/edm/EntityStoreSchemaGenerator"
           Namespace="BooksModel" Alias="Self">

     <Using Namespace="BooksModel.Extended" Alias="BMExt" />

 <EntityContainer Name="BooksContainer" >
       <EntitySet Name="Publishers" EntityType="BooksModel.Publisher" />
     </EntityContainer>

 <EntityType Name="Publisher">
       <Key>
         <PropertyRef Name="Id" />
       </Key>
       <Property Type="Int32" Name="Id" Nullable="false" />
       <Property Type="String" Name="Name" Nullable="false" />
       <Property Type="BMExt.Address" Name="Address" Nullable="false" />
     </EntityType>

 </Schema>
```
 

 

## <a name="annotation-attributes-csdl"></a><span data-ttu-id="9a003-1179">Annotation 特性 (CSDL)</span><span class="sxs-lookup"><span data-stu-id="9a003-1179">Annotation Attributes (CSDL)</span></span>

<span data-ttu-id="9a003-1180">以概念架构定义语言 (CSDL) 表示的批注特性是概念模型中的自定义 XML 特性。</span><span class="sxs-lookup"><span data-stu-id="9a003-1180">Annotation attributes in conceptual schema definition language (CSDL) are custom XML attributes in the conceptual model.</span></span> <span data-ttu-id="9a003-1181">除了具有有效的 XML 结构之外，还必须满足批注特性的以下各项条件：</span><span class="sxs-lookup"><span data-stu-id="9a003-1181">In addition to having valid XML structure, the following must be true of annotation attributes:</span></span>

-   <span data-ttu-id="9a003-1182">批注特性不能位于为 CSDL 保留的任何 XML 命名空间中。</span><span class="sxs-lookup"><span data-stu-id="9a003-1182">Annotation attributes must not be in any XML namespace that is reserved for CSDL.</span></span>
-   <span data-ttu-id="9a003-1183">可以将多个批注特性应用于给定的 CSDL 元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-1183">More than one annotation attribute may be applied to a given CSDL element.</span></span>
-   <span data-ttu-id="9a003-1184">任何两个批注特性的完全限定名称都不能相同。</span><span class="sxs-lookup"><span data-stu-id="9a003-1184">The fully-qualified names of any two annotation attributes must not be the same.</span></span>

<span data-ttu-id="9a003-1185">可以使用批注特性提供有关概念模型中元素的额外元数据。</span><span class="sxs-lookup"><span data-stu-id="9a003-1185">Annotation attributes can be used to provide extra metadata about the elements in a conceptual model.</span></span> <span data-ttu-id="9a003-1186">可以使用 System.Data.Metadata.Edm 命名空间中的类，在运行时访问批注元素中包含的元数据。</span><span class="sxs-lookup"><span data-stu-id="9a003-1186">Metadata contained in annotation elements can be accessed at runtime by using classes in the System.Data.Metadata.Edm namespace.</span></span>

### <a name="example"></a><span data-ttu-id="9a003-1187">示例</span><span class="sxs-lookup"><span data-stu-id="9a003-1187">Example</span></span>

<span data-ttu-id="9a003-1188">下面的示例演示**EntityType**元素具有一个批注特性 (**CustomAttribute**)。</span><span class="sxs-lookup"><span data-stu-id="9a003-1188">The following example shows an **EntityType** element with an annotation attribute (**CustomAttribute**).</span></span> <span data-ttu-id="9a003-1189">本示例还演示了一个应用于实体类型元素的批注元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-1189">The example also shows an annotation element applied to the entity type element.</span></span>

``` xml
 <Schema Namespace="SchoolModel" Alias="Self"
         xmlns:annotation="http://schemas.microsoft.com/ado/2009/02/edm/annotation"
         xmlns="http://schemas.microsoft.com/ado/2009/11/edm">
   <EntityContainer Name="SchoolEntities" annotation:LazyLoadingEnabled="true">
     <EntitySet Name="People" EntityType="SchoolModel.Person" />
   </EntityContainer>
   <EntityType Name="Person" xmlns:p="http://CustomNamespace.com"
               p:CustomAttribute="Data here.">
     <Key>
       <PropertyRef Name="PersonID" />
     </Key>
     <Property Name="PersonID" Type="Int32" Nullable="false"
               annotation:StoreGeneratedPattern="Identity" />
     <Property Name="LastName" Type="String" Nullable="false"
               MaxLength="50" Unicode="true" FixedLength="false" />
     <Property Name="FirstName" Type="String" Nullable="false"
               MaxLength="50" Unicode="true" FixedLength="false" />
     <Property Name="HireDate" Type="DateTime" />
     <Property Name="EnrollmentDate" Type="DateTime" />
     <p:CustomElement>
       Custom metadata.
     </p:CustomElement>
   </EntityType>
 </Schema>
```
 

<span data-ttu-id="9a003-1190">下面的代码检索批注特性中的元数据并将其写入控制台：</span><span class="sxs-lookup"><span data-stu-id="9a003-1190">The following code retrieves the metadata in the annotation attribute and writes it to the console:</span></span>

``` xml
 EdmItemCollection collection = new EdmItemCollection("School.csdl");
 MetadataWorkspace workspace = new MetadataWorkspace();
 workspace.RegisterItemCollection(collection);
 EdmType contentType;
 workspace.TryGetType("Person", "SchoolModel", DataSpace.CSpace, out contentType);
 if (contentType.MetadataProperties.Contains("http://CustomNamespace.com:CustomAttribute"))
 {
     MetadataProperty annotationProperty =
         contentType.MetadataProperties["http://CustomNamespace.com:CustomAttribute"];
     object annotationValue = annotationProperty.Value;
     Console.WriteLine(annotationValue.ToString());
 }
```
 

<span data-ttu-id="9a003-1191">上面的代码假定 `School.csdl` 文件位于项目的输出目录中，且您已将下面的 `Imports` 和 `Using` 语句添加到项目中：</span><span class="sxs-lookup"><span data-stu-id="9a003-1191">The code above assumes that the `School.csdl` file is in the project's output directory and that you have added the following `Imports` and `Using` statements to your project:</span></span>

``` csharp
 using System.Data.Metadata.Edm;
```
 

 

## <a name="annotation-elements-csdl"></a><span data-ttu-id="9a003-1192">Annotation 元素 (CSDL)</span><span class="sxs-lookup"><span data-stu-id="9a003-1192">Annotation Elements (CSDL)</span></span>

<span data-ttu-id="9a003-1193">以概念架构定义语言 (CSDL) 表示的批注元素是概念模型中的自定义 XML 元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-1193">Annotation elements in conceptual schema definition language (CSDL) are custom XML elements in the conceptual model.</span></span> <span data-ttu-id="9a003-1194">除了具有有效的 XML 结构之外，还必须满足批注元素的以下各项条件：</span><span class="sxs-lookup"><span data-stu-id="9a003-1194">In addition to having valid XML structure, the following must be true of annotation elements:</span></span>

-   <span data-ttu-id="9a003-1195">批注元素不能位于为 CSDL 保留的任何 XML 命名空间中。</span><span class="sxs-lookup"><span data-stu-id="9a003-1195">Annotation elements must not be in any XML namespace that is reserved for CSDL.</span></span>
-   <span data-ttu-id="9a003-1196">多个批注元素可能是某个给定 CSDL 元素的子元素。</span><span class="sxs-lookup"><span data-stu-id="9a003-1196">More than one annotation element may be a child of a given CSDL element.</span></span>
-   <span data-ttu-id="9a003-1197">任何两个批注元素的完全限定名称都不能相同。</span><span class="sxs-lookup"><span data-stu-id="9a003-1197">The fully-qualified names of any two annotation elements must not be the same.</span></span>
-   <span data-ttu-id="9a003-1198">批注元素必须出现在给定 CSDL 元素的所有其他子元素之后。</span><span class="sxs-lookup"><span data-stu-id="9a003-1198">Annotation elements must appear after all other child elements of a given CSDL element.</span></span>

<span data-ttu-id="9a003-1199">可以使用批注元素提供有关概念模型中元素的额外元数据。</span><span class="sxs-lookup"><span data-stu-id="9a003-1199">Annotation elements can be used to provide extra metadata about the elements in a conceptual model.</span></span> <span data-ttu-id="9a003-1200">从.NET Framework 版本 4 开始，访问元数据批注元素中包含可以在运行时使用 System.Data.Metadata.Edm 命名空间中的类。</span><span class="sxs-lookup"><span data-stu-id="9a003-1200">Starting with the .NET Framework version 4, metadata contained in annotation elements can be accessed at runtime by using classes in the System.Data.Metadata.Edm namespace.</span></span>

### <a name="example"></a><span data-ttu-id="9a003-1201">示例</span><span class="sxs-lookup"><span data-stu-id="9a003-1201">Example</span></span>

<span data-ttu-id="9a003-1202">下面的示例演示**EntityType**具有一个批注元素的元素 (**CustomElement**)。</span><span class="sxs-lookup"><span data-stu-id="9a003-1202">The following example shows an **EntityType** element with an annotation element (**CustomElement**).</span></span> <span data-ttu-id="9a003-1203">本示例还演示了一个应用于实体类型元素的批注特性。</span><span class="sxs-lookup"><span data-stu-id="9a003-1203">The example also show an annotation attribute applied to the entity type element.</span></span>

``` xml
 <Schema Namespace="SchoolModel" Alias="Self"
         xmlns:annotation="http://schemas.microsoft.com/ado/2009/02/edm/annotation"
         xmlns="http://schemas.microsoft.com/ado/2009/11/edm">
   <EntityContainer Name="SchoolEntities" annotation:LazyLoadingEnabled="true">
     <EntitySet Name="People" EntityType="SchoolModel.Person" />
   </EntityContainer>
   <EntityType Name="Person" xmlns:p="http://CustomNamespace.com"
               p:CustomAttribute="Data here.">
     <Key>
       <PropertyRef Name="PersonID" />
     </Key>
     <Property Name="PersonID" Type="Int32" Nullable="false"
               annotation:StoreGeneratedPattern="Identity" />
     <Property Name="LastName" Type="String" Nullable="false"
               MaxLength="50" Unicode="true" FixedLength="false" />
     <Property Name="FirstName" Type="String" Nullable="false"
               MaxLength="50" Unicode="true" FixedLength="false" />
     <Property Name="HireDate" Type="DateTime" />
     <Property Name="EnrollmentDate" Type="DateTime" />
     <p:CustomElement>
       Custom metadata.
     </p:CustomElement>
   </EntityType>
 </Schema>
```
 

<span data-ttu-id="9a003-1204">下面的代码检索批注元素中的元数据并将其写入控制台：</span><span class="sxs-lookup"><span data-stu-id="9a003-1204">The following code retrieves the metadata in the annotation element and writes it to the console:</span></span>

``` csharp
 EdmItemCollection collection = new EdmItemCollection("School.csdl");
 MetadataWorkspace workspace = new MetadataWorkspace();
 workspace.RegisterItemCollection(collection);
 EdmType contentType;
 workspace.TryGetType("Person", "SchoolModel", DataSpace.CSpace, out contentType);
 if (contentType.MetadataProperties.Contains("http://CustomNamespace.com:CustomElement"))
 {
     MetadataProperty annotationProperty =
         contentType.MetadataProperties["http://CustomNamespace.com:CustomElement"];
     object annotationValue = annotationProperty.Value;
     Console.WriteLine(annotationValue.ToString());
 }
```
 

<span data-ttu-id="9a003-1205">上面的代码假定 School.csdl 文件位于项目的输出目录中并且您已将下面的 `Imports` 和 `Using` 语句添加到项目中：</span><span class="sxs-lookup"><span data-stu-id="9a003-1205">The code above assumes that the School.csdl file is in the project's output directory and that you have added the following `Imports` and `Using` statements to your project:</span></span>

``` csharp
 using System.Data.Metadata.Edm;
```
 

 

## <a name="conceptual-model-types-csdl"></a><span data-ttu-id="9a003-1206">概念模型类型 (CSDL)</span><span class="sxs-lookup"><span data-stu-id="9a003-1206">Conceptual Model Types (CSDL)</span></span>

<span data-ttu-id="9a003-1207">概念架构定义语言 (CSDL) 支持一种抽象的基元数据类型，称为**Edmsimpletype**，用于定义概念模型中的属性。</span><span class="sxs-lookup"><span data-stu-id="9a003-1207">Conceptual schema definition language (CSDL) supports a set of abstract primitive data types, called **EDMSimpleTypes**, that define properties in a conceptual model.</span></span> <span data-ttu-id="9a003-1208">**Edmsimpletype**是存储或承载环境中支持的基元数据类型的代理。</span><span class="sxs-lookup"><span data-stu-id="9a003-1208">**EDMSimpleTypes** are proxies for primitive data types that are supported in the storage or hosting environment.</span></span>

<span data-ttu-id="9a003-1209">下表列出了 CSDL 支持的基元数据类型。</span><span class="sxs-lookup"><span data-stu-id="9a003-1209">The table below lists the primitive data types that are supported by CSDL.</span></span> <span data-ttu-id="9a003-1210">该表还列出了可以应用于每个方面**EDMSimpleType**。</span><span class="sxs-lookup"><span data-stu-id="9a003-1210">The table also lists the facets that can be applied to each **EDMSimpleType**.</span></span>

| <span data-ttu-id="9a003-1211">EDMSimpleType</span><span class="sxs-lookup"><span data-stu-id="9a003-1211">EDMSimpleType</span></span>                    | <span data-ttu-id="9a003-1212">描述</span><span class="sxs-lookup"><span data-stu-id="9a003-1212">Description</span></span>                                                | <span data-ttu-id="9a003-1213">适用的方面</span><span class="sxs-lookup"><span data-stu-id="9a003-1213">Applicable Facets</span></span>                                                        |
|:---------------------------------|:-----------------------------------------------------------|:-------------------------------------------------------------------------|
| <span data-ttu-id="9a003-1214">**Edm.Binary**</span><span class="sxs-lookup"><span data-stu-id="9a003-1214">**Edm.Binary**</span></span>                   | <span data-ttu-id="9a003-1215">包含二进制数据。</span><span class="sxs-lookup"><span data-stu-id="9a003-1215">Contains binary data.</span></span>                                      | <span data-ttu-id="9a003-1216">MaxLength、FixedLength、Nullable、Default</span><span class="sxs-lookup"><span data-stu-id="9a003-1216">MaxLength, FixedLength, Nullable, Default</span></span>                                |
| <span data-ttu-id="9a003-1217">**Edm.Boolean**</span><span class="sxs-lookup"><span data-stu-id="9a003-1217">**Edm.Boolean**</span></span>                  | <span data-ttu-id="9a003-1218">包含值 **，则返回 true**或**false**。</span><span class="sxs-lookup"><span data-stu-id="9a003-1218">Contains the value **true** or **false**.</span></span>                  | <span data-ttu-id="9a003-1219">Nullable、Default</span><span class="sxs-lookup"><span data-stu-id="9a003-1219">Nullable, Default</span></span>                                                        |
| <span data-ttu-id="9a003-1220">**Edm.Byte**</span><span class="sxs-lookup"><span data-stu-id="9a003-1220">**Edm.Byte**</span></span>                     | <span data-ttu-id="9a003-1221">包含一个无符号的 8 位整数值。</span><span class="sxs-lookup"><span data-stu-id="9a003-1221">Contains an unsigned 8-bit integer value.</span></span>                  | <span data-ttu-id="9a003-1222">Precision、Nullable、Default</span><span class="sxs-lookup"><span data-stu-id="9a003-1222">Precision, Nullable, Default</span></span>                                             |
| <span data-ttu-id="9a003-1223">**Edm.DateTime**</span><span class="sxs-lookup"><span data-stu-id="9a003-1223">**Edm.DateTime**</span></span>                 | <span data-ttu-id="9a003-1224">表示日期和时间。</span><span class="sxs-lookup"><span data-stu-id="9a003-1224">Represents a date and time.</span></span>                                | <span data-ttu-id="9a003-1225">Precision、Nullable、Default</span><span class="sxs-lookup"><span data-stu-id="9a003-1225">Precision, Nullable, Default</span></span>                                             |
| <span data-ttu-id="9a003-1226">**Edm.DateTimeOffset**</span><span class="sxs-lookup"><span data-stu-id="9a003-1226">**Edm.DateTimeOffset**</span></span>           | <span data-ttu-id="9a003-1227">包含以相对于 GMT 的偏移量（以分钟为单位）表示的日期和时间。</span><span class="sxs-lookup"><span data-stu-id="9a003-1227">Contains a date and time as an offset in minutes from GMT.</span></span> | <span data-ttu-id="9a003-1228">Precision、Nullable、Default</span><span class="sxs-lookup"><span data-stu-id="9a003-1228">Precision, Nullable, Default</span></span>                                             |
| <span data-ttu-id="9a003-1229">**Edm.Decimal**</span><span class="sxs-lookup"><span data-stu-id="9a003-1229">**Edm.Decimal**</span></span>                  | <span data-ttu-id="9a003-1230">包含一个具有固定精度和小数位数的数值。</span><span class="sxs-lookup"><span data-stu-id="9a003-1230">Contains a numeric value with fixed precision and scale.</span></span>   | <span data-ttu-id="9a003-1231">Precision、Nullable、Default</span><span class="sxs-lookup"><span data-stu-id="9a003-1231">Precision, Nullable, Default</span></span>                                             |
| <span data-ttu-id="9a003-1232">**Edm.Double**</span><span class="sxs-lookup"><span data-stu-id="9a003-1232">**Edm.Double**</span></span>                   | <span data-ttu-id="9a003-1233">包含具有 15 位精度浮点数</span><span class="sxs-lookup"><span data-stu-id="9a003-1233">Contains a floating point number with 15-digit precision</span></span>   | <span data-ttu-id="9a003-1234">Precision、Nullable、Default</span><span class="sxs-lookup"><span data-stu-id="9a003-1234">Precision, Nullable, Default</span></span>                                             |
| <span data-ttu-id="9a003-1235">**Edm.Float**</span><span class="sxs-lookup"><span data-stu-id="9a003-1235">**Edm.Float**</span></span>                    | <span data-ttu-id="9a003-1236">包含一个具有 7 位精度的浮点数。</span><span class="sxs-lookup"><span data-stu-id="9a003-1236">Contains a floating point number with 7-digit precision.</span></span>   | <span data-ttu-id="9a003-1237">Precision、Nullable、Default</span><span class="sxs-lookup"><span data-stu-id="9a003-1237">Precision, Nullable, Default</span></span>                                             |
| <span data-ttu-id="9a003-1238">**Edm.Guid**</span><span class="sxs-lookup"><span data-stu-id="9a003-1238">**Edm.Guid**</span></span>                     | <span data-ttu-id="9a003-1239">包含一个 16 字节的唯一标识符。</span><span class="sxs-lookup"><span data-stu-id="9a003-1239">Contains a 16-byte unique identifier.</span></span>                      | <span data-ttu-id="9a003-1240">Precision、Nullable、Default</span><span class="sxs-lookup"><span data-stu-id="9a003-1240">Precision, Nullable, Default</span></span>                                             |
| <span data-ttu-id="9a003-1241">**Edm.Int16**</span><span class="sxs-lookup"><span data-stu-id="9a003-1241">**Edm.Int16**</span></span>                    | <span data-ttu-id="9a003-1242">包含一个带符号的 16 位整数值。</span><span class="sxs-lookup"><span data-stu-id="9a003-1242">Contains a signed 16-bit integer value.</span></span>                    | <span data-ttu-id="9a003-1243">Precision、Nullable、Default</span><span class="sxs-lookup"><span data-stu-id="9a003-1243">Precision, Nullable, Default</span></span>                                             |
| <span data-ttu-id="9a003-1244">**Edm.Int32**</span><span class="sxs-lookup"><span data-stu-id="9a003-1244">**Edm.Int32**</span></span>                    | <span data-ttu-id="9a003-1245">包含一个带符号的 32 位整数值。</span><span class="sxs-lookup"><span data-stu-id="9a003-1245">Contains a signed 32-bit integer value.</span></span>                    | <span data-ttu-id="9a003-1246">Precision、Nullable、Default</span><span class="sxs-lookup"><span data-stu-id="9a003-1246">Precision, Nullable, Default</span></span>                                             |
| <span data-ttu-id="9a003-1247">**Edm.Int64**</span><span class="sxs-lookup"><span data-stu-id="9a003-1247">**Edm.Int64**</span></span>                    | <span data-ttu-id="9a003-1248">包含一个带符号的 64 位整数值。</span><span class="sxs-lookup"><span data-stu-id="9a003-1248">Contains a signed 64-bit integer value.</span></span>                    | <span data-ttu-id="9a003-1249">Precision、Nullable、Default</span><span class="sxs-lookup"><span data-stu-id="9a003-1249">Precision, Nullable, Default</span></span>                                             |
| <span data-ttu-id="9a003-1250">**Edm.SByte**</span><span class="sxs-lookup"><span data-stu-id="9a003-1250">**Edm.SByte**</span></span>                    | <span data-ttu-id="9a003-1251">包含一个带符号的 8 位整数值。</span><span class="sxs-lookup"><span data-stu-id="9a003-1251">Contains a signed 8-bit integer value.</span></span>                     | <span data-ttu-id="9a003-1252">Precision、Nullable、Default</span><span class="sxs-lookup"><span data-stu-id="9a003-1252">Precision, Nullable, Default</span></span>                                             |
| <span data-ttu-id="9a003-1253">**Edm.String**</span><span class="sxs-lookup"><span data-stu-id="9a003-1253">**Edm.String**</span></span>                   | <span data-ttu-id="9a003-1254">包含字符数据。</span><span class="sxs-lookup"><span data-stu-id="9a003-1254">Contains character data.</span></span>                                   | <span data-ttu-id="9a003-1255">Unicode、FixedLength、MaxLength、Collation、Precision、Nullable、Default</span><span class="sxs-lookup"><span data-stu-id="9a003-1255">Unicode, FixedLength, MaxLength, Collation, Precision, Nullable, Default</span></span> |
| <span data-ttu-id="9a003-1256">**Edm.Time**</span><span class="sxs-lookup"><span data-stu-id="9a003-1256">**Edm.Time**</span></span>                     | <span data-ttu-id="9a003-1257">包含当天的时间。</span><span class="sxs-lookup"><span data-stu-id="9a003-1257">Contains a time of day.</span></span>                                    | <span data-ttu-id="9a003-1258">Precision、Nullable、Default</span><span class="sxs-lookup"><span data-stu-id="9a003-1258">Precision, Nullable, Default</span></span>                                             |
| <span data-ttu-id="9a003-1259">**Edm.Geography**</span><span class="sxs-lookup"><span data-stu-id="9a003-1259">**Edm.Geography**</span></span>                |                                                            | <span data-ttu-id="9a003-1260">可以为 null，默认的 SRID</span><span class="sxs-lookup"><span data-stu-id="9a003-1260">Nullable, Default, SRID</span></span>                                                  |
| <span data-ttu-id="9a003-1261">**Edm.GeographyPoint**</span><span class="sxs-lookup"><span data-stu-id="9a003-1261">**Edm.GeographyPoint**</span></span>           |                                                            | <span data-ttu-id="9a003-1262">可以为 null，默认的 SRID</span><span class="sxs-lookup"><span data-stu-id="9a003-1262">Nullable, Default, SRID</span></span>                                                  |
| <span data-ttu-id="9a003-1263">**Edm.GeographyLineString**</span><span class="sxs-lookup"><span data-stu-id="9a003-1263">**Edm.GeographyLineString**</span></span>      |                                                            | <span data-ttu-id="9a003-1264">可以为 null，默认的 SRID</span><span class="sxs-lookup"><span data-stu-id="9a003-1264">Nullable, Default, SRID</span></span>                                                  |
| <span data-ttu-id="9a003-1265">**Edm.GeographyPolygon**</span><span class="sxs-lookup"><span data-stu-id="9a003-1265">**Edm.GeographyPolygon**</span></span>         |                                                            | <span data-ttu-id="9a003-1266">可以为 null，默认的 SRID</span><span class="sxs-lookup"><span data-stu-id="9a003-1266">Nullable, Default, SRID</span></span>                                                  |
| <span data-ttu-id="9a003-1267">**Edm.GeographyMultiPoint**</span><span class="sxs-lookup"><span data-stu-id="9a003-1267">**Edm.GeographyMultiPoint**</span></span>      |                                                            | <span data-ttu-id="9a003-1268">可以为 null，默认的 SRID</span><span class="sxs-lookup"><span data-stu-id="9a003-1268">Nullable, Default, SRID</span></span>                                                  |
| <span data-ttu-id="9a003-1269">**Edm.GeographyMultiLineString**</span><span class="sxs-lookup"><span data-stu-id="9a003-1269">**Edm.GeographyMultiLineString**</span></span> |                                                            | <span data-ttu-id="9a003-1270">可以为 null，默认的 SRID</span><span class="sxs-lookup"><span data-stu-id="9a003-1270">Nullable, Default, SRID</span></span>                                                  |
| <span data-ttu-id="9a003-1271">**Edm.GeographyMultiPolygon**</span><span class="sxs-lookup"><span data-stu-id="9a003-1271">**Edm.GeographyMultiPolygon**</span></span>    |                                                            | <span data-ttu-id="9a003-1272">可以为 null，默认的 SRID</span><span class="sxs-lookup"><span data-stu-id="9a003-1272">Nullable, Default, SRID</span></span>                                                  |
| <span data-ttu-id="9a003-1273">**Edm.GeographyCollection**</span><span class="sxs-lookup"><span data-stu-id="9a003-1273">**Edm.GeographyCollection**</span></span>      |                                                            | <span data-ttu-id="9a003-1274">可以为 null，默认的 SRID</span><span class="sxs-lookup"><span data-stu-id="9a003-1274">Nullable, Default, SRID</span></span>                                                  |
| <span data-ttu-id="9a003-1275">**Edm.Geometry**</span><span class="sxs-lookup"><span data-stu-id="9a003-1275">**Edm.Geometry**</span></span>                 |                                                            | <span data-ttu-id="9a003-1276">可以为 null，默认的 SRID</span><span class="sxs-lookup"><span data-stu-id="9a003-1276">Nullable, Default, SRID</span></span>                                                  |
| <span data-ttu-id="9a003-1277">**Edm.GeometryPoint**</span><span class="sxs-lookup"><span data-stu-id="9a003-1277">**Edm.GeometryPoint**</span></span>            |                                                            | <span data-ttu-id="9a003-1278">可以为 null，默认的 SRID</span><span class="sxs-lookup"><span data-stu-id="9a003-1278">Nullable, Default, SRID</span></span>                                                  |
| <span data-ttu-id="9a003-1279">**Edm.GeometryLineString**</span><span class="sxs-lookup"><span data-stu-id="9a003-1279">**Edm.GeometryLineString**</span></span>       |                                                            | <span data-ttu-id="9a003-1280">可以为 null，默认的 SRID</span><span class="sxs-lookup"><span data-stu-id="9a003-1280">Nullable, Default, SRID</span></span>                                                  |
| <span data-ttu-id="9a003-1281">**Edm.GeometryPolygon**</span><span class="sxs-lookup"><span data-stu-id="9a003-1281">**Edm.GeometryPolygon**</span></span>          |                                                            | <span data-ttu-id="9a003-1282">可以为 null，默认的 SRID</span><span class="sxs-lookup"><span data-stu-id="9a003-1282">Nullable, Default, SRID</span></span>                                                  |
| <span data-ttu-id="9a003-1283">**Edm.GeometryMultiPoint**</span><span class="sxs-lookup"><span data-stu-id="9a003-1283">**Edm.GeometryMultiPoint**</span></span>       |                                                            | <span data-ttu-id="9a003-1284">可以为 null，默认的 SRID</span><span class="sxs-lookup"><span data-stu-id="9a003-1284">Nullable, Default, SRID</span></span>                                                  |
| <span data-ttu-id="9a003-1285">**Edm.GeometryMultiLineString**</span><span class="sxs-lookup"><span data-stu-id="9a003-1285">**Edm.GeometryMultiLineString**</span></span>  |                                                            | <span data-ttu-id="9a003-1286">可以为 null，默认的 SRID</span><span class="sxs-lookup"><span data-stu-id="9a003-1286">Nullable, Default, SRID</span></span>                                                  |
| <span data-ttu-id="9a003-1287">**Edm.GeometryMultiPolygon**</span><span class="sxs-lookup"><span data-stu-id="9a003-1287">**Edm.GeometryMultiPolygon**</span></span>     |                                                            | <span data-ttu-id="9a003-1288">可以为 null，默认的 SRID</span><span class="sxs-lookup"><span data-stu-id="9a003-1288">Nullable, Default, SRID</span></span>                                                  |
| <span data-ttu-id="9a003-1289">**Edm.GeometryCollection**</span><span class="sxs-lookup"><span data-stu-id="9a003-1289">**Edm.GeometryCollection**</span></span>       |                                                            | <span data-ttu-id="9a003-1290">可以为 null，默认的 SRID</span><span class="sxs-lookup"><span data-stu-id="9a003-1290">Nullable, Default, SRID</span></span>                                                  |

## <a name="facets-csdl"></a><span data-ttu-id="9a003-1291">方面 (CSDL)</span><span class="sxs-lookup"><span data-stu-id="9a003-1291">Facets (CSDL)</span></span>

<span data-ttu-id="9a003-1292">以概念架构定义语言 (CSDL) 表示的方面表示对于实体类型和复杂类型的属性的约束。</span><span class="sxs-lookup"><span data-stu-id="9a003-1292">Facets in conceptual schema definition language (CSDL) represent constraints on properties of entity types and complex types.</span></span> <span data-ttu-id="9a003-1293">方面作为 XML 特性出现在以下 CSDL 元素上：</span><span class="sxs-lookup"><span data-stu-id="9a003-1293">Facets appear as XML attributes on the following CSDL elements:</span></span>

-   <span data-ttu-id="9a003-1294">属性</span><span class="sxs-lookup"><span data-stu-id="9a003-1294">Property</span></span>
-   <span data-ttu-id="9a003-1295">TypeRef</span><span class="sxs-lookup"><span data-stu-id="9a003-1295">TypeRef</span></span>
-   <span data-ttu-id="9a003-1296">参数</span><span class="sxs-lookup"><span data-stu-id="9a003-1296">Parameter</span></span>

<span data-ttu-id="9a003-1297">下表描述了 CSDL 中支持的方面。</span><span class="sxs-lookup"><span data-stu-id="9a003-1297">The following table describes the facets that are supported in CSDL.</span></span> <span data-ttu-id="9a003-1298">所有方面都是可选的。</span><span class="sxs-lookup"><span data-stu-id="9a003-1298">All facets are optional.</span></span> <span data-ttu-id="9a003-1299">从概念模型生成数据库时，将使用实体框架的下面列出一些方面。</span><span class="sxs-lookup"><span data-stu-id="9a003-1299">Some facets listed below are used by the Entity Framework when generating a database from a conceptual model.</span></span>

> [!NOTE]
> <span data-ttu-id="9a003-1300">有关概念模型中的数据类型的信息，请参阅概念模型类型 (CSDL)。</span><span class="sxs-lookup"><span data-stu-id="9a003-1300">For information about data types in a conceptual model, see Conceptual Model Types (CSDL).</span></span>

| <span data-ttu-id="9a003-1301">方面</span><span class="sxs-lookup"><span data-stu-id="9a003-1301">Facet</span></span>               | <span data-ttu-id="9a003-1302">描述</span><span class="sxs-lookup"><span data-stu-id="9a003-1302">Description</span></span>                                                                                                                                                                                                                                                   | <span data-ttu-id="9a003-1303">适用对象</span><span class="sxs-lookup"><span data-stu-id="9a003-1303">Applies to</span></span>                                                                                                                                                                                                                                                                                                                                                                           | <span data-ttu-id="9a003-1304">用于生成数据库</span><span class="sxs-lookup"><span data-stu-id="9a003-1304">Used for the database generation</span></span> | <span data-ttu-id="9a003-1305">由运行时使用</span><span class="sxs-lookup"><span data-stu-id="9a003-1305">Used by the runtime</span></span> |
|:--------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:---------------------------------|:--------------------|
| <span data-ttu-id="9a003-1306">**排序规则**</span><span class="sxs-lookup"><span data-stu-id="9a003-1306">**Collation**</span></span>       | <span data-ttu-id="9a003-1307">指定在对属性值执行比较和排序操作时要使用的排序序列。</span><span class="sxs-lookup"><span data-stu-id="9a003-1307">Specifies the collating sequence (or sorting sequence) to be used when performing comparison and ordering operations on values of the property.</span></span>                                                                                                               | <span data-ttu-id="9a003-1308">**Edm.String**</span><span class="sxs-lookup"><span data-stu-id="9a003-1308">**Edm.String**</span></span>                                                                                                                                                                                                                                                                                                                                                                       | <span data-ttu-id="9a003-1309">是</span><span class="sxs-lookup"><span data-stu-id="9a003-1309">Yes</span></span>                              | <span data-ttu-id="9a003-1310">否</span><span class="sxs-lookup"><span data-stu-id="9a003-1310">No</span></span>                  |
| <span data-ttu-id="9a003-1311">**ConcurrencyMode**</span><span class="sxs-lookup"><span data-stu-id="9a003-1311">**ConcurrencyMode**</span></span> | <span data-ttu-id="9a003-1312">表示应使用属性的值来进行开放式并发检查。</span><span class="sxs-lookup"><span data-stu-id="9a003-1312">Indicates that the value of the property should be used for optimistic concurrency checks.</span></span>                                                                                                                                                                    | <span data-ttu-id="9a003-1313">所有**EDMSimpleType**属性</span><span class="sxs-lookup"><span data-stu-id="9a003-1313">All **EDMSimpleType** properties</span></span>                                                                                                                                                                                                                                                                                                                                                     | <span data-ttu-id="9a003-1314">否</span><span class="sxs-lookup"><span data-stu-id="9a003-1314">No</span></span>                               | <span data-ttu-id="9a003-1315">是</span><span class="sxs-lookup"><span data-stu-id="9a003-1315">Yes</span></span>                 |
| <span data-ttu-id="9a003-1316">**默认**</span><span class="sxs-lookup"><span data-stu-id="9a003-1316">**Default**</span></span>         | <span data-ttu-id="9a003-1317">如果在安装时未提供值，则指定属性的默认值。</span><span class="sxs-lookup"><span data-stu-id="9a003-1317">Specifies the default value of the property if no value is supplied upon instantiation.</span></span>                                                                                                                                                                       | <span data-ttu-id="9a003-1318">所有**EDMSimpleType**属性</span><span class="sxs-lookup"><span data-stu-id="9a003-1318">All **EDMSimpleType** properties</span></span>                                                                                                                                                                                                                                                                                                                                                     | <span data-ttu-id="9a003-1319">是</span><span class="sxs-lookup"><span data-stu-id="9a003-1319">Yes</span></span>                              | <span data-ttu-id="9a003-1320">是</span><span class="sxs-lookup"><span data-stu-id="9a003-1320">Yes</span></span>                 |
| <span data-ttu-id="9a003-1321">**FixedLength**</span><span class="sxs-lookup"><span data-stu-id="9a003-1321">**FixedLength**</span></span>     | <span data-ttu-id="9a003-1322">指定属性值的长度是否可变。</span><span class="sxs-lookup"><span data-stu-id="9a003-1322">Specifies whether the length of the property value can vary.</span></span>                                                                                                                                                                                                  | <span data-ttu-id="9a003-1323">**Edm.Binary**， **Edm.String**</span><span class="sxs-lookup"><span data-stu-id="9a003-1323">**Edm.Binary**, **Edm.String**</span></span>                                                                                                                                                                                                                                                                                                                                                       | <span data-ttu-id="9a003-1324">是</span><span class="sxs-lookup"><span data-stu-id="9a003-1324">Yes</span></span>                              | <span data-ttu-id="9a003-1325">否</span><span class="sxs-lookup"><span data-stu-id="9a003-1325">No</span></span>                  |
| <span data-ttu-id="9a003-1326">**MaxLength**</span><span class="sxs-lookup"><span data-stu-id="9a003-1326">**MaxLength**</span></span>       | <span data-ttu-id="9a003-1327">指定属性值的最大长度。</span><span class="sxs-lookup"><span data-stu-id="9a003-1327">Specifies the maximum length of the property value.</span></span>                                                                                                                                                                                                           | <span data-ttu-id="9a003-1328">**Edm.Binary**， **Edm.String**</span><span class="sxs-lookup"><span data-stu-id="9a003-1328">**Edm.Binary**, **Edm.String**</span></span>                                                                                                                                                                                                                                                                                                                                                       | <span data-ttu-id="9a003-1329">是</span><span class="sxs-lookup"><span data-stu-id="9a003-1329">Yes</span></span>                              | <span data-ttu-id="9a003-1330">否</span><span class="sxs-lookup"><span data-stu-id="9a003-1330">No</span></span>                  |
| <span data-ttu-id="9a003-1331">**可以为 null**</span><span class="sxs-lookup"><span data-stu-id="9a003-1331">**Nullable**</span></span>        | <span data-ttu-id="9a003-1332">指定属性是否可以具有**null**值。</span><span class="sxs-lookup"><span data-stu-id="9a003-1332">Specifies whether the property can have a **null** value.</span></span>                                                                                                                                                                                                     | <span data-ttu-id="9a003-1333">所有**EDMSimpleType**属性</span><span class="sxs-lookup"><span data-stu-id="9a003-1333">All **EDMSimpleType** properties</span></span>                                                                                                                                                                                                                                                                                                                                                     | <span data-ttu-id="9a003-1334">是</span><span class="sxs-lookup"><span data-stu-id="9a003-1334">Yes</span></span>                              | <span data-ttu-id="9a003-1335">是</span><span class="sxs-lookup"><span data-stu-id="9a003-1335">Yes</span></span>                 |
| <span data-ttu-id="9a003-1336">**精度**</span><span class="sxs-lookup"><span data-stu-id="9a003-1336">**Precision**</span></span>       | <span data-ttu-id="9a003-1337">类型的属性**十进制**，指定属性值可以具有的位数。</span><span class="sxs-lookup"><span data-stu-id="9a003-1337">For properties of type **Decimal**, specifies the number of digits a property value can have.</span></span> <span data-ttu-id="9a003-1338">类型的属性**时间**， **DateTime**，并**DateTimeOffset**，指定属性值的秒小数部分的位数。</span><span class="sxs-lookup"><span data-stu-id="9a003-1338">For properties of type **Time**, **DateTime**, and **DateTimeOffset**, specifies the number of digits for the fractional part of seconds of the property value.</span></span> | <span data-ttu-id="9a003-1339">**Edm.DateTime**， **Edm.DateTimeOffset**， **Edm.Decimal**， **Edm.Time**</span><span class="sxs-lookup"><span data-stu-id="9a003-1339">**Edm.DateTime**, **Edm.DateTimeOffset**, **Edm.Decimal**, **Edm.Time**</span></span>                                                                                                                                                                                                                                                                                                              | <span data-ttu-id="9a003-1340">是</span><span class="sxs-lookup"><span data-stu-id="9a003-1340">Yes</span></span>                              | <span data-ttu-id="9a003-1341">否</span><span class="sxs-lookup"><span data-stu-id="9a003-1341">No</span></span>                  |
| <span data-ttu-id="9a003-1342">缩放</span><span class="sxs-lookup"><span data-stu-id="9a003-1342">**Scale**</span></span>           | <span data-ttu-id="9a003-1343">指定属性值小数点右侧的位数。</span><span class="sxs-lookup"><span data-stu-id="9a003-1343">Specifies the number of digits to the right of the decimal point for the property value.</span></span>                                                                                                                                                                      | <span data-ttu-id="9a003-1344">**Edm.Decimal**</span><span class="sxs-lookup"><span data-stu-id="9a003-1344">**Edm.Decimal**</span></span>                                                                                                                                                                                                                                                                                                                                                                      | <span data-ttu-id="9a003-1345">是</span><span class="sxs-lookup"><span data-stu-id="9a003-1345">Yes</span></span>                              | <span data-ttu-id="9a003-1346">否</span><span class="sxs-lookup"><span data-stu-id="9a003-1346">No</span></span>                  |
| <span data-ttu-id="9a003-1347">**SRID**</span><span class="sxs-lookup"><span data-stu-id="9a003-1347">**SRID**</span></span>            | <span data-ttu-id="9a003-1348">指定空间系统引用系统 id。</span><span class="sxs-lookup"><span data-stu-id="9a003-1348">Specifies the Spatial System Reference System ID.</span></span> <span data-ttu-id="9a003-1349">有关详细信息，请参阅[SRID](http://en.wikipedia.org/wiki/SRID)并[SRID (SQL Server)](https://msdn.microsoft.com/library/bb964707.aspx)。</span><span class="sxs-lookup"><span data-stu-id="9a003-1349">For more information, see [SRID](http://en.wikipedia.org/wiki/SRID) and [SRID (SQL Server)](https://msdn.microsoft.com/library/bb964707.aspx).</span></span>                                                              | <span data-ttu-id="9a003-1350">**Edm.Geography、 Edm.GeographyPoint、 Edm.GeographyLineString、 Edm.GeographyPolygon、 Edm.GeographyMultiPoint、 Edm.GeographyMultiLineString、 Edm.GeographyMultiPolygon、 Edm.GeographyCollection、 Edm.Geometry、 Edm.GeometryPoint，Edm.GeometryLineString、 Edm.GeometryPolygon、 Edm.GeometryMultiPoint、 Edm.GeometryMultiLineString、 Edm.GeometryMultiPolygon、 Edm.GeometryCollection**</span><span class="sxs-lookup"><span data-stu-id="9a003-1350">**Edm.Geography, Edm.GeographyPoint, Edm.GeographyLineString, Edm.GeographyPolygon, Edm.GeographyMultiPoint, Edm.GeographyMultiLineString, Edm.GeographyMultiPolygon, Edm.GeographyCollection, Edm.Geometry, Edm.GeometryPoint, Edm.GeometryLineString, Edm.GeometryPolygon, Edm.GeometryMultiPoint, Edm.GeometryMultiLineString, Edm.GeometryMultiPolygon, Edm.GeometryCollection**</span></span> | <span data-ttu-id="9a003-1351">否</span><span class="sxs-lookup"><span data-stu-id="9a003-1351">No</span></span>                               | <span data-ttu-id="9a003-1352">是</span><span class="sxs-lookup"><span data-stu-id="9a003-1352">Yes</span></span>                 |
| <span data-ttu-id="9a003-1353">**Unicode**</span><span class="sxs-lookup"><span data-stu-id="9a003-1353">**Unicode**</span></span>         | <span data-ttu-id="9a003-1354">指示是否将属性值存储为 Unicode。</span><span class="sxs-lookup"><span data-stu-id="9a003-1354">Indicates whether the property value is stored as Unicode.</span></span>                                                                                                                                                                                                    | <span data-ttu-id="9a003-1355">**Edm.String**</span><span class="sxs-lookup"><span data-stu-id="9a003-1355">**Edm.String**</span></span>                                                                                                                                                                                                                                                                                                                                                                       | <span data-ttu-id="9a003-1356">是</span><span class="sxs-lookup"><span data-stu-id="9a003-1356">Yes</span></span>                              | <span data-ttu-id="9a003-1357">是</span><span class="sxs-lookup"><span data-stu-id="9a003-1357">Yes</span></span>                 |

>[!NOTE]
> <span data-ttu-id="9a003-1358">当从概念模型生成数据库，生成数据库向导将识别的值**StoreGeneratedPattern**特性，可以在**属性**元素是否在下面的示例命名空间： http://schemas.microsoft.com/ado/2009/02/edm/annotation 。</span><span class="sxs-lookup"><span data-stu-id="9a003-1358">When generating a database from a conceptual model, the Generate Database Wizard will recognize the value of the **StoreGeneratedPattern** attribute on a **Property** element if it is in the following namespace: http://schemas.microsoft.com/ado/2009/02/edm/annotation.</span></span> <span data-ttu-id="9a003-1359">支持的属性值为**标识**并**计算**。</span><span class="sxs-lookup"><span data-stu-id="9a003-1359">The supported values for the attribute are **Identity** and **Computed**.</span></span> <span data-ttu-id="9a003-1360">值为**标识**将生成具有在数据库中生成的标识值的数据库列。</span><span class="sxs-lookup"><span data-stu-id="9a003-1360">A value of **Identity** will produce a database column with an identity value that is generated in the database.</span></span> <span data-ttu-id="9a003-1361">值为**计算**将生成具有在数据库中计算的值的列。</span><span class="sxs-lookup"><span data-stu-id="9a003-1361">A value of **Computed** will produce a column with a value that is computed in the database.</span></span>

### <a name="example"></a><span data-ttu-id="9a003-1362">示例</span><span class="sxs-lookup"><span data-stu-id="9a003-1362">Example</span></span>

<span data-ttu-id="9a003-1363">下面的示例演示了应用于实体类型的属性的方面：</span><span class="sxs-lookup"><span data-stu-id="9a003-1363">The following example shows facets applied to the properties of an entity type:</span></span>

``` xml
 <EntityType Name="Product">
   <Key>
     <PropertyRef Name="ProductId" />
   </Key>
   <Property Type="Int32"
             Name="ProductId" Nullable="false"
             a:StoreGeneratedPattern="Identity"
    xmlns:a="http://schemas.microsoft.com/ado/2009/02/edm/annotation" />
   <Property Type="String"
             Name="ProductName"
             Nullable="false"
             MaxLength="50" />
   <Property Type="String"
             Name="Location"
             Nullable="true"
             MaxLength="25" />
 </EntityType>
```