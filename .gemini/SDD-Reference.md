# Gemini SDD (Solution Design Document) 提示詞框架

這是一個基於解決方案設計文件（SDD）的提示詞框架，旨在引導您使用 Gemini 來設計、開發和部署此 Spring Boot 專案。您可以直接複製這些提示詞，填入您的具體需求，然後發送給 Gemini。

## 1. 專案概述 (Project Overview)
- **定義目標**: `請根據這個想法：「[在這裡填寫您的核心想法，例如：一個線上的待辦事項清單應用]」，為這個 Spring Boot 專案產生一個清晰的專案目標與範圍說明。`
- **列出主要功能**: `這個專案的核心功能是什麼？請幫我列出 3-5 個主要功能點。`
- **分析技術棧**: `目前專案使用 Spring Boot 和 JDK 8。請基於專案目標，分析並建議其他可能需要的技術（例如：資料庫建議使用 PostgreSQL，緩存建議使用 Redis，前端框架建議使用 React）。`

## 2. 需求分析 (Requirements Analysis)
- **定義功能性需求**: `我需要一個「使用者註冊」功能，它能讓使用者透過 Email 和密碼進行註冊，註冊成功後自動登入。請幫我把這個需求轉換成詳細的功能規格。` (可重複此模式來定義所有功能)
- **定義非功能性需求**:
    - **效能**: `請定義主要 API (例如：GET /items) 的預期回應時間和每秒請求數 (RPS)。`
    - **安全性**: `針對使用者認證和授權，請建議一個適合 Spring Boot 的安全實現方案 (例如：使用 Spring Security + JWT)，並說明實作步驟。`
    - **可靠性**: `系統需要達到 99.9% 的可用性。請建議實現此目標的策略，例如健康檢查端點、資料庫備份等。`

## 3. 系統架構 (System Architecture)
- **繪製架構圖**: `基於這是一個 Spring Boot 單體應用，請幫我使用 Mermaid 語法繪製一個簡單的系統架構圖，包含使用者、負載均衡器、Web 伺服器和資料庫。`
- **設計分層結構**: `請為這個專案設計一個經典的三層式架構 (Controller/Presentation, Service/Business, Repository/Data Access)，並在 `src/main/java/org/example` 下建立對應的資料夾結構。`
- **定義組件關係**: `請識別此專案中的關鍵組件 (例如 UserController, UserService, UserRepository)，並使用 Mermaid 的序列圖描述「使用者註冊」流程中它們之間的互動關係。`

## 4. 資料庫設計 (Data Design)
- **產生實體類別**: `我需要儲存「產品」資訊，它包含 ID、名稱(name)、價格(price)和建立時間(created_at)。請幫我產生對應的 JPA Entity 類別 (Product.java)，並放在 `org.example.model` 套件中。`
- **設計資料庫綱要**: `基於「使用者」和「產品」這兩個實體，其中一個使用者可以擁有多個產品。請幫我產生一個表示此一對多關係的資料庫 ERD (使用 Mermaid 語法)。`
- **產生資料庫遷移腳本**: `請為 `Product` 實體產生一個 Flyway V2__Create_product_table.sql 遷移腳本。`

## 5. API 設計 (API Design)
- **設計 RESTful API**: `我需要設計一個「獲取所有產品」的 RESTful API。請幫我定義出 HTTP 方法、URL 路徑 (`/api/products`)、請求參數和預期的 JSON 回應格式。`
- **產生 OpenAPI 規格**: `請為 `HelloController.java` 中的 `GET /` 端點產生 OpenAPI 3.0 規格，並以 YAML 格式提供。`
- **建立 Controller**: `請幫我建立一個 `ProductController.java`，包含一個 `GET /api/products` 的端點，並回傳一個靜態的產品列表。`

## 6. 開發與實作 (Development & Implementation)
- **實作業務邏輯**: `請幫我實作 `UserService.java` 中的 `registerUser` 方法。它需要檢查 Email 是否已存在，對密碼進行加密，然後將新使用者存到資料庫。`
- **編寫單元測試**: `請為 `UserService` 的 `registerUser` 方法編寫一個使用 Mockito 的單元測試，驗證當 Email 已存在時，是否會拋出預期的例外。`
- **編寫整合測試**: `請編寫一個 Spring Boot 整合測試，使用 Testcontainers 來啟動一個 PostgreSQL 資料庫，驗證從 `ProductController` 到 `ProductRepository` 的完整流程。`

## 7. 部署與維運 (Deployment & Operations)
- **產生 Dockerfile**: `請為這個 Spring Boot 專案產生一個最佳化的、用於生產環境的多階段建置 (multi-stage build) Dockerfile。`
- **建立 CI/CD 流程**: `請為這個專案建立一個使用 GitHub Actions 的 CI/CD 工作流程檔案 (`.github/workflows/ci.yml`)。這個流程需要在每次推送到 main 分支時，自動執行 Maven 測試、建置專案，並建置 Docker 映像。`
- **整合監控與日誌**: `請說明如何在 `pom.xml` 和 `application.properties` 中加入必要的依賴和配置，以整合 Micrometer、Prometheus 和 Loki 進行監控與日誌記錄。`