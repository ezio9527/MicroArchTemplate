
# ics-server 项目目录结构

这个项目采用了基于 Monorepo 的管理方式，使用 Lerna 来管理多个微服务、应用程序和共享库。以下是项目的目录结构和每个部分的详细说明。

## 目录结构

```
ics-server/
│
├── .github/                         # GitHub工作流目录
├── packages/                        # 所有包的根目录
│   ├── apps/                        # 应用程序和业务服务
│   │   ├── ics-server-api-gateway/  # API Gateway，处理所有外部请求的入口
│   │   ├── ics-server-user/         # 用户服务，处理用户管理
│   │   ├── ics-server-order/        # 订单服务，处理订单管理
│   │   └── ...                      # 其他应用/业务服务
│   │
│   ├── services/                    # 微服务目录
│   │   ├── auth/                    # 认证/授权相关微服务
│   │   │   ├── auth-service/        # 核心认证服务（登录验证）
│   │   │   ├── registration-service/# 用户注册服务
│   │   │   ├── oauth-service/       # 第三方 OAuth 授权服务
│   │   │   ├── token-service/       # 令牌管理服务（JWT）
│   │   │   └── ...                  # 未来扩展的认证/授权微服务
│   │   └── ...                      # 其他微服务目录（如支付、通知等）
│   │
│   ├── libs/                        # 公共库目录
│   │   ├── shared-config/           # 共享配置模块
│   │   ├── shared-utils/            # 共享的工具函数和帮助类库
│   │   ├── shared-types/            # 共享的 TypeScript 类型和接口定义
│   │   ├── shared-constants/        # 共享的常量定义
│   │   └── ...                      # 其他共享模块
│   │
│   ├── tools/                       # 工具和脚本目录
│   │   ├── scripts/                 # 自定义脚本（如部署、构建、清理）
│   │   ├── ci/                      # CI/CD 配置和脚本
│   │   └── ...                      # 其他工具和配置
│   │
│   └── docs/                        # 文档目录
│       ├── api/                     # API 文档
│       ├── architecture/            # 系统架构文档
│       └── ...                      # 其他相关文档
│
├── .gitignore                       # Git 忽略文件
├── docker-compose.yml               # Docker Compose配置
├── lerna.json                       # Lerna 配置文件
├── package.json                     # 根 package.json 文件，管理 Monorepo 整体依赖
└── tsconfig.base.json               # TypeScript 基础配置
```

## 目录结构说明

- **`packages/`**: 这是所有包的根目录，包含了所有的应用程序、微服务和共享库。
- **`apps/`**: 该目录用于存放业务应用程序和服务，比如用户管理、订单管理等。API Gateway 也是一个重要的部分，它充当所有外部请求的统一入口。
- **`services/`**: 此目录存放所有的微服务。`auth/` 目录专门处理与认证和授权相关的微服务。将来，如果有新的功能模块（如支付、通知等），可以在此目录下添加新的子目录。
- **`libs/`**: 公共库目录，用于存放所有共享模块和库。包括共享的配置、工具函数、类型定义和常量等。这些模块可以被 `apps/` 和 `services/` 中的微服务共同使用。
- **`tools/`**: 工具和脚本目录，存放各种工具和脚本，如部署脚本、CI/CD 配置和其他自定义工具。
- **`docs/`**: 文档目录，用于存放 API 文档、系统架构文档和其他相关文档。这有助于团队成员和外部协作者了解系统的设计和功能。
- **`.gitignore`**: Git 忽略文件，用于定义哪些文件和目录不应纳入版本控制。
- **`lerna.json`**: Lerna 配置文件，定义了 Lerna 如何管理这个 Monorepo 项目。
- **`package.json`**: 根目录的 package.json 文件，用于管理 Monorepo 的全局依赖和脚本。
- **`tsconfig.base.json`**: TypeScript 的基础配置文件，供各个包和模块继承使用。

## 项目管理

- 使用 Lerna 来管理 Monorepo 中的所有包，可以使用 `lerna bootstrap` 进行依赖安装，使用 `lerna run` 运行脚本。
- 使用 CI/CD 工具（如 GitHub Actions、GitLab CI 等）来实现自动化构建、测试和部署。
- 为每个微服务和应用程序编写独立的 README 文件，描述其功能、依赖和使用方法。

## 结论

该项目结构设计旨在提供高扩展性和模块化，适合中大型项目的开发。通过将不同的功能模块分离到独立的目录下，可以实现更好的代码隔离、复用性和团队协作。
