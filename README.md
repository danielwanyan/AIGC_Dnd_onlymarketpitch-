# AIGC_Dnd_onlymarketpitch

视频纯营销叫卖判定 - 3 Jurors + 1 Chief Judge

## 目录结构

```
AIGC_Dnd_onlymarketpitch/
├── prompts/
│   ├── reviewer_system_prompt.txt              # 陪审员 System Prompt（原始版）
│   ├── reviewer_system_prompt_compressed.txt   # 陪审员 System Prompt（压缩版）
│   ├── reviewer_user_prompt.txt                # 陪审员 User Prompt（原始版）
│   ├── reviewer_user_prompt_compressed.txt     # 陪审员 User Prompt（压缩版）
│   ├── chief_judge_system_prompt.txt           # 裁判 System Prompt（原始版）
│   ├── chief_judge_system_prompt_compressed.txt# 裁判 System Prompt（压缩版）
│   ├── chief_judge_user_prompt.txt             # 裁判 User Prompt（原始版）
│   └── chief_judge_user_prompt_compressed.txt  # 裁判 User Prompt（压缩版）
├── rules/
│   ├── rules_text.txt                          # 判定规则（原始版）
│   └── rules_text_compressed.txt               # 判定规则（压缩版）
└── README.md
```

## 规则引用方式

规则通过 HTTP Request 引用 raw URL，让 `{{body}}` 占位符动态加载：

```
{{body}} → https://raw.githubusercontent.com/danielwanyan/AIGC_Dnd_onlymarketpitch-/main/rules/rules_text_compressed.txt
```

## Aicolate 节点配置

**陪审员 LLM 节点：**

| 字段 | URL |
|------|-----|
| System Prompt | `https://raw.githubusercontent.com/danielwanyan/AIGC_Dnd_onlymarketpitch-/main/prompts/reviewer_system_prompt_compressed.txt` |
| User Prompt | `https://raw.githubusercontent.com/danielwanyan/AIGC_Dnd_onlymarketpitch-/main/prompts/reviewer_user_prompt_compressed.txt` |
| Rules（HTTP Request → `{{body}}`） | `https://raw.githubusercontent.com/danielwanyan/AIGC_Dnd_onlymarketpitch-/main/rules/rules_text_compressed.txt` |

**裁判节点：**

| 字段 | URL |
|------|-----|
| System Prompt | `https://raw.githubusercontent.com/danielwanyan/AIGC_Dnd_onlymarketpitch-/main/prompts/chief_judge_system_prompt_compressed.txt` |
| User Prompt | `https://raw.githubusercontent.com/danielwanyan/AIGC_Dnd_onlymarketpitch-/main/prompts/chief_judge_user_prompt_compressed.txt` |

## 规则

MP01 — 纯营销叫卖。ASR + OCR 只有营销话术、无任何商品信息 → 命中。

### 数据质量检查（优先）

- ASR 乱码/语言错误/非人类语言 → 报错，需人工审核
- ASR 空 + OCR 正常 → 按 OCR-only 判定
- 两者都空 → 无营销，或标记数据缺失

### 判定逻辑

- 有营销话术 + 无商品信息 → HIT
- 有商品信息（功能、规格、用法、材质）→ NOT hit

## 压缩率

| 文件 | 原始 | 压缩 | 缩减 |
|------|------|------|------|
| reviewer_system_prompt | 4,367B | 3,129B | 28% |
| reviewer_user_prompt | 344B | 166B | 52% |
| chief_judge_system_prompt | 3,093B | 2,133B | 31% |
| chief_judge_user_prompt | 173B | 118B | 32% |
| rules_text | 8,598B | 2,138B | 75% |

## 版本

- 2026-07-03: 重构为纯营销叫卖（MP01），移除 LQ01/LQ03/LQ04，新增数据质量检查，全英文输出
- 2025-05-19-v3: 原始版本，4 规则决策树