# Front Matter 标签智能映射配置

本文档定义了 AutoSmirk front matter 生成功能的标签智能推断规则，基于文件路径和内容关键词自动生成合适的标签。

## 标签映射规则 (90+ 关键词)

### 编程语言

| 关键词 | 自动标签 |
|--------|----------|
| `java`, `jdk`, `jre` | Java |
| `python`, `py`, `pip` | Python |
| `javascript`, `js`, `node`, `nodejs` | JavaScript, Node.js |
| `typescript`, `ts` | TypeScript |
| `rust`, `cargo` | Rust |
| `go`, `golang` | Go |
| `c++`, `cpp`, `cplusplus` | C++ |
| `csharp`, `c#` | C# |
| `php`, `laravel`, `symfony` | PHP, Laravel |
| `kotlin` | Kotlin |
| `swift` | Swift |
| `dart`, `flutter` | Dart, Flutter |

### 框架与库

| 关键词 | 自动标签 |
|--------|----------|
| `spring`, `springboot`, `spring-boot` | Spring Boot |
| `springcloud`, `spring-cloud` | Spring Cloud |
| `mybatis`, `mybatis-plus` | MyBatis |
| `hibernate`, `jpa` | Hibernate, JPA |
| `vue`, `vuejs`, `vue.js` | Vue.js |
| `react`, `reactjs`, `next`, `nextjs` | React, Next.js |
| `angular` | Angular |
| `nuxt`, `nuxtjs` | Nuxt.js |
| `svelte` | Svelte |
| `django`, `djangorestframework`, `drf` | Django, Django REST |
| `fastapi` | FastAPI |
| `flask` | Flask |
| `express`, `koa`, `nest`, `nestjs` | Node.js, Express/Koa/NestJS |
| `electron` | Electron |
| `tauri` | Tauri |

### 前端技术

| 关键词 | 自动标签 |
|--------|----------|
| `vite`, `vitepress` | Vite, VitePress |
| `webpack`, `rollup`, `esbuild` | 前端工程化 |
| `css`, `scss`, `sass`, `less` | CSS |
| `tailwind`, `tailwindcss` | Tailwind CSS |
| `bootstrap` | Bootstrap |
| `html`, `htm` | HTML |
| `svg`, `canvas` | 前端图形 |
| `webassembly`, `wasm` | WebAssembly |

### 后端技术

| 关键词 | 自动标签 |
|--------|----------|
| `microservice`, `micro-service` | 微服务 |
| `distributed`, `distribution` | 分布式 |
| `architecture`, `arch` | 系统架构 |
| `design-pattern`, `pattern` | 设计模式 |
| `rest`, `restful`, `api` | REST API |
| `graphql`, `gql` | GraphQL |
| `grpc` | gRPC |
| `websocket`, `ws`, `socket` | WebSocket |
| `middleware` | 中间件 |

### 安全与认证

| 关键词 | 自动标签 |
|--------|----------|
| `security`, `sec` | 安全 |
| `auth`, `authentication` | 认证鉴权 |
| `authorization`, `permission`, `rbac`, `abac` | 认证鉴权 |
| `oauth`, `oauth2`, `openid`, `oidc` | OAuth, OIDC |
| `sso`, `single-sign-on` | 单点登录 |
| `jwt`, `json-web-token` | JWT |
| `ssl`, `tls`, `https` | HTTPS, SSL/TLS |
| `encrypt`, `crypto`, `cipher` | 加密 |
| `hash`, `md5`, `sha256` | 哈希 |
| `vulnerability`, `xss`, `csrf`, `sql-injection` | 安全, Web安全 |

### 性能与优化

| 关键词 | 自动标签 |
|--------|----------|
| `performance`, `perf` | 性能优化 |
| `optimization`, `optimize` | 性能优化 |
| `jvm`, `gc`, `garbage` | JVM调优 |
| `cache`, `caching`, `redis` | Redis, 缓存 |
| `concurrent`, `parallel`, `async`, `await` | 并发编程 |
| `multithread`, `thread` | 多线程 |
| `monitor`, `monitoring`, `metric`, `prometheus` | 监控 |
| `profiling`, `profile` | 性能分析 |
| `loadbalance`, `load-balance` | 负载均衡 |

### 数据库

| 关键词 | 自动标签 |
|--------|----------|
| `database`, `db` | 数据库 |
| `mysql` | MySQL |
| `postgresql`, `postgres` | PostgreSQL |
| `mongodb`, `mongo` | MongoDB |
| `redis` | Redis |
| `elasticsearch`, `es` | Elasticsearch |
| `sqlite` | SQLite |
| `mssql`, `sqlserver` | SQL Server |
| `oracle` | Oracle |
| `clickhouse` | ClickHouse |
| `influxdb` | InfluxDB |
| `sql`, `query`, `transaction` | 数据库, SQL |

### 消息队列

