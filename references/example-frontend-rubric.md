# 參考範例：Anthropic Frontend Design Rubric（含 1-5 分 Few-Shot）

這份檔案是給 skill 在 Step 4 使用的**顆粒度校準工具**。

當你跟使用者展開每個維度的 1-5 分描述時，**對照這份範例的格式與具體程度**。你的產出要達到這份範例的具體性——每一分都是「可掃描的可觀察行為」，不是抽象品質形容詞。
---

## 結構：兩層維度

frontend 評估其實是**兩層結構**：

### 美學支柱（Aesthetic Pillars）｜標準權重
你在執行時要顧的具體面向。Claude 預設在這些上面就有一定水準。

1. Typography（字體）
2. Color & Theme（色彩與主題）
3. Motion（動效）
4. Spatial Composition（空間構成）
5. Backgrounds & Visual Details（背景與視覺細節）

### 整體判準（Holistic Dimensions）｜高權重在前兩項
評估時看「整體」是不是達到水準。Anthropic 刻意加重前兩個，因為 Claude 在這兩個上面最常出 AI slop。

6. **Design Quality**（設計品質）｜**高權重**
7. **Originality**（原創性）｜**高權重**
8. Craft（工藝）｜標準權重
9. Functionality（功能性）｜標準權重

權重邏輯：**權重反映瓶頸位置，不是「什麼都一樣重要」。**

---

# 美學支柱（Aesthetic Pillars）

---

## 1. Typography（字體）

選用美觀、獨特、有個性的字體；Display + Body 配對形成層次。

**Check for**：
- 是否使用獨特的 display font 作為標題？
- Display 與 body 之間是否有明確的字體層次（不只字級不同）？
- 是否避開 AI 預設字體（Inter、Roboto、Arial、system-ui）？
- 字體選擇是否與整體美學一致？
- 跨頁面 / 組件的字體使用是否有意圖（不是隨手套）？

**Scoring**：

| 分數 | 判準 |
|------|------|
| 1 | 全站使用 Inter、Roboto、Arial 或 system-ui；無 display/body 區分；看起來像 unstyled Tailwind preset。 |
| 2 | 用了一種非預設字體，但所有層級只靠 font-weight/size 區分；字體選擇與內容主題無關。 |
| 3 | 有 display + body 配對，但兩者性格相近（兩個都是中性 sans-serif，如 Inter + Geist Sans）；字體可讀但無記憶點。 |
| 4 | Display 字體有性格（serif、襯線變化、變體寬度，如 IBM Plex Serif、Söhne）；body 易讀；兩者形成明確視覺對比。 |
| 5 | Display 字體本身就是設計宣言（Editorial New、GT Sectra、PP Editorial、Migra）；body 字體獨立挑選且呼應 display 氣質；字體選擇承擔了一半的美感傳達。 |

**5 分典型樣態**：Display 用 PP Editorial Old 大字體當作 hero，body 用 Geist Mono 形成 serif/mono 對比，字體本身就傳達了「editorial × technical」的雙重定位。

**1-2 分典型樣態**：`font-family: system-ui, -apple-system, sans-serif` 或全站 `font-family: 'Inter'`，所有層級只用 `font-weight: 400/600/700` 區分。

---

## 2. Color & Theme（色彩與主題）

承諾一個連貫的美學方向；主色搭配銳利強調色，優於平均分配的膽怯配色。

**Check for**：
- 是否使用 CSS variables 確保跨組件一致性？
- 是否有明確的主色 + accent 系統，還是平均分配的灰階堆？
- 配色是否承擔了**主題**（不只是裝飾）？
- 是否避開 AI cliché 配色（紫漸層在白卡片、藍漸層在深色背景、霓虹漸層按鈕）？
- 移除顏色之後，產品還認得出來嗎？

**Scoring**：

| 分數 | 判準 |
|------|------|
| 1 | 直接用 Tailwind 預設 palette；通篇灰底 + 藍色 CTA；或踩了 AI cliché（紫漸層白卡片、紫粉霓虹）。 |
| 2 | 有自訂主色但配色膽怯——主色低彩度、accent 與主色色相相近、整體 wash out。 |
| 3 | 有 CSS variables 結構；配色完整但平均分配（每個色塊權重差不多）；安全牌但無立場。 |
| 4 | 主色強烈 + 銳利 accent（高彩度對比或互補色）；配色有明確態度；可辨識的色彩識別。 |
| 5 | 色彩選擇本身就是品牌——換掉顏色等於換掉產品身份；主色與 accent 形成記憶點；色彩承擔美學氛圍的 50% 以上。 |

