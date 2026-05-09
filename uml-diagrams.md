# awesome 项目 - 4+1 视图 UML 图

## 1. 逻辑视图 (Logical View) - 文件结构

```mermaid
graph TD
    ROOT["/ (根目录)"]
    
    CORE["核心文档"]
    README["readme.md<br/>主索引/内容"]
    AWESOME["awesome.md<br/>规范定义"]
    CREATE["create-list.md<br/>创建指南"]
    
    GUIDES["指南文档"]
    CONTRIB["contributing.md<br/>贡献指南"]
    CONDUCT["code-of-conduct.md<br/>行为准则"]
    PR["pull_request_template.md<br/>PR模板"]
    
    CONFIG["配置文件"]
    EDITOR[".editorconfig"]
    GITATTR[".gitattributes"]
    LICENSE["license<br/>MIT许可证"]
    
    GITHUB[".github/"]
    WORKFLOWS["workflows/"]
    MAIN["main.yml<br/>CI工作流"]
    LINTER["repo_linter.sh<br/>检查脚本"]
    
    MEDIA["media/"]
    IMAGES["徽章/图标<br/>svg/png/ai"]
    MEDIA_README["readme.md"]
    
    ROOT --> CORE
    ROOT --> GUIDES
    ROOT --> CONFIG
    ROOT --> GITHUB
    ROOT --> MEDIA
    
    CORE --> README
    CORE --> AWESOME
    CORE --> CREATE
    
    GUIDES --> CONTRIB
    GUIDES --> CONDUCT
    GUIDES --> PR
    
    CONFIG --> EDITOR
    CONFIG --> GITATTR
    CONFIG --> LICENSE
    
    GITHUB --> WORKFLOWS
    WORKFLOWS --> MAIN
    WORKFLOWS --> LINTER
    
    MEDIA --> IMAGES
    MEDIA --> MEDIA_README
```

## 2. 过程视图 (Process View) - PR 协作流程

```mermaid
sequenceDiagram
    participant C as 贡献者
    participant G as GitHub
    participant A as GitHub Actions
    participant M as 维护者
    
    C->>G: 1. Fork 仓库
    G-->>C: 个人副本
    
    C->>C: 2. 编辑 readme.md
    
    C->>G: 3. 提交 Pull Request
    G->>G: 应用 PR 模板
    
    G->>A: 4. 触发 CI 检查
    A->>A: 运行 repo_linter.sh
    A-->>G: 检查结果
    
    G-->>M: 5. 通知审核
    M->>G: 6. 审核代码
    
    alt 审核通过
        M->>G: 7. Merge
        G->>C: 通知合并成功
    else 需要修改
        M->>C: 请求修改
        C->>G: 更新 PR
    end
```

## 3. 开发视图 (Development View) - 目录结构

```mermaid
flowchart LR
    subgraph ROOT["D:/awesome/"]
        direction TB
        DOCS["📄 文档文件<br/>6个"]
        CONFIGS["⚙️ 配置文件<br/>3个"]
        
        subgraph GIT["🔧 .github/"]
            CI["CI配置"]
            LINT["lint脚本"]
        end
        
        subgraph MEDIA["🖼️ media/"]
            BADGES["徽章"]
            LOGOS["Logo"]
        end
    end
    
    DOCS --> GIT
    DOCS --> MEDIA
    CONFIGS --> ROOT
```

## 4. 物理视图 (Physical View) - 部署架构

```mermaid
graph TD
    subgraph USERS["用户端"]
        U1[浏览器]
        U2[Git 客户端]
    end
    
    subgraph GITHUB["GitHub 云服务"]
        REPO[awesome 仓库]
        ACTIONS[Actions 运行器]
        PAGES[GitHub Pages]
    end
    
    subgraph EXTERNAL["外部资源"]
        EXT[被索引的网站]
    end
    
    U1 -->|https 浏览| REPO
    U2 -->|git clone/push| REPO
    REPO --> ACTIONS
    REPO --> PAGES
    U1 -.->|点击链接| EXT
```

## 5. 场景示例 (Scenarios) - 用户查看项目

```mermaid
sequenceDiagram
    participant User as 用户
    participant Browser as 浏览器
    participant GitHub as GitHub服务器
    participant Repo as awesome仓库
    
    User->>Browser: 输入 GitHub 地址
    Browser->>GitHub: 发送 HTTPS 请求
    GitHub->>Repo: 读取仓库内容
    Repo-->>GitHub: 返回 readme.md
    GitHub-->>Browser: 渲染 HTML 页面
    Browser-->>User: 显示项目首页
    
    User->>Browser: 点击分类链接
    Browser->>External: 跳转到外部网站
    External-->>Browser: 返回内容
    Browser-->>User: 显示资源页面
```
