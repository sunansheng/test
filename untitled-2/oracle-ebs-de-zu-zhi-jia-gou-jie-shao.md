# ORACLE EBS的组织架构介绍



## 一、Oracle EBS的组织架构

软件系统的“组织设置”必须以业务流程运作为核心，要求尽可能简单并保持相对稳定，在公司（人员）规模扩大的过程中具有延续性与继承性。 ORACLE EBS系统组织划分为“业务组（Business Group）、法律实体（Legal Entity）、业务实体（Operating Unit）、库存组织（Inventory Org）”等，与企业实际的行政组织不是完全等同的概念，而是基于系统业务运作需要而设定的。

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/38bfcc96-c38b-493e-863a-b0c037d59d85/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/38bfcc96-c38b-493e-863a-b0c037d59d85/Untitled.png)

## **二、业务组（BG，Business Group）**

“业务组”的概念可以视同企业的“集团”概念，但不同的是一个企业在系统中可以设置多个“业务组（集团）”。 通常对于一个企业来说，系统中有一个“业务组”就够了，这表示企业就是一个“集团公司”。而对于某些业务“多元化”的特大型公司（如跨国公司），则可能需要在系统中设置多个“业务组”，表示企业由多个“集团公司”组成。 业务组设置是系统组织设置的第一步，是最高层级的组织形态，但它主要是与人力资源信息的分隔有关，即“人员信息”的设置在一个BG范围内是由各业务模块共享的（如果需要）。一旦系统设置的用户名（User）被与“人员”（Employee）关联，无论使用什么“责任”进入系统，都会定位至一个确定的BG中，任何责任在任意时刻只能关联一个BG。EBS安装好后，系统里面已经预置了一个名为“Setup Business Group”的“初始业务组”。

## **三、法律实体（LE，Legal Entity）**

对应实际的按国家法律法规注册的法人公司。 R12中在定义“分类帐”时的“会计科目设置管理器”WEB中定义并分配法人实体LE。一个分类帐设置（主辅分类帐）可以添加多个LE，但每个LE只能具有一个分类帐设置。

业务实体（OU，Operating Unit）是EBS系统组织设置的重点也是难点之一。它与法人主体LE本身没有必然的关系，与会计科目弹性域结构中的“公司段”也没有直接关系。从企业实际业务管理需要的角度去看，业务实体OU可以看作是在系统中按照业务的相似性，把多个不同公司（包括LE）的业务处理过程及数据划分成相对独立的“管理单元”。在每个管理单元内部，各公司的业务运作共享相关数据并执行统一的业务策略。

## **四、库存组织（Inventory Org）**

不是真实业务的“仓库管理部门”那么简单，它除了是有“物料接收与发出”等业务功能之外，更重要的是，它还是EBS系统有关计划（MPS主生产计划/MRP物料需求计划）、在制品管理（WIP）、物料清单（BOM）等模块业务功能的操作与管理平台。 在EBS中还有两个组织概念“MRP组织、WIP组织”，它们实际是必须构建于库存组织之上的组织概念，表示该库存组织还可以进行MRP或WIP的功能。系统之所以如此处理，主要是为了控制某些INV不能做MRP或WIP而已，因为基于物料接收或发出需要所设定的INV数量可能比较多。对于绝大多数基于库存组织INV的业务功能（个别除外），系统用户在做业务操作时，均必须首先进行INV的选择切换，以便进入确定的INV上下文环境。库存组织的作用是如此基础，以至于EBS的相关文档在提及组织（Org）概念时，如果未作特别说明，默认就是指INV组织。 一个库存组织INV只能属于一个确定的帐套SOB、一个确定的法人实体LE、一个确定的业务实体OU。反之，一个“帐套/法人实体/业务实体”组合则可以有多个库存组织INV。

## **五、HR组织**

系统的HR组织设置是与HRM模块的相关业务处理功能相关，与核心业务、财务处理功能关系不大

## **六、资产组织**

“资产组织”的设置，它是在企业需使用到资产管理模块FA时才涉及到。“资产组织”实际上是所谓“资产账簿”的代名词，它只是表示有关资产信息的一个数据维度，作用主要在于分隔数据范围

## **七、多组织访问控制**

EBS组织设置界面中，所谓的组织“类型”（Type）划分仅是基于组织自身的统计分析工作需要而定义的一个“维度”，例如“公司总部、产品线”等等，并不影响系统的业务处理功能。真正起作用的是设置界面中的“组织分类”，系统预置的组织分类LOV除了上述“业务组、法律实体、业务实体、库存组织”等之外，还有诸如“资产组织、运营公司、雇主”等等选项。在EBS系统中各应用模块所具有的业务处理功能通常需构建在一个确定的“组织分类”之上，“组织”是相关业务处理功能的平台，企业是否需要作相关组织分类设置、如何设置，取决于企业所需要使用到的应用模块功能。ORACLR系统通过“组织”所具有的“层次结构”（Hierarchy）概念来达到“多组织访问”权限的控制功能。这里的组织“层次结构”与真实企业的行政管理组织层次结构没有直接关系（尽管可能有所参考），它只是企业根据某种需要（如权限管理控制、数据统计汇报等）而人为设定的一个“层次结构”，例如将系统中已经设置的任意数量的“业务实体”或“库存组织”等组织，人为地设定一个具有上下级关系、自顶向下的金字塔形多层结构。

