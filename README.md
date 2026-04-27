# Todo-fullstack

全栈 Todo 应用，基于 Next.js 16 + React 19 + Prisma + SQLite。

## 技术架构

```
┌─────────────────────────────────────────────────────────────┐
│                        Frontend                              │
│  Next.js 16 (App Router) + React 19 + TypeScript + Tailwind │
│  状态管理: Zustand  │  动画: Framer Motion  │  UI: shadcn/ui │
└────────────────────────────┬────────────────────────────────┘
                             │
                    Server Actions (BFF)
                             │
┌────────────────────────────▼────────────────────────────────┐
│                        Backend                               │
│              Next.js Serverless Functions                    │
└────────────────────────────┬────────────────────────────────┘
                             │
┌────────────────────────────▼────────────────────────────────┐
│                     Data Layer                               │
│         Prisma ORM  │  SQLite (开发) / Neon (生产)           │
└─────────────────────────────────────────────────────────────┘
```

## 快速启动

```bash
# 安装依赖
pnpm install

# 初始化数据库
pnpm prisma generate
pnpm prisma db push

# 启动开发服务器
pnpm dev
```

访问 [http://localhost:3000](http://localhost:3000)

## 项目结构

```
├── app/                    # Next.js App Router
│   ├── actions.ts         # Server Actions (API 逻辑)
│   ├── page.tsx           # 主页
│   ├── layout.tsx         # 根布局
│   └── globals.css        # 全局样式
├── components/             # React 组件
│   ├── TodoForm.tsx       # 新建 Todo 表单
│   └── TodoItem.tsx       # Todo 项组件
├── lib/                    # 工具库
│   ├── prisma.ts          # Prisma 客户端
│   ├── store.ts           # Zustand 状态管理
│   └── utils.ts           # 工具函数
├── prisma/                 # 数据库 schema
│   └── schema.prisma       # Todo 模型定义
└── package.json
```

## 开发流程

本项目使用 [Agent Skills](https://github.com/addyosmani/agent-skills) 规范开发流程：

```
DEFINE          PLAN           BUILD          VERIFY         REVIEW          SHIP
┌──────┐      ┌──────┐      ┌──────┐      ┌──────┐      ┌──────┐      ┌──────┐
│ Idea │ ───▶ │ Spec │ ───▶ │ Code │ ───▶ │ Test │ ───▶ │  QA  │ ───▶ │  Go  │
│Refine│      │  PRD │      │ Impl │      │Debug │      │ Gate │      │ Live │
└──────┘      └──────┘      └──────┘      └──────┘      └──────┘      └──────┘
```

### 开发阶段与对应 Skills

| 阶段 | Skill | 说明 |
|------|-------|------|
| 需求定义 | `idea-refine` | 细化需求，结构化思考 |
| 架构设计 | `spec-driven-development` | 编写 SPEC 文档后再编码 |
| 任务分解 | `planning-and-task-breakdown` | 拆分为小而可验证的任务 |
| 增量实现 | `incremental-implementation` | 逐个 slice 实现，每步验证 |
| 测试驱动 | `test-driven-development` | 先写测试，再实现 |
| 代码审查 | `code-review-and-quality` | 五维度审查（正确性、可读性、架构、安全、性能） |
| 安全审查 | `security-and-hardening` | OWASP Top 10 防护 |
| 前端开发 | `frontend-ui-engineering` | 生产级 UI + 可访问性 |
| API 设计 | `api-and-interface-design` | 稳定接口，清晰契约 |
| 性能优化 | `performance-optimization` | 按需优化，测量先行 |
| 代码简化 | `code-simplification` | 清晰优于聪明 |
| Git 工作流 | `git-workflow-and-versioning` | 原子提交，干净历史 |
| CI/CD | `ci-cd-and-automation` | 自动化质量门禁 |
| 文档编写 | `documentation-and-adrs` | 记录决策过程 |
| 部署上线 | `shipping-and-launch` | 上线检查清单，监控，回滚 |

### 可用命令

```bash
/spec      # 启动 spec-driven-development
/plan      # 启动 planning-and-task-breakdown
/build     # 启动 incremental-implementation
/test      # 启动 test-driven-development
/review    # 启动 code-review-and-quality
/code-simplify  # 启动 code-simplification
/ship      # 启动 shipping-and-launch
```

## 技术栈详情

### 前端
- **Next.js 16.2.4** (Turbopack)
- **React 19.2.4**
- **TypeScript 5**
- **Tailwind CSS 4** + PostCSS
- **Zustand 5** - 轻量状态管理
- **Framer Motion 12** - 动画库
- **Lucide React** - 图标库
- **Zod 4** - Schema 验证

### 后端 & 数据
- **Prisma 6** - ORM
- **SQLite** - 开发数据库 (dev.db)
- **Server Actions** - API 逻辑

### 开发工具
- **ESLint 9** - 代码检查
- **pnpm 10** - 包管理器

## 环境变量

```env
DATABASE_URL="file:./dev.db"
```

## 数据库 Schema

```prisma
model Todo {
  id        String   @id @default(uuid())
  title     String
  completed Boolean  @default(false)
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
}
```

## 学习资源

- [Next.js 文档](https://nextjs.org/docs)
- [React 文档](https://react.dev)
- [Prisma 文档](https://pris.ly/d/prisma-schema)
- [Agent Skills](https://github.com/addyosmani/agent-skills)
