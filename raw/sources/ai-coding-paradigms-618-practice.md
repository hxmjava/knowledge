# 1个场景(618促销)5种范式(Spec/Vibe/Glue/TDD/Harness) ，企业级AI Coding经验分享(附代码示例)

- 来源：微信公众号「沐然云计算」
- 作者：吕昭波
- 发布日期：2026-05-10
- 原文链接：https://mp.weixin.qq.com/s/8dRi3pApghRhMtXh0HWmHg

---

## 核心观点速览

在618促销这样的大型项目中，我们通过实战验证了五种研发范式的价值，核心发现如下：

1. **范式无优劣，场景定选择**
   Spec Coding重文档、TDD重质量、Glue Coding重效率、Harness重交付、Vibe Coding重体验，没有绝对的好坏之分。

2. **资产复用是效率关键**
   复用春节促销和周年庆的Reference代码，618核心功能开发周期缩短60%，代码复用率达70%。

3. **规范先行保障质量**
   遵循AGENTS.md规范（命名、日志、异常处理），确保代码风格统一，降低维护成本。

4. **组合使用效果最佳**
   不同阶段采用不同范式：Spec Coding定需求、TDD保核心、Glue Coding提效率、Harness自动化、Vibe Coding优体验。

5. **PM角色随范式调整**
   Spec Coding中PM主导需求，TDD中PM关注验收标准，Vibe Coding中PM聚焦用户体验。

6. **文档参考各有侧重**
   需求文档对应Spec Coding，测试文档对应TDD，Reference代码对应Glue Coding，部署文档对应Harness，设计稿对应Vibe Coding。

## 一、项目背景：站在巨人的肩膀上

在开始618促销开发之前，我们团队已经积累了丰富的技术资产，这为我们选择不同研发范式提供了坚实基础。

### 1.1 已有代码资产（Reference）

我们整理了去年春节促销和周年庆活动的核心代码：

```
Reference/
├── SpringFestivalPromotionService.java  # 春节促销服务
│   ├── processOrder()          # 处理订单优惠
│   ├── applyFullReduction()    # 满减计算
│   ├── checkGiftEligibility()  # 赠品资格判断
│   └── applyPointsMultiplier() # 积分翻倍
├── AnniversaryCouponService.java       # 周年庆优惠券服务
│   ├── distributeCoupons()      # 发放优惠券
│   ├── determineCouponAmount()  # 按等级确定金额
│   └── batchDistribute()        # 批量发放
└── PromotionConfig.java                # 促销配置
    ├── springFestival           # 春节配置
    ├── anniversary              # 周年庆配置
    └── configMap                # 通用配置
```

### 1.2 研发规范（AGENTS.md）

项目已建立完善的研发规范：

| 规范类别 | 内容 |
|---------|------|
| 技术栈 | Spring Boot 2.7.18、MyBatis-Plus 3.5.3.1 |
| 代码规范 | 使用@Slf4j日志、统一异常处理、事务管理 |
| 命名规范 | Service接口名、VO/DTO命名规则 |
| 永久红线 | 禁止修改财务模块 |
| 验证命令 | Maven编译、JUnit测试、Checkstyle检查 |

### 1.3 项目架构信息

（图片略）

## 二、618大促需求分析

整个方案不涉及客户信息，所以，这些都是Mock数据，模拟促销信息。当然，为了更真实的Mock，还Mock了618促销需求讨论的邮件.md、会议纪要.md。

所以，在这里我们重点关注中间的逻辑，而非具体需求或者功能本身。

### 2.1 核心需求

基于现有资产，我们需要实现：

1. 优惠券系统：用户领取、使用优惠券（可复用周年庆代码）
2. 满减优惠：满300减50（可复用春节满减逻辑）
3. 限时抢购：新增功能
4. 积分翻倍：可复用春节积分逻辑

### 2.2 技术要求

- 高并发：支持每秒10万级请求
- 高可用：系统可用性99.9%以上
- 数据一致性：库存扣减、优惠券核销必须准确
- 快速迭代：两周内完成开发和测试

## 三、多种研发范式实战

### 3.1 Spec Coding：文档先行，规范驱动

**核心思想：** 先写完整的需求文档和设计规范，再严格按照文档进行代码实现。

**切入点：** 从需求分析开始，结合现有Reference代码，明确"做什么"和"怎么做"。

**实战过程：**

