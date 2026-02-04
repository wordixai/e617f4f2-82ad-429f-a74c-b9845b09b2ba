# AI 换衣应用 - 实现计划

## 产品概述
一款让用户上传自己的照片，从预设服装库选择衣服，通过 AI 生成虚拟试穿效果的应用。

---

## 核心功能模块

### 1. 首页 (Landing Page)
- 渐变动画背景的 Hero 区域
- 功能亮点展示（上传 → 选择 → 获取结果）
- 示例效果展示轮播

### 2. 图片上传
- 拖拽上传区域，支持点击选择
- 图片格式/大小校验
- 上传进度显示
- 图片预览

### 3. 服装选择
- 分类浏览（上装、下装、连衣裙、外套）
- 网格展示服装缩略图
- 服装详情预览

### 4. AI 换衣处理
- 处理进度动画
- 错误处理与重试
- 预估时间显示

### 5. 结果展示
- 前后对比滑块
- 下载生成图片
- 分享功能
- 再试一件

---

## 用户流程

```
首页 → 点击开始 → 上传照片 → 选择服装 → 确认生成 → 等待处理 → 查看结果 → 下载/分享/重试
```

---

## 设计系统（活力年轻风格）

### 配色方案 (HSL)
| 变量 | 颜色 | 用途 |
|------|------|------|
| primary | 270 91% 65% | 电光紫 - 主色调 |
| secondary | 180 100% 50% | 青色 - 辅助色 |
| accent | 330 100% 60% | 热粉色 - 强调色 |

### 渐变效果
- **主渐变**: 紫色 → 粉色 (按钮、卡片悬停)
- **背景渐变**: 淡紫 → 淡粉 → 淡青 (Hero 背景)
- **动画渐变**: 15秒循环流动效果

### 圆角
- 使用 1rem 圆角，营造友好感

---

## 技术架构

### 前端组件结构
```
src/
├── components/
│   ├── layout/          # Header, Footer, PageContainer
│   ├── landing/         # HeroSection, FeatureCards, GallerySection
│   ├── upload/          # UploadZone, ImagePreview, UploadProgress
│   ├── garments/        # GarmentGrid, GarmentCard, CategoryFilter
│   ├── processing/      # ProcessingView, ProgressAnimation
│   └── result/          # ResultView, ComparisonSlider, DownloadButton
├── pages/
│   ├── Index.tsx        # 首页
│   ├── TryOn.tsx        # 换衣主页面
│   └── Result.tsx       # 结果页
├── hooks/
│   ├── useFileUpload.ts
│   ├── useGarments.ts
│   └── useTryOn.ts
├── stores/
│   └── tryOnStore.ts    # Zustand 状态管理
└── types/
    └── index.ts         # 类型定义
```

### Supabase 集成

**数据库表：**
- `garments` - 服装库（名称、分类、图片URL）
- `tryon_sessions` - 换衣会话记录

**存储桶：**
- `garments` - 预设服装图片（公开）
- `user-uploads` - 用户上传照片（私有）
- `results` - 生成结果（私有）

**Edge Functions：**
- `tryon-process` - 调用 Replicate AI API
- `tryon-status` - 查询处理状态

### AI 服务
- **使用 Replicate IDM-VTON 模型**
- 通过 Supabase Edge Function 调用
- 支持上装、下装、全身服装

---

## 实现步骤

### Phase 1: 基础设置
1. 更新 `index.css` - 配色和渐变
2. 更新 `tailwind.config.ts` - 动画配置
3. 启用 Supabase 集成
4. 创建数据库表和存储桶

### Phase 2: UI 组件
1. 布局组件 (Header, PageContainer)
2. 首页 Hero 和功能展示
3. 上传组件 (UploadZone)
4. 服装展示组件 (GarmentGrid, GarmentCard)

### Phase 3: 核心功能
1. 文件上传到 Supabase Storage
2. Zustand 状态管理
3. 服装数据获取
4. 处理状态组件

### Phase 4: AI 集成
1. 创建 Edge Function 处理换衣
2. 配置 Replicate API
3. 实现轮询状态更新
4. 存储生成结果

### Phase 5: 结果展示
1. 结果页面
2. 前后对比滑块
3. 下载和分享功能

---

## 关键文件修改清单

| 文件 | 操作 |
|------|------|
| `/app/src/index.css` | 更新配色、渐变、动画 |
| `/app/tailwind.config.ts` | 添加自定义动画 |
| `/app/src/App.tsx` | 添加路由配置 |
| `/app/src/pages/Index.tsx` | 重写为首页 |
| `/app/src/pages/TryOn.tsx` | 新建 - 换衣主页面 |
| `/app/src/pages/Result.tsx` | 新建 - 结果页 |
| `/app/src/stores/tryOnStore.ts` | 新建 - 状态管理 |

---

## 环境变量

```env
# 前端 (Vite)
VITE_SUPABASE_URL=
VITE_SUPABASE_ANON_KEY=

# Edge Functions (Supabase Secrets)
REPLICATE_API_TOKEN=
```

---

## 验证方案

1. **首页展示** - 访问首页，检查渐变动画和布局
2. **图片上传** - 上传图片，确认预览和存储正常
3. **服装选择** - 浏览服装分类，选择服装
4. **AI 处理** - 触发换衣，观察进度显示
5. **结果展示** - 查看生成图片，测试下载功能
6. **响应式** - 在移动端测试所有页面

---

## 注意事项

- 需要 Replicate API Token（付费，约 $0.02-0.05/次）
- 处理时间约 30-60 秒
- 初始需要准备 20-30 张服装图片作为服装库