| 关键词 | 自动标签 |
|--------|----------|
| `mq`, `message-queue`, `message-queue` | 消息队列 |
| `kafka` | Kafka |
| `rabbitmq`, `rabbit` | RabbitMQ |
| `rocketmq` | RocketMQ |
| `activemq` | ActiveMQ |
| `pulsar` | Apache Pulsar |
| `nats` | NATS |
| `pubsub`, `pub-sub` | 消息队列 |

### AI 与大模型

| 关键词 | 自动标签 |
|--------|----------|
| `ai`, `artificial-intelligence` | AI |
| `llm`, `large-language-model` | 大模型 |
| `claude`, `anthropic` | Claude |
| `gpt`, `openai`, `chatgpt` | OpenAI, GPT |
| `prompt`, `prompt-engineering` | 提示工程 |
| `rag`, `retrieval-augmented` | RAG |
| `langchain` | LangChain |
| `ml`, `machine-learning` | 机器学习 |
| `dl`, `deep-learning` | 深度学习 |
| `nlp`, `natural-language` | NLP |
| `cv`, `computer-vision` | 计算机视觉 |
| `tensorflow`, `pytorch`, `keras` | TensorFlow/PyTorch |
| `huggingface`, `transformers` | HuggingFace |

### DevOps 与工具

| 关键词 | 自动标签 |
|--------|----------|
| `docker`, `container` | Docker, 容器化 |
| `kubernetes`, `k8s`, `kube` | Kubernetes |
| `cicd`, `ci-cd`, `ci`, `cd` | CI/CD |
| `jenkins` | Jenkins |
| `gitlab`, `github` | Git |
| `git` | Git |
| `terraform`, `ansible`, `chef`, `puppet` | 自动化运维 |
| `nginx`, `apache`, `tomcat` | Nginx/Apache/Tomcat |
| `linux`, `unix`, `shell`, `bash` | Linux, Shell |
| `aws`, `azure`, `gcp`, `aliyun` | 云计算 |
| `serverless`, `lambda` | Serverless |

### 开发工具

| 关键词 | 自动标签 |
|--------|----------|
| `idea`, `intellij`, `pycharm`, `webstorm` | IDEA |
| `vscode`, `visual-studio-code` | VSCode |
| `vim`, `neovim` | Vim |
| `plugin`, `extension` | 插件开发 |
| `ide`, `editor` | 开发工具 |

### 算法与数据结构

| 关键词 | 自动标签 |
|--------|----------|
| `algorithm`, `algo` | 算法 |
| `data-structure`, `ds` | 数据结构 |
| `dynamic-programming`, `dp` | 动态规划 |
| `greedy` | 贪心算法 |
| `backtrack` | 回溯算法 |
| `sort`, `sorting` | 排序算法 |
| `search`, `searching` | 搜索算法 |
| `graph`, `tree`, `heap`, `stack`, `queue` | 数据结构 |
| `linkedlist`, `linked-list` | 数据结构 |
| `binary-tree`, `bst` | 二叉树 |
| `dp`, `memoization` | 动态规划 |

### 其他

| 关键词 | 自动标签 |
|--------|----------|
| `blog`, `article` | 技术感悟 |
| `note`, `notes`, `learning` | 学习笔记 |
| `tutorial`, `guide`, `howto` | 教程 |
| `interview`, `job` | 面试 |
| `leetcode` | LeetCode, 算法 |
| `code`, `coding`, `programming` | 编程 |
| `debug`, `debugging` | 调试 |
| `refactor`, `refactoring` | 重构 |
| `test`, `testing`, `unittest`, `integration-test` | 测试 |
| `tdd`, `bdd` | TDD, 测试 |
| `agile`, `scrum`, `kanban` | 敏捷开发 |
| `code-review`, `review` | Code Review |
| `pattern`, `practice`, `best-practice` | 最佳实践 |
| `idea`, `insight`, `thinking` | 技术感悟 |

## 默认规则

1. **标签数量限制**：最多生成 5 个标签
2. **标签优先级**：路径关键词 > 内容关键词
3. **默认标签**：无法推断时使用 `['技术']`
4. **去重**：自动去除重复标签
5. **大小写**：标签首字母大写（如 "Spring Boot"）
6. **特殊字符**：保留中文标签，英文标签空格分隔

## 标签推断示例

| 文件路径 | 推断标签 |
|----------|----------|
| `docs/spring-security-jwt-auth.md` | Spring Boot, Spring Security, 认证鉴权, JWT |
| `posts/redis-cache-best-practices.md` | Redis, 缓存, 性能优化 |
| `notes/algorithm-dynamic-programming.md` | 算法, 动态规划 |
| `tutorials/react-typescript-tailwind.md` | React, TypeScript, Tailwind CSS, 前端开发 |
| `articles/kafka-message-queue-architecture.md` | Kafka, 消息队列, 系统架构, 分布式 |