第一步：编写Spec文档（参考已有资产）

我们基于AGENTS.md规范编写了14份Spec文档：
- 01-Spec写作总则与文档编号索引.md
- 02-需求来源与采集记录.md
- 03-立项提案与范围说明.md
- ...
- 08-系统架构与技术选型.md → 参考现有架构设计
- 09-API接口规格.md → 参考AnniversaryCouponService
- 10-数据模型与存储规格.md → 参考现有表结构
- ...
- 14-需求追踪矩阵.md

第二步：识别可复用资产

| 需求 | 可复用资产 | 复用方式 |
|------|-----------|---------|
| 优惠券领取 | AnniversaryCouponService | 直接复用 |
| 满减计算 | SpringFestivalPromotionService | 修改阈值 |
| 积分翻倍 | SpringFestivalPromotionService | 直接复用 |

第三步：设计新增功能

限时抢购功能需要全新设计：
```json
// POST /api/promotion/flash-sale
{
  "productId": 1001,
  "userId": 12345,
  "quantity": 1
}
```

**关注点：**
- 需求明确：结合Reference明确需求边界
- 设计先行：先设计后开发，避免返工
- 可追溯性：每个需求都能追溯到文档
- 团队协作：文档作为团队沟通桥梁

**优点：** 需求清晰，减少歧义；设计严谨，架构清晰；可维护性强，便于后续迭代；适合大型团队协作。

**缺点：** 前期投入大，文档编写耗时；灵活性不足，需求变更成本高；不适合快速迭代场景。

### 3.2 基于Spec的TDD：测试先行，质量驱动

如果只是TDD，那么还是之前的TDD，如果基于Spec的TDD，会让TDD更严谨。

**核心思想：** 先写测试用例，再实现代码，确保代码可测试性和正确性。

**切入点：** 从测试场景出发，参考Reference代码定义"成功的标准"。

**实战过程：**

第一步：参考Reference编写测试用例

```java
@Test
void testReceiveCoupon_Success() {
    // 参考AnniversaryCouponService的发放逻辑
    UserCouponVO result = couponService.receiveCoupon(userId, couponId);
    assertEquals("AVAILABLE", result.getStatus());
}

@Test
void testFullReduction_618Rule() {
    // 618规则：满300减50（参考春节满500减100）
    BigDecimal total = BigDecimal.valueOf(700);
    BigDecimal discount = promotionService.applyFullReduction(total);
    assertEquals(BigDecimal.valueOf(100), discount); // 300*2=600，减100
}

@Test
void testFlashSale_Success() {
    // 新增限时抢购测试
    FlashSaleResult result = flashSaleService.purchase(userId, productId, 1);
    assertEquals("SUCCESS", result.getStatus());
}
```

第二步：运行测试（预期失败）
```
mvn test -pl order-service -Dtest=CouponServiceTest
```

第三步：实现代码（复用+新增）

```java
@Service
public class Promotion618Service {
    
    @Autowired
    private AnniversaryCouponService couponService; // 复用
    
    @Autowired
    private SpringFestivalPromotionService springService; // 复用
    
    @Transactional(rollbackFor = Exception.class)
    public PromotionResult processOrder(Long orderId) {
        Order order = orderMapper.selectById(orderId);
        
        // 复用春节满减逻辑，修改618阈值
        BigDecimal discount = applyFullReduction(order.getTotalAmount());
        order.setDiscountAmount(discount);
        
        // 复用周年庆优惠券逻辑
        if (order.getCouponId() != null) {
            couponService.validateAndUseCoupon(order.getUserId(), order.getCouponId());
        }
        
        // 新增：积分翻倍（复用春节逻辑）
        springService.applyPointsMultiplier(order.getUserId(), order.getTotalAmount());
        
        return convertToResult(order);
    }
    
    private BigDecimal applyFullReduction(BigDecimal totalAmount) {
        // 618规则：满300减50
        BigDecimal threshold = BigDecimal.valueOf(300);
        BigDecimal amount = BigDecimal.valueOf(50);
        int times = totalAmount.divide(threshold, RoundingMode.DOWN).intValue();
        return amount.multiply(BigDecimal.valueOf(times));
    }
}
```

**关注点：**
- 测试覆盖：确保核心逻辑有测试覆盖
- 可测试性：代码设计考虑可测试性
- 质量保障：测试驱动开发，代码质量高
- 重构安全：测试保障重构不破坏功能

