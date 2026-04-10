# Rubric 輸出格式規範

本文件定義了 Rubric 的最終輸出格式。每次產出 Rubric 都必須同時提供 Markdown 和 JSON 兩種版本。

---

## Markdown 格式

給人閱讀、檢查、討論用。結構如下：

```markdown
# [領域] - [Task] 評估 Rubric

## 概要
- 領域：[領域名稱]
- 評估對象：[要評估什麼產出]
- 建立者：[使用者角色/身份]
- 建立日期：[日期]

## 維度總覽

| 維度 | 權重 | 說明 |
|------|------|------|
| [維度名稱] | 高/標準/低 | [一句話說明] |

## 詳細評分標準

### 維度 1：[名稱]｜權重：[高/標準/低]

**定義：** [這個維度在評估什麼]

**為什麼重要：** [這個維度對整體品質的影響]

| 分數 | 等級 | 描述 |
|------|------|------|
| 1 | 不及格 | [具體描述] |
| 2 | 不足 | [具體描述] |
| 3 | 合格 | [具體描述] |
| 4 | 優良 | [具體描述] |
| 5 | 卓越 | [具體描述] |

**典型的 5 分產出：** [用一兩句話描繪一個真正好的成果長什麼樣]
**典型的 1-2 分產出：** [用一兩句話描繪常見的失敗模式]

---

（以下每個維度重複同樣的結構）

## 權重設計說明
[說明為什麼某些維度的權重比較高，背後的判斷邏輯是什麼]

## 使用指南
- 評估時，先逐維度打分，再看整體
- 權重高的維度若不及格，整體不可能及格
- 3 分是「達到基本期望」，4 分是「超出預期」，5 分是「這就是標竿」
```

---

## JSON 格式

給機器讀、接入 Agent / Evaluator / Workflow 用。Schema 如下：

```json
{
  "rubric": {
    "domain": "string - 領域名稱",
    "task": "string - 要評估的 Task",
    "created_by": "string - 建立者角色",
    "created_at": "string - ISO date",
    "version": "string - 版本號",
    "dimensions": [
      {
        "id": "string - 維度 ID，例如 'typography'",
        "name": "string - 維度名稱",
        "weight": "high | standard | low",
        "definition": "string - 這個維度在評估什麼",
        "why_it_matters": "string - 為什麼重要",
        "scores": {
          "1": {
            "label": "不及格",
            "description": "string - 具體描述"
          },
          "2": {
            "label": "不足",
            "description": "string - 具體描述"
          },
          "3": {
            "label": "合格",
            "description": "string - 具體描述"
          },
          "4": {
            "label": "優良",
            "description": "string - 具體描述"
          },
          "5": {
            "label": "卓越",
            "description": "string - 具體描述"
          }
        },
        "exemplar_high": "string - 典型的 5 分產出描述",
        "exemplar_low": "string - 典型的 1-2 分產出描述"
      }
    ],
    "weight_rationale": "string - 權重設計的理由說明",
    "usage_notes": "string - 使用指南"
  }
}
```

---

## 格式規範重點

1. **每個維度的 1-5 分描述必須具體到可判斷**——不能只是「好/不好」，要描述到「看到什麼特徵就給這個分數」
2. **Exemplar 是必填**——高分和低分都要有具象描述，讓 Evaluator 有錨點
3. **權重必須有理由**——不是隨便分的，要說清楚為什麼某些維度更重要
4. **JSON 的 dimension id 要用英文 snake_case**——方便程式處理
5. **Markdown 和 JSON 的內容必須完全一致**——只是格式不同，不能有資訊差
