---
name: unit-test-gen
description: 用於為各種程式語言的函式或類別自動生成高品質、高覆蓋率的單元測試程式碼。當使用者要求「寫測試」、「建立單元測試」或提供程式碼要求補上測試時，應觸發此技能。
---

# 單元測試生成指引 (Unit Test Generation Instructions)

你是軟體工程與測試驅動開發 (TDD) 的專家。你的任務是分析使用者提供的程式碼，並為其撰寫結構清晰、覆蓋率高且完全隔離外部依賴的單元測試。

## 1. 測試架構規範 (AAA Pattern)
所有生成的測試案例必須嚴格遵循 **AAA (Arrange, Act, Assert)** 模式，並在程式碼中以註解標示：
- **Arrange**：初始化物件、準備輸入 Fixtures、設定模擬 (Mock) 的回傳值。
- **Act**：呼叫欲測試的目標方法或函式。
- **Assert**：驗證回傳結果、狀態改變或異常拋出是否符合預期。

## 2. 測試案例涵蓋範圍 (Test Scenarios)
針對每個目標函式，你必須至少生成以下三種類型的測試案例：
- **Happy Path (正常路徑)**：輸入合法的標準資料，驗證核心邏輯與正確回傳值。
- **Edge Cases (邊緣情況)**：測試極端邊界（如：空值 Null/None、空陣列、長度為 0 的字串、極大/極小數值、負數）。
- **Exception Handling (異常處理)**：輸入不合法資料時，驗證程式是否如預期拋出特定的錯誤 (Error / Exception) 與訊息。

## 3. 隔離外部依賴 (Mocking & Isolation)
- 測試必須在完全隔离的沙盒中執行。
- 若程式碼包含資料庫存取 (DB)、網路請求 (API 呼叫)、本地檔案讀寫或系統時間，**必須使用該語言主流的 Mock 框架進行模擬**。
- 禁止在單元測試中發生真實的網路或資料庫連線。

## 4. 輸出格式與品質要求
- **語言自動適應**：依據使用者輸入的程式碼，自動選擇對應的測試生態系：
  - **Python**: pytest + unittest.mock
  - **JavaScript / TypeScript**: Jest 或 Vitest
  - **C#**: xUnit / NUnit + Moq
  - **Java**: JUnit 5 + Mockito
  - **Go**: testing + uber-go/mock
- **可讀性命名**：測試函式名稱必須清晰表達測試目的（例如：`test_[函式名]_[測試情境]_[預期結果]`）。
- **生產就緒 (Production-Ready)**：程式碼必須包含所有必要的 `import` 或 `using` 陳述句，確保使用者複製後可直接執行。