**优点：** 代码质量高，测试覆盖充分；可测试性好，便于维护；重构安全，测试作为安全网；适合核心业务逻辑。

**缺点：** 开发周期较长；初期投入大；对测试人员要求高。

### 3.3 Glue Coding：复用先行，效率驱动

"天下文章一大抄"，就是说的Glue Coding。项目中已经有稳定的代码框架和模板了，就没必要让AI再重新生成一遍代码，重新生成一定带来更多隐患和检查代价。

**核心思想：** 优先复用现有代码和组件，快速拼接实现新功能。

**切入点：** 从Reference代码出发，寻找可复用的组件。

**实战过程：**

第一步：识别可复用组件

```java
@Component
public class PromotionComponentScanner {
    
    public Map<String, Object> scanReusableComponents() {
        Map<String, Object> components = new HashMap<>();
        
        // 扫描春节促销代码
        components.put("fullReduction", new SpringFestivalPromotionService());
        components.put("pointsMultiplier", new SpringFestivalPromotionService());
        
        // 扫描周年庆代码
        components.put("couponDistributor", new AnniversaryCouponService());
        components.put("levelCalculator", new AnniversaryCouponService());
        
        // 扫描配置
        components.put("config", new PromotionConfig());
        
        return components;
    }
}
```

第二步：组合复用组件

```java
@Service
public class Promotion618Service {
    
    @Autowired
    private AnniversaryCouponService couponService; // 直接注入
    
    @Autowired
    private PromotionConfig promotionConfig;
    
    @Value("${promotion.618.full-reduction.threshold:300}")
    private BigDecimal threshold;
    
    @Value("${promotion.618.full-reduction.amount:50}")
    private BigDecimal amount;
    
    @Transactional(rollbackFor = Exception.class)
    public PromotionResult processOrder(Long orderId) {
        Order order = orderMapper.selectById(orderId);
        
        // 复用春节满减逻辑（修改参数）
        BigDecimal discount = calculateDiscount(order.getTotalAmount());
        order.setDiscountAmount(discount);
        
        // 复用周年庆优惠券验证
        if (order.getCouponId() != null) {
            couponService.validateAndUseCoupon(order.getUserId(), order.getCouponId());
        }
        
        return convertToResult(order);
    }
    
    private BigDecimal calculateDiscount(BigDecimal totalAmount) {
        // 复用SpringFestivalPromotionService的计算逻辑
        int times = totalAmount.divide(threshold, RoundingMode.DOWN).intValue();
        return amount.multiply(BigDecimal.valueOf(times));
    }
}
```

第三步：配置618活动参数

```yaml
# application.yml
promotion:
  618:
    enabled: true
    start-time: 2026-06-01T00:00:00
    end-time: 2026-06-18T23:59:59
    full-reduction:
      threshold: 300
      amount: 50
```

**关注点：**
- 代码复用：最大化复用Reference代码
- 快速开发：缩短开发周期
- 一致性：保持代码风格与现有一致
- 配置化：可变参数外部配置

**优点：** 开发速度快（复用已有代码）；代码质量有保障（经过验证的代码）；代码一致性好；适合快速迭代。

**缺点：** 可能受限于现有代码结构；需要良好的代码资产积累；可能引入不必要的依赖。

### 3.4 Harness：自动化先行，交付驱动

整体是个框架，限制边界。

**核心思想：** 建立自动化的CI/CD流水线，实现从代码提交到生产部署的全流程自动化。

**切入点：** 从部署流程出发，结合现有基础设施构建自动化能力。

**实战过程：**

第一步：配置CI流水线（复用已有配置）

```yaml
stage:
  name: 构建阶段
type: CI
spec:
  codebase:
    repo: https://github.com/example/order-service
    branch: feature/618-promotion
  build:
    type: Maven
    spec:
      pomPath: pom.xml
      goals: clean package -DskipTests
  artifacts:
    - name: order-service.jar
      path: target/order-service-1.0.0.jar
```

第二步：配置CD流水线（参考现有部署规范）

```yaml
stage:
  name: 部署阶段
type: CD
spec:
  environment: 测试环境
  deploymentType: Kubernetes
  strategy:
    type: RollingUpdate
    spec:
      maxSurge: 25%
      maxUnavailable: 25%
  manifest:
    type: Helm
    spec:
      chartPath: charts/order-service
      values:
        replicaCount: 5
        env:
          - name: PROMOTION_ENABLED
            value: "true"
          - name: PROMOTION_THRESHOLD
            value: "300"
```