## **八、配置文件**

所有定义的“安全性配置文件”构成系统多组织接入控制参数“MO：安全性配置文件”的LOV。EBS 通过“MO：业务实体”、“MO：安全性配置文件”、“MO：默认业务实体”这三个系统配置文件的共同作用，实现所谓“多组织访问”控制功能。 对于“MO：业务实体”：在R12中， 一旦设定“MO：安全性配置文件”，则此配置文件失效而不起作用。 对于“MO：安全性配置文件”，：在R12中，该参数如果不设定，则必须设定“MO：业务实体”参数；一旦该参数被设定，则就起决定作用，系统主要依赖其实现“多组织访问”控制功能。 对于“MO：默认业务实体”： 在R12中，随“MO：安全配置文件”起作用后才起作用，其LOV是所有已定义OU，但如果设定值不在“MO：安全配置文件”所选择的“组织层次架构”的范围内，则仍不起作用（即在与OU相关诸如PO、OM等的FORM界面，OU字段的默认值仍然为空）。 ORACLE强调其“多组织接入MOAC”功能主要是针对业务实体OU而言。库存组织的访问是在“组织访问”控制功能中，专门设定“库存组织”与“责任”的关联性 。EBS系统通过“弹性域段值安全性”、“帐套/分类帐安全性”、“多组织访问控制（MOAC）”、“库存组织访问控制”等多维度、多方面的组合系统设置，提供了灵活、方便的用户权限管理功能，理清并掌握它们的复杂关系是系统实施的一项重要基础性工作。

## 九、补充了解...

一般来说：一个公司下面有多个子公司，那么公司就是**LE（法人实体）**，子公司就是**balancing entity（平衡段）**，也就是一个利润中心。在设置组织的地方定义法人实体（LE），指定帐簿，然后把**子公司设置为业务实体（OU）**，指定法人，在定义会计科目表（COA）时给每个子公司设置一个平衡段值。法人本身可以为一个平衡段。

一般部门只是作为财务上一个成本中心来处理，子公司可以设置为一个业务实体（OU），每个子公司一个公司段，车间和仓库对应库存组织。 以下是提到的专业术语，现具体解释如下：

**帐套**

使用特定会计科目表（COA）、记帐本位币、和会计日历的财务报告实体。如果以上三个要素中有一个不同，就必须建立不同的帐套。Oracle总帐按帐套设置业务信息（日记帐分录和余额）的安全性控制。

**组织**

使用“定义组织”窗口定义的任何实体都称为“组织”，“组织”有不同的分类， 对组织进行分类决定了组织的类型和用途。组织的类型有：业务组\(Business Group\)、法人实体\(Legal Entity\)、业务实体\(Operating Unit\)、库存组织\(Inventory Organization\)、和人事组织 \(HR Organization\) 。一个组织可以指定为多个分类，如某个组织可能是法人组织，同时也是业务实体、库存组织和资产组织。

**业务组**

业务组代表结构的最高层如企业合并或公司的最高部门，当前的业务组除用于隔离人事信息之外没有其他目的。在任何模块只能看到核算单位所属业务组的雇员名单。多个法人实体可以指定到同一业务组。

**法人实体**

代表要提交财务和税务报表的法人公司。指定税务登记号和其他法人信息到此类型的组织，法人组织要指定其会计核算的帐套。

**业务实体**

使用Oracle应收、Oracle应付、Oracle销售、Oracle采购、Oracle现金管理和Oracle项目会计等模块的独立会计核算实体。任何独立核算的组织均是已指定法人实体的“业务实体”。在以上的模块中，业务信息按“业务实体”设置安全性，有些信息是共享的。

**库存组织**

使用库存组织跟踪库存业务和余额，和\(或者\)制造商分销商品。Oracle库存、Oracle物料单、Oracle工艺设计、Oracle在产品、Oracle主生产计划/MRP、Oracle能力、Oracle质量、Oracle成本管理、Oracle供应链计划和Oracle采购\(接收功能\)均 按库存组织设立安全性控制。库存组织可以指定到同一帐套下的任何业务实体，库存组织与帐套之间的关系仅限于财务核算目的，库存组织决定了销售和采购模块可 获得的物料\(Items\)。

**人事组织**

人事组织仅用于Oracle HR 和 Oracle项目会计模块，对财务和制造模块没有任何影响，使之能适应复杂的组织结构，简化业务经营的组织结构。

帐套的三要素是会计科目弹性域结构、币种和日历，如果多个法人这些结构相同，那多个法人共享一个帐套是可以的。

