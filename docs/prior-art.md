# 既有做法與差異（2026-10-14，已實際開啟各專案頁面核對）

| 專案 | 它是什麼 | 與 agentpact 的差異 | 判斷 |
|---|---|---|---|
| [multi-agent-governance](https://github.com/simaba/multi-agent-governance) | 多代理治理的文件框架（角色、決策權限、升級邏輯、問責、控制設計），多檔、MIT | 它是給人讀的治理文件；agentpact 是讓 agent 直接執行的單一 prompt | 借做法 |
| [agent-playbook-template](https://github.com/screenleon/agent-playbook-template) | 可攜的 AI 開發代理治理範本（AGENTS.md、skills、adapter、GitHub Actions、evals），MIT；**頁面標示已封存，實作移至 pm-dispatch** | 檔案多、需整套導入；且已封存 | 借做法 |
| [agent-memory-system](https://github.com/Romadethat/agent-memory-system) | 檔案式代理記憶系統模板（初始化腳本、skills、知識庫、多代理協調），MIT | 重點是持久記憶，不處理「進環境前的邊界」 | 不適用 |

結論：沒有看到「一個 prompt、讓各 agent 依自身 memory 現場生成邊界設定」的現成做法，所以自己做。