第三步：配置持续验证

```yaml
stage:
  name: 验证阶段
type: Verify
spec:
  duration: 30m
  metrics:
    - name: 响应时间
      query: avg(http_request_duration_seconds)
      threshold: 500ms
    - name: 错误率
      query: sum(http_requests_total{status=~"5..*"})/sum(http_requests_total)
      threshold: 5%
  onFailure:
    action: rollback
```

**关注点：**
- 自动化部署：代码提交自动触发部署
- 持续验证：部署后持续监控
- 智能回滚：自动检测问题并回滚
- 可观测性：实时监控和告警

**优点：** 部署效率高；可靠性强，自动回滚；可观测性好；适合持续交付。

**缺点：** 前期配置复杂；需要一定的DevOps能力；基础设施要求高。

### 3.5 Vibe Coding：体验先行，氛围驱动

没想到吧，Vibe Coding在企业场景也有用处的，有很大的作用。

**核心思想：** 通过快速原型验证用户体验和交互设计，强调情感化设计和用户感受。

**切入点：** 从用户体验出发，快速验证交互效果和视觉风格。

**实战过程：**

第一步：快速原型设计

```html
<!-- 618活动页快速原型 -->
<div class="promotion-page">
    <!-- 方案A：红色主色调 + 倒计时动画 -->
    <div class="theme-red">
        <div class="countdown">
            <span class="digit">0</span>
            <span class="digit">6</span>
            <span class="separator">:</span>
            <span class="digit">1</span>
            <span class="digit">8</span>
        </div>
    </div>
    
    <!-- 方案B：渐变紫 + 悬浮卡片效果 -->
    <div class="theme-purple">
        <div class="floating-card">
            <div class="coupon" @click="animateBounce">
                满300减50
            </div>
        </div>
    </div>
</div>
```

第二步：A/B测试验证

```javascript
// 多版本同时测试
const variants = ['theme-red', 'theme-purple', 'theme-minimal'];
const users = getUserSegment();

// 根据用户分组展示不同版本
const userVariant = variants[users.id % variants.length];
document.body.classList.add(userVariant);

// 收集用户行为数据
trackEvent('page_view', { variant: userVariant });
trackEvent('coupon_click', { variant: userVariant });
trackEvent('purchase', { variant: userVariant });
```

第三步：数据驱动优化

```javascript
// 分析各版本转化率
const results = analyzeVariants([
    { variant: 'theme-red', conversion: 32.5 },
    { variant: 'theme-purple', conversion: 38.2 },
    { variant: 'theme-minimal', conversion: 28.8 }
]);

// 选择最优方案
const bestVariant = results.sort((a, b) => b.conversion - a.conversion)[0];
console.log(`最优方案: ${bestVariant.variant}, 转化率: ${bestVariant.conversion}%`);
```

**关注点：**
- 用户体验：关注交互设计和视觉效果
- 情感化设计：通过微动画提升用户愉悦感
- 快速验证：A/B测试快速找到最优方案
- 数据驱动：基于用户行为数据优化

**优点：** 用户体验优先，转化率提升明显；快速试错，避免后期大规模返工；数据驱动决策，科学验证效果；适合重体验的促销活动场景。

**缺点：** 需要专门的设计团队支持；A/B测试需要一定的用户流量；可能过度关注视觉效果而忽视性能。

## 四、五种范式对比分析

### 4.1 对比表格

| 维度 | Spec Coding | TDD | Glue Coding | Harness | Vibe Coding |
|------|-------------|-----|-------------|---------|-------------|
| 核心思想 | 文档先行 | 测试先行 | 复用先行 | 自动化先行 | 体验先行 |
| 切入点 | 需求分析+Reference | 测试场景+Reference | Reference代码 | 部署流程+规范 | 用户体验 |
| 关注点 | 需求明确 | 代码质量 | 开发效率 | 交付可靠性 | 交互设计 |
| 开发速度 | 慢 | 中 | 快 | 快（部署） | 快（原型） |
| 代码质量 | 高（设计驱动） | 高（测试驱动） | 中（依赖复用） | 高（自动化保障） | 中（原型验证） |
| 可维护性 | 高 | 高 | 中 | 高 | 中 |
| 灵活性 | 低 | 中 | 高 | 中 | 高 |
| 团队规模 | 大型团队 | 中型团队 | 小型团队 | 任何规模 | 中小型团队 |
| 适用场景 | 大型项目 | 核心逻辑 | 快速迭代 | 持续交付 | 界面交互 |

