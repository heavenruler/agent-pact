# 既有做法（2026-10-14）

已開啟原始專案頁檢視：

| 專案 | 判斷 | 理由 |
|---|---|---|
| [multi-agent-governance](https://github.com/simaba/multi-agent-governance) | 借做法 | 清楚拆出授權來源、傳遞與驗證；範圍偏完整治理框架，不適合作為單一 prompt 直接用。 |
| [agent-playbook-template](https://github.com/screenleon/agent-playbook-template) | 借做法 | 有可攜的規則與檢查點；其多檔模板及 harness 比本產品目標重。 |
| [agent-memory-system](https://github.com/Romadethat/agent-memory-system) | 不適用 | 偏持久記憶與協作系統實作；可提醒盤點 memory，但不能直接作為安裝公約。 |

因此以單一 `PACT.md` 作為入口，其他檔案只提供預設規則及選配模組。