业务组是Oracle多组织架构的一个组织形式，oracle系统默认有一个业务组：setup business group，一般来说只要应用这个默认的业务组就可以了。对于跨国公司来说，譬如IBM中国和IBM香港想共用一套系统，那么就需要设置两个业务组：IBM中国业务组和IBM香港业务组。

我理解的法人就是需要独立向社会公布财务报告的实体，譬如上市公司，那么上市公司的子公司、甚至是分公司就可以设置为业务实体（OU）。

### 表关系

**LE**:法人实体（LEGAL ENTITY）

**OU**:业务实体（OPERATING UNIT）

**LEDGER**:分类账（LEDGER），即11i里帐套（SOB）的概念。

**LE、OU 是组织架构，Ledger和SLA是财务架构**，SLA是把OU中的交易分录到不同的Ledger上的一种方式。

在定义ledger的时候可以为一个ledger分配多个LE，一个LE也可以有多个ledger（一个主分类账，多个辅助分类账），所以，**理论上存在LE和Ledger多对多的关系**。

GL\_LEDGERS

分类账定义

GL\_LEDGER\_RELATIONSHIPS

分类账间关系

GL\_LEDGER\_CONFIGURATIONS

主分类账

GL\_LEDGER\_CONFIG\_DETAILS

主分类账配置明细信息，含LE、辅助分类账等设置

XLE\_ENTITY\_PROFILES

LE信息

GL\_LEGAL\_ENTITIES\_BSVS

LE与公司段值集

**OU与LE/ledger对应关系:**

OU信息视图中有默认业务实体及分类账信息，即 HR\_OPERATING\_UNITS 中的 DEFAULT\_LEGAL\_CONTEXT\_ID 和 SET\_OF\_BOOKS\_ID:

**HR\_OPERATING\_UNITS.DEFAULT\_LEGAL\_CONTEXT\_ID = XLE\_ENTITY\_PROFILES.LEGAL\_ENTITY\_ID**

**HR\_OPERATING\_UNITS.SET\_OF\_BOOKS\_ID = GL\_LEDGERS.LEDGER\_ID**

**LE与ledger对应关系:**

关于LE与ledger的对应关系，oracle给出了一个视图:**GL\_LEDGER\_LE\_V**，关联关系可以在这个视图里找到

```text
SELECT lg.ledger_id
      ,lg.name                       ledger_name
      ,lg.short_name                 ledger_short_name
      ,cfgdet.object_id              legal_entity_id
      ,le.name                       legal_entity_name
      ,reg.location_id               location_id
      ,hrloctl.location_code         location_code
      ,hrloctl.description           location_description
      ,lg.ledger_category_code
      ,lg.currency_code
      ,lg.chart_of_accounts_id
      ,lg.period_set_name
      ,lg.accounted_period_type
      ,lg.sla_accounting_method_code
      ,lg.sla_accounting_method_type
      ,lg.bal_seg_value_option_code
      ,lg.bal_seg_column_name
      ,lg.bal_seg_value_set_id
      ,cfg.acctg_environment_code
      ,cfg.configuration_id
      ,rs.primary_ledger_id
      ,rs.relationship_enabled_flag
  FROM gl_ledger_config_details primdet
      ,gl_ledgers               lg
      ,gl_ledger_relationships  rs
      ,gl_ledger_configurations cfg
      ,gl_ledger_config_details cfgdet
      ,xle_entity_profiles      le
      ,xle_registrations        reg
      ,hr_locations_all_tl      hrloctl
 WHERE rs.application_id = 101
   AND ((rs.target_ledger_category_code = 'SECONDARY' AND rs.relationship_type_code <> 'NONE') OR
       (rs.target_ledger_category_code = 'PRIMARY' AND rs.relationship_type_code = 'NONE') OR
       (rs.target_ledger_category_code = 'ALC' AND rs.relationship_type_code IN ('JOURNAL', 'SUBLEDGER')))
   AND lg.ledger_id = rs.target_ledger_id
   AND lg.ledger_category_code = rs.target_ledger_category_code
   AND nvl(lg.complete_flag, 'Y') = 'Y'
   AND primdet.object_id = rs.primary_ledger_id
   AND primdet.object_type_code = 'PRIMARY'
   AND primdet.setup_step_code = 'NONE'
   AND cfg.configuration_id = primdet.configuration_id
   AND cfgdet.configuration_id(+) = cfg.configuration_id
   AND cfgdet.object_type_code(+) = 'LEGAL_ENTITY'
   AND le.legal_entity_id(+) = cfgdet.object_id
   AND reg.source_id(+) = cfgdet.object_id
   AND reg.source_table(+) = 'XLE_ENTITY_PROFILES'
   AND reg.identifying_flag(+) = 'Y'
   AND hrloctl.location_id(+) = reg.location_id
   AND hrloctl.language(+) = userenv('LANG');
```