### 4.2 适用场景分析

| 场景类型 | Spec Coding | TDD | Glue Coding | Harness | Vibe Coding |
|---------|-------------|-----|-------------|---------|-------------|
| 项目规模 | 大型项目 | 中型项目 | 中小型项目 | 任何规模 | 中小型项目 |
| 需求复杂度 | 复杂 | 中等 | 简单-中等 | 不限 | 中等 |
| 需求稳定性 | 稳定 | 中等 | 多变 | 不限 | 多变 |
| 团队规模 | 大型团队 | 中型团队 | 小型团队 | 任何规模 | 中小型团队 |
| 代码复用率 | 中等 | 中等 | 高 | 不限 | 低 |
| 协作需求 | 高 | 中等 | 低 | 中等 | 中等 |
| 质量要求 | 高（设计驱动） | 高（测试驱动） | 中等 | 高（自动化保障） | 中（体验驱动） |
| 交付速度 | 慢 | 中 | 快 | 快（部署） | 快（原型） |
| 典型适用 | 企业级系统、金融核心 | 核心业务逻辑、支付系统 | 促销活动、快速迭代 | 持续交付、多环境部署 | 活动页面、交互设计 |
| 不适用 | 快速原型、频繁变更 | 简单CRUD、快速交付 | 复杂架构设计 | 一次性交付 | 后台系统、核心逻辑 |

### 4.3 文档参考优先级对比

| 文档类型 | Spec Coding | TDD | Glue Coding | Harness | Vibe Coding |
|---------|-------------|-----|-------------|---------|-------------|
| 核心作用 | ★★★★ | ★★ | ★★ | ★★ | ★ |
| Reference代码 | ★★★★★ | - | ★★★ | ★ | ★ |
| 需求文档 | ★★★★★ | - | ★ | ★ | ★ |
| 研发规范 | ★★★ | ★★★ | ★★★ | ★★★ | ★★ |
| 架构文档 | ★★★★★ | ★★ | - | ★ | - |
| 测试文档 | ★★★ | ★★★★★ | ★★ | ★★★ | - |
| 部署文档 | - | - | - | ★★★★ | - |
| 设计稿/原型 | ★ | - | - | - | ★★★★ |

### 4.4 量化指标对比

| 指标 | Spec Coding | TDD | Glue Coding | Harness | Vibe Coding |
|------|-------------|-----|-------------|---------|-------------|
| 开发周期 | 慢（3-4周） | 中（2-3周） | 快（1-2周） | 快（部署<10分钟） | 快（原型1-2天） |
| 代码复用率 | 中等（30%） | 中等（30%） | 高（70%） | 不限 | 低（10%） |
| 测试覆盖率 | 中（60%） | 高（90%） | 中（60%） | 高（85%） | 低（30%） |
| 人力成本 | 高 | 高 | 低 | 中 | 中 |
| 维护成本 | 低 | 低 | 中 | 低 | 中 |
| 风险等级 | 低 | 低 | 中 | 低 | 中 |

### 4.5 常见问题与解决方案

（各范式常见坑点略，详见原文）

### 4.6 工具推荐

（各范式工具链略，详见原文）

## 五、组合使用策略

### 5.1 推荐组合架构图

（图片生成提示词略）

### 5.2 组合策略说明

| 阶段 | 推荐范式 | 说明 |
|------|---------|------|
| 项目启动 | - | 加载Reference代码、参考AGENTS.md规范 |
| 需求分析 | Spec Coding | 编写需求文档，识别可复用资产 |
| 设计阶段 | Spec Coding + Vibe Coding | 架构设计用Spec，交互体验用Vibe |
| 开发阶段 | TDD + Glue Coding | 核心逻辑用TDD，辅助功能用Glue Coding |
| 体验优化 | Vibe Coding | A/B测试验证最优方案 |
| 测试阶段 | Harness | 自动化测试、持续验证 |
| 上线阶段 | Harness | 自动化部署、灰度发布 |

## 六、实战经验总结

### 6.1 核心亮点

