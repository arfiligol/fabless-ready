---
title: STA
---
> [!question] 先定義「問題」
> 為什麼數位電路需要 STA？

## Preliminary Information（前情提要）
###### Problem Background
- 在 IC 設計中，[[Clock（時脈）| 時脈（Clock）]] 是用來同步所有訊號的核心，但實際上訊號傳遞不是瞬時的。
- 訊號會因為各種物理層面的 Delay（e.g [[Device-Level Delay（元件層延遲）]], [[Interconnect Delay（互聯延遲）]], 又或是 [[Clock Distribution Delay（時鐘分配延遲）#Clock Tree Delay（時鐘樹延遲） | Clock Distribution Delay 中的 Clock Tree Delay]]） 影響，使得訊號可能無法準時到達目的地，進而導致錯誤。
- 這些時序問題「**無法單靠 [[Functional Simulation（RTL Simulation） | RTL 模擬（Functional Simulation）]] 找出**」，因為 RTL 模擬只關心邏輯正確性（0/1），但不考慮**時間（Timing）**。
- 為了確保時序正確，必須透過「**[[STA（Static Timing Analysis, 靜態時序分析）| 靜態時序分析（Static Timing Analysis）]] 工具**」來驗證 **所有可能的訊號傳遞時間，確保每條路徑都符合時序約束**，否則會產生「**[[Timing Violations（時序違規，延遲累積的結果）| 時序違規（Timing Violation）]]**」。

###### 在哪些情況下，時序違規會發生
- [[Timing Violations（時序違規，延遲累積的結果）#Setup Time Violation（設定時間違規） | Setup Violation（設定時間違規）]]：訊號沒能在[[Clock Edge（時鐘邊緣）| 時鐘邊緣（Clock Edge）]]前準時到達，導致寄存器存入錯誤數據。
- [[Timing Violations（時序違規，延遲累積的結果）#Hold Time Violation（保持時間違規） | Hold Violation（保持時間違規）]]：訊號太快到達，導致新的數據覆蓋舊的數據，發生錯誤。
- 第三種可能影響時序的因素：[[Clock Distribution Delay（時鐘分配延遲）#Clock Jitter（時鐘抖動）| 時鐘抖動（Clock Jitter）]]、[[Clock Distribution Delay（時鐘分配延遲）#Clock Skew（時鐘偏移）| 時鐘偏移（Clock Skew）]]

###### Timing Violations 發生，會影響什麼？
- 設計功能無法正常運作（功能性錯誤）
- 影響功耗與效能[[PPA（Power, Performence, Area - 功耗與效能） |（PPA：Power, Performance, Area）]]
- 可能導致最終晶片無法 tap-out，影響產品上市時程

> [!todo] 待辦事項
> - Timing Violations 具體如何影響 PPA 尚未明瞭。

---
## STA 如何幫助我們解決時序問題？