**5 分典型樣態**：深墨綠 (#0F2E25) 為主色 + 鮮橘 (#FF6B35) 為唯一 accent，整站不用其他彩色；用 negative space 與 typography 取代色彩堆疊；色彩出現處全部是關鍵 CTA 或重點。

**1-2 分典型樣態**：`bg-gray-50` + `text-gray-900` + `bg-blue-600` CTA，所有 card 都帶 `from-purple-500 to-pink-500` 漸層。

---

## 3. Motion（動效）

聚焦高影響力時刻——一個精心編排的頁面載入 > 零散的微互動。

**Check for**：
- 是否有「高影響力時刻」（精心編排的進場、scroll-triggered 場景變化）？
- 動畫是否服務於敘事，還是裝飾性的 hover state 鋪設？
- HTML 是否優先用 CSS-only？React 是否用 Motion library？
- Stagger 與 delay 是否有節奏感？
- 動效是否會讓人想再看一遍？

**Scoring**：

| 分數 | 判準 |
|------|------|
| 1 | 完全沒有動效；或每個按鈕都套同一個 `transition-all duration-200`（cargo cult 動效）。 |
| 2 | 有零散的 hover scale / fade-in，但無編排——所有元件同時觸發、無 stagger、無焦點。 |
| 3 | 該有過場的地方有過場（modal fade、page transition），但沒有「驚喜時刻」。 |
| 4 | 至少一個被精心編排的時刻——例如頁面進場有 staggered reveals、scroll 到特定點觸發特定動效；動效服務於閱讀節奏。 |
| 5 | 動效本身就是記憶點——可能是 hero 段的 choreographed reveal、可能是 scroll-triggered 場景轉換、可能是 cursor 互動驚喜；移除這個動效，整個體驗會少一半。 |

**5 分典型樣態**：Landing page 進場時 hero 字逐字打出（GSAP SplitText）、背景 grid 從中心向外擴散、accent color 線條沿 viewport 邊緣繪出——全部在 1.2 秒內完成且彼此呼應。

**1-2 分典型樣態**：`hover:scale-105 transition-all` 灑在所有 card 上；或完全靜態無動效。

---

## 4. Spatial Composition（空間構成）

非預期的版面配置——不對稱、重疊、對角線流動、打破格線。

**Check for**：
- 是否打破 12-col grid 的預設站位（hero 居中、cards 三欄、footer 四欄）？
- 是否有不對稱、重疊、對角線流動？
- 留白是否被用作構圖元素，不是預設 padding？
- Density 與 negative space 是否有對比？
- 把所有顏色字體拿掉、只剩黑白方塊，構圖還站得住嗎？

**Scoring**：

| 分數 | 判準 |
|------|------|
| 1 | 直接 Tailwind 預設站位——hero 居中、三欄 cards、四欄 footer；所有區塊等寬等高。 |
| 2 | 有些變化但仍對稱——左右兩欄、上下兩段，無打破格線的元素。 |
| 3 | 有留白策略，部分非對稱（hero 偏左、image 偏右），但仍 grid-aligned。 |
| 4 | 多處非對稱、重疊；元素跨越 grid 邊界；density 與 negative space 有明顯對比與節奏。 |
| 5 | 版面本身就是表達——對角線流動、戲劇性留白、刻意的密度堆疊；layout 即內容；把元素內容換掉，版面感還在。 |

**5 分典型樣態**：Hero 區域只佔 40% viewport、剩下 60% 是空白；下一段卻是滿版密集排列的卡片牆形成節奏對比；中間用一條對角線元素串連。

**1-2 分典型樣態**：`<div className="container mx-auto grid grid-cols-3 gap-6">` 重複四次。

---

## 5. Backgrounds & Visual Details（背景與視覺細節）

營造氛圍與深度，不是預設純色背景。

**Check for**：
- 背景是否承擔氛圍營造，還是預設 `bg-white` / `bg-black`？
- 是否有與美學匹配的紋理（gradient mesh、noise、grain、geometric patterns）？
- 是否有戲劇性陰影、自定義 cursor、裝飾性邊框？
- 細節層次是否多層次（不只一個 gradient 就交差）？
- 把背景移除後，介面氣質是否消失？

**Scoring**：

| 分數 | 判準 |
|------|------|
| 1 | 純白 / 純黑 / Tailwind 預設 `bg-gray-50` 背景；無紋理無深度。 |
| 2 | 一個 CSS gradient 或一張預設 hero image，但與整體美學無關聯。 |
| 3 | 有 noise / texture，但是 decorative add-on，不是整合進設計語言。 |
| 4 | 多層次背景元素（gradient mesh + grain overlay + 裝飾邊框）；元素之間有層次與呼應；背景參與美學表達。 |
| 5 | 背景與內容地位等齊——移除背景 = 失去身份；可能是 animated noise field、可能是 procedural pattern、可能是 layered transparencies；背景本身就是個值得截圖的設計。 |

**5 分典型樣態**：背景是緩慢漂浮的 grain + procedural mesh gradient，搭配 viewport 邊緣的細線 grid overlay 與 cursor-following light spot；五個元素層層疊但不互搶。

**1-2 分典型樣態**：`<body className="bg-white">` 或單一 `bg-gradient-to-br from-purple-500 to-pink-500`。

---

# 整體判準（Holistic Dimensions）

---

## 6. Design Quality（設計品質）｜**高權重**

整個設計是否感覺像一個連貫的整體，而非零件的拼湊。

**Check for**：
- 各部分（color、typography、layout、imagery）是否服務於同一個設計意圖？
- 移除任一元素，整體是否會弱化（而不是維持原樣）？
- 是否有可辨識的「設計語言」——一致的決策邏輯？
- 不同頁面 / section 之間是否視覺呼應？
- 你能用三個形容詞描述這個設計的氣質嗎？

**Scoring**：

| 分數 | 判準 |
|------|------|
| 1 | 看起來像多個 template 拼起來——每個 section 風格不同、字體配色不一致；像是不同人做的縫合怪。 |
| 2 | 元件個別 OK 但彼此無關——每張卡片自己合理，但放在一起像家具店展示。 |
| 3 | 有 design system 痕跡，但氣質平庸——所有東西「都對」但「沒一個讓人記得」。 |
| 4 | 明確的視覺方向——color/font/motion 都服務同一個美學 POV；可辨識的識別。 |
| 5 | 設計即身份——一眼可辨識、每個元素強化同一個美學 POV；可被歸類進特定 aesthetic（editorial、brutalist、cyberpunk、organic...）並執行到底。 |

**5 分典型樣態**：整站走 "editorial × technical" 方向——serif display + mono body + 高彩度 single accent + 戲劇性留白 + grain texture，五個元素全部都在說同一件事。

**1-2 分典型樣態**：Hero 用紫漸層、cards 用陰影白底、footer 用黑底白字、CTA 用 outline button——四種不同設計語言並列。

---

## 7. Originality（原創性）｜**高權重**

是否有「人做的決定」的痕跡，還是 AI 預設模板？

**Check for**：
- 是否有自定義的設計決策，還是套版 / library default？
- 是否有 AI 生成的典型模式——紫漸層蓋白卡片、hero + 3 個 metric box、相同的 card grid、icon + heading + description 三件套？
- 有沒有至少一個「我沒看過這樣做」的元素？
- 字體 / 色彩 / 元件選擇是否避開所有最常見的 AI 預設？
- 人類設計師會不會說「這是刻意選的」？

**Scoring**：

| 分數 | 判準 |
|------|------|
| 1 | 通篇 AI slop tells——紫漸層白卡片、hero + 3 metric box、Inter + 系統灰、shadcn 預設未修改、glassmorphism + dark glow。直接不及格。 |
| 2 | 有試圖客製但仍辨識得出 AI templates——可能改了主色，但 layout、字體、元件結構都是預設。 |
| 3 | 客製化程度足夠，但選擇都走「最常見的安全路徑」——SaaS landing convention、Stripe-style hero、Linear-style cards。 |
| 4 | 至少 2-3 個非 AI 預設的設計決策——可能是字體選擇、可能是 layout 結構、可能是動效編排。 |
| 5 | 設計師看了會說「我沒看過這樣做」——值得被截圖收藏、值得被討論；每個關鍵決策都是刻意的不選熱門選項。 |

**5 分典型樣態**：用 `text-align: justify` + 寬窄 column 切換做 hero、Display 字體用反白 + 大量 negative space、scroll 時整個 viewport 翻頁而非滾動——三個都不是 AI 會預設選的方向。

**1-2 分典型樣態**：「紫漸層 hero + 三個白色 metric card + dark mode toggle + Inter 字體」這種組合直接 1 分，無例外。

---

## 8. Craft（工藝）｜標準權重

技術執行——字體層次、間距一致性、色彩和諧、對比度。

**Check for**：
- 字體層次是否清楚（h1 vs h2 vs body 不只是 size 差）？
- 間距系統是否一致（用了 4/8/16/24 還是亂用 7px 11px）？
- 配色是否和諧（hover / focus / disabled 狀態的對比是否合理）？
- 對比度是否符合 WCAG（重要文字 ≥ 4.5:1）？
- 細節是否都精修過（圓角一致、border 一致、icon 大小一致）？

**Scoring**：

| 分數 | 判準 |
|------|------|
| 1 | 對齊歪掉、間距亂用、字體層次不清；不同地方的相同元素（button、card）規格不一致；對比度低到看不清。 |
| 2 | 大致 OK 但多處小不一致——按鈕 padding 各處不同、圓角混用、字體 size 跳階。 |
| 3 | 技術上乾淨——Tailwind / shadcn 預設等級的 craft；無明顯錯誤但無 craft 亮點。 |
| 4 | 間距系統明確套用；字體層次有節奏；對比刻意；hover/focus/disabled 狀態都處理過。 |
| 5 | 每個細節都被校準——pixel-level 精度；spacing 決策有數學感（如 golden ratio、modular scale）；字體 letter-spacing 微調過；hover state 有微互動。 |

**5 分典型樣態**：所有 padding 都用同一 8/16/24/32/48/64 modular scale；字體有 -0.02em letter-spacing 微調；border-radius 12px 全站一致；focus ring 有自訂顏色與時序。

**1-2 分典型樣態**：按鈕 padding `px-3 py-2` 跟 `px-4 py-2.5` 並列；圓角 4px / 8px / 12px 混用；body 文字 `#999` 在白底（對比不足）。

---

## 9. Functionality（功能性）｜標準權重

與美學無關的可用性——使用者能否理解介面、找到主操作、完成任務而不需要猜。

**Check for**：
- 使用者一眼看出「這頁要做什麼、主操作在哪」嗎？
- 主 CTA 是否唯一且明顯？
- 導航是否清楚（不是 icon-only）？
- 表單 / 互動是否有清楚的 loading / error / empty state？
- 你需要對使用者解釋怎麼用嗎？

**Scoring**：

| 分數 | 判準 |
|------|------|
| 1 | 看不出這頁是幹嘛的；主操作不存在或埋在四個 menu 後面；無 loading / error state。 |
| 2 | 主操作存在但要找——可能 CTA 太弱、可能跟其他按鈕同重量、可能位置詭異。 |
| 3 | 標準可用性——能用、需要稍微想一下、states 大致處理。 |
| 4 | 主 CTA 一眼可見；次要路徑可發現；loading / error / empty / success 四種狀態都處理。 |
| 5 | 任務完成毫無阻力——介面消失感（你只記得做了什麼，不記得介面長怎樣）；連 edge cases 都優雅處理（空狀態有 helpful illustration、錯誤訊息可 actionable）。 |

**5 分典型樣態**：用戶第一次進站不用 onboarding 就能找到主操作；錯誤訊息會告訴你「Email 缺 @」而不是「Invalid input」；空狀態不是 "No data" 而是「還沒有資料——這裡就是你的第一筆」+ CTA。

**1-2 分典型樣態**：四個 CTA 同樣大小同樣顏色；錯誤訊息只顯示 "Error: 500"；表單送出沒有 loading state。

---

# Total Score Mapping

| 總分（9 維度 × 5） | 評等 | 意義 |
|--------------------|------|------|
| 40-45 | 卓越 | 可以直接交付給客戶 / 上 portfolio |
| 33-39 | 優良 | 微調 polish 後可上 production |
| 24-32 | 合格 | 還在 AI slop 邊緣，需要重點補強 high-weight 維度 |
| 15-23 | 不足 | 需要重做主要美學決策 |
| 9-14 | 不及格 | 整體重來，重新選擇美學方向 |

加權版本（Design Quality + Originality 各 × 2）：

| 加權總分（11 維度 × 5 = 55） | 評等 |
|------------------------------|------|
| 48-55 | 卓越 |
| 40-47 | 優良 |
| 28-39 | 合格 |
| 18-27 | 不足 |
| 11-17 | 不及格 |

---

# 給校準者的提醒

當你看到一個前端產出時，**先看 Originality（第 7 項）**——如果直接踩到紫漸層白卡片、hero + 3 metric box 這種 AI cliché，整體就不可能 ≥ 3 分。

然後看 Design Quality（第 6 項）——如果各組件之間明顯沒有設計語言一致性，第 1-5 的支柱再強也沒救。

最後才逐一打 1-5 的細項分。

**這個順序很重要：先過 AI slop 篩，再看細節。**