1. **资产复用带来的效率提升**：通过复用春节促销和周年庆的Reference代码，618促销的核心功能开发时间缩短了60%。优惠券发放逻辑直接复用AnniversaryCouponService，仅需配置新的面额参数；满减计算逻辑复用SpringFestivalPromotionService，仅修改阈值（满300减50）。

2. **规范先行保障质量**：遵循AGENTS.md规范，确保代码风格统一（@Slf4j日志、统一异常处理）；严格遵守永久红线，避免触碰财务模块；使用统一的验证命令：mvn test、mvn checkstyle:check。

3. **范式组合的最佳实践**：需求阶段Spec Coding确保需求清晰，输出14份规范文档；核心逻辑TDD保障质量，覆盖优惠券领取、库存扣减等关键路径；辅助功能Glue Coding快速实现，复用率达70%；交付环节Harness实现自动化部署，缩短上线时间80%。

4. **可追溯性与可维护性**：每个功能点都能追溯到Spec文档；测试用例覆盖核心业务场景，支持安全重构；配置化设计使活动参数可灵活调整，无需修改代码。

### 6.2 关键数据

| 指标 | 数值 | 说明 |
|------|------|------|
| 代码复用率 | 70% | 核心功能复用Reference代码 |
| 开发周期 | 2周 | 从需求到上线的完整周期 |
| 测试覆盖率 | 85% | 核心逻辑单元测试覆盖 |
| 部署时间 | <10分钟 | 自动化流水线部署 |
| 系统可用性 | 99.95% | 618大促期间实际表现 |

### 6.3 关键决策回顾

- **决策1：选择Glue Coding作为主要开发方式** → 理由：促销活动与历史活动相似度高，代码复用价值大。收益：开发效率提升60%，代码质量有保障。
- **决策2：核心逻辑采用TDD** → 理由：优惠券核销、库存扣减涉及资金安全。收益：零线上故障，数据一致性100%。
- **决策3：引入Harness自动化部署** → 理由：多环境部署需求，频繁迭代需要快速验证。收益：部署效率提升80%，支持智能回滚。

## 七、PM角色与跨角色协作

### 7.1 PM在不同范式中的核心职责

| 研发范式 | PM核心职责 | 关键产出 | 协作重点 |
|---------|-----------|---------|---------|
| Spec Coding | 需求收集、优先级排序、文档评审 | 产品需求文档、验收标准 | 与架构师、技术负责人深度协作 |
| TDD | 定义验收标准、参与测试用例评审 | 测试场景描述、验收条件 | 与测试团队紧密配合 |
| Glue Coding | 识别可复用资产、定义功能边界 | 复用资产清单、配置参数 | 与开发团队快速对齐 |
| Harness | 定义发布节奏、参与灰度策略 | 发布计划、回滚预案 | 与DevOps团队协作 |
| Vibe Coding | 用户研究、体验目标定义 | 设计需求、A/B测试方案 | 与设计团队、数据团队协作 |

### 7.2 跨角色协作矩阵

（Mermaid flowchart 略）

### 7.3 典型协作流程

- 阶段一：需求分析（Spec Coding为主）→ PM收集需求 → 整理用户故事 → 与技术团队评审 → 输出PRD文档
- 阶段二：设计阶段（Spec + Vibe Coding）→ PM定义体验目标 → 设计师出原型 → A/B测试验证 → 确定最终方案
- 阶段三：开发阶段（TDD + Glue Coding）→ PM确认验收标准 → 开发团队复用Reference → 测试团队编写用例 → 功能实现
- 阶段四：上线阶段（Harness）→ PM制定发布计划 → DevOps配置流水线 → 灰度发布 → 数据监测 → 全量上线

### 7.4 PM必备工具集

| 工具类型 | 推荐工具 | 用途 |
|---------|---------|------|
| 需求管理 | Jira、PingCode | 需求收集、优先级管理 |
| 原型设计 | Figma、Axure | 快速原型、交互设计 |
| 协作沟通 | 飞书、Slack | 团队沟通、文档协作 |
| 数据分析 | 神策、GrowingIO | 用户行为分析、A/B测试 |
| 项目管理 | Trello、Asana | 任务跟踪、进度管理 |

## 八、结语

五种研发范式各有优劣，没有绝对的好坏之分，关键在于是否适合当前的项目场景。

2026年企业AI Coding，不是简单的Vibe Coding，单一Spec Coding也难以满足需求。
一同探索！一同解锁！
