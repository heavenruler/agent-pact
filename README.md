# agentpact

將 [`PACT.md`](PACT.md) 貼給要建立共用公約的 agent。它先盤點現況，產出 diff 與雜湊供人審查，再安裝。`defaults/safety.md` 是保守規則，`modules/boundary-check/SKILL.md` 是選配的事前邊界檢查。Prompt 本身不能提供 hook 式強制攔截。

## 三種環境走查：預期產出

- **只有 Claude**：列出實際找到的 Claude 設定、memory、hook 與權限來源；若 hook 經驗證可用，才標「有強制攔截」。先給 diff/雜湊並等待確認，逐項回報選配元件。
- **只有 Codex**：列出實際找到的 Codex 設定、memory、sandbox/批准與 hook 能力；不存在的 Claude 入口標未知或未啟用。未證實 hook 時標「只有操作前檢查，無強制攔截」。先給 diff/雜湊並等待確認。
- **無 hook 的純聊天 agent**：只能交付規則文字、安裝預覽與人工操作步驟；hook 標「未啟用：平台不支援」，明說「只有操作前檢查，無強制攔截」。不能宣稱已安裝或已強制攔截。

## 安全界線

預設採階段 1：人確認具體 diff 與雜湊後才寫入。階段 2 需人手動開總開關，僅可附加一條更嚴的 deny/ask 規則。未知環境當最高風險級；既有平台政策優先，任何 prompt 都無法繞過權限控制。
