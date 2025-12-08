# Execution Environment

## 运行环境

**Dec 08, 2025**

**Likes:** 0

# 🌐 **Execution Environment Guide**

 _for ADK · Decade of Agents Projects_

https://github.com/STEMMOM/adk-decade-of-agents/tree/main

* * *

## 🇺🇸 **1\. Introduction**

This guide defines the unified execution environment for all **ADK (Agent Development Kit)** projects across the P01–P50 series, including memory experiments, persona systems, state engines, preference extraction, and router dispatch.

A consistent environment ensures **deterministic behavior, reproducibility, and evolutionary continuity**.

* * *

## 🇺🇸 **2\. System Requirements**

  *  **OS** : macOS / Linux / Windows

  *  **Python** : Recommended **Python 3.11+**

  *  **Network** : Access to Google Generative AI API




* * *

## 🇺🇸 **3\. Virtual Environment**

All projects share the same root-level environment:
    
    
    adk-decade-of-agents/.venv
    
    

Create:
    
    
    python3 -m venv .venv
    source .venv/bin/activate        # macOS / Linux
    .\\.venv\\Scripts\\activate         # Windows PowerShell
    
    

* * *

## 🇺🇸 **4\. Dependencies**

All projects share a single dependency file:
    
    
    requirements.txt
    
    

Install:
    
    
    pip install -r requirements.txt
    
    

Includes:

  * Google Generative AI SDK

  * Google ADK runtime (google-ai-agents)

  * Rich, SQLAlchemy, Pydantic

  * Memory / State / Router utilities




* * *

## 🇺🇸 **5\. API Key Configuration**

Create `.env` at the repo root:
    
    
    GOOGLE_API_KEY=your_api_key
    
    

`.env` is already ignored by git.

* * *

## 🇺🇸 **6\. ADK Runtime**

All projects rely on the unified ADK runtime stack:

  *  **Session Runtime**

  *  **Event Ledger & Compaction**

  *  **Memory Store**

  *  **State Injection**

  *  **Runners** (InMemory / SQLite)

  *  **Router / Persona Dispatch**

  *  **Observability (logs, traces, metrics)**




Install:
    
    
    pip install -U google-ai-agents
    
    

* * *

## 🇺🇸 **7\. Running a Project**

Each project follows the same structure:
    
    
    projects/p18-preference-extraction/src/main.py
    
    

Run:
    
    
    cd projects/pXX-some-project
    python src/main.py
    
    

* * *

## 🇺🇸 **8\. Shared Global Data Structures**

All projects evolve through the same shared structures:

  * `session.events` — event ledger

  * `session.state` — working memory

  * `memory_store.json` — long-term memory

  * Persona Card & Preference JSON

  * Router policies




These structures **persist across projects** to maintain continuity of the agent.

* * *

## 🇺🇸 **9\. Notes**

  * Individual projects will not repeat environment setup

  * Updates to the environment will be documented here




# 🌐 **运行环境指南（Execution Environment Guide）**

 _for ADK · Decade of Agents Projects_

* * *

##  🇨🇳 **一、简介（Introduction）**

本指南定义了所有 **ADK（Agent Development Kit）项目** 的统一运行环境，包括 P01–P50 的所有单元项目、结构卡测试项目、Persona/Memory 系列，以及 Router/Preference 系列等。

为了保证 **行为一致性、可重复性和链式演化** ，所有项目必须运行在 **同一套环境** 中。

* * *

## 🇨🇳 **二、系统要求（System Requirements）**

  *  **操作系统** ：macOS / Linux / Windows 均可

  *  **Python 版本** ：推荐 **Python 3.11+**

  *  **网络要求** ：可访问 Google Generative AI API




* * *

## 🇨🇳 **三、虚拟环境（Virtual Environment）**

所有项目必须使用仓库根目录的统一虚拟环境：
    
    
    adk-decade-of-agents/.venv
    
    

创建方式：
    
    
    python3 -m venv .venv
    source .venv/bin/activate        # macOS / Linux
    .\\.venv\\Scripts\\activate         # Windows PowerShell
    
    

* * *

## 🇨🇳 **四、依赖安装（Dependencies）**

所有项目共享同一个依赖文件：
    
    
    requirements.txt
    
    

安装方式：
    
    
    pip install -r requirements.txt
    
    

依赖包含：

  * Google Generative AI SDK

  * Google ADK (google-ai-agents)

  * Rich, SQLAlchemy, Pydantic 等

  * 用于 Memory / State / Router 的必要模块




* * *

## 🇨🇳 **五、API Key 配置（API Key Configuration）**

在仓库根目录创建 `.env`：
    
    
    adk-decade-of-agents/.env
    
    

写入：
    
    
    GOOGLE_API_KEY=your_api_key
    
    

`.env` 已列入 `.gitignore` 避免泄露。

* * *

## 🇨🇳 **六、ADK Runtime（核心环境）**

所有项目依赖 ADK 的统一运行环境，包括：

  *  **Session Runtime** （事件与上下文管理）

  *  **Memory Store** （长期记忆）

  *  **Event Ledger / Compaction**

  *  **State 注入机制**

  *  **Runners：InMemoryRunner / SQLiteRunner**

  *  **Router / Persona Dispatch 机制**

  *  **Observability（logs/traces/metrics）**




安装 ADK：
    
    
    pip install -U google-ai-agents
    
    

* * *

## 🇨🇳 **七、项目运行方法（Running a Project）**

每个项目都有统一结构：
    
    
    projects/p18-preference-extraction/src/main.py
    
    

运行：
    
    
    cd projects/pXX-some-project
    python src/main.py
    
    

* * *

## 🇨🇳 **八、全局共享数据结构（Global Shared Structures）**

所有项目使用同一套演化数据结构：

  * `session.events` —— 事件账本（短期记忆）

  * `session.state` —— 结构化“工作记忆”

  * `memory_store.json` —— 长期记忆与偏好

  * Persona Card / Preference JSON

  * Router 策略参数




这些结构 **在多个项目间持续演化** ，保证智能体“从一代到下一代”保持连续性。

* * *

## 🇨🇳 **九、说明（Notes）**

  * 单个项目不再重复描述环境

  * 所有环境更新会在此文件同步维护



