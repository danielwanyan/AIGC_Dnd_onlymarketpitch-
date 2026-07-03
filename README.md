# AIGC_Dnd_onlymarketpitch

视频低质问题判定规则仓库

## 规则文件

| 文件 | 说明 | Raw URL |
|------|------|---------|
| `rules/rules_text.txt` | 原始版规则（含详细示例和说明） | `https://raw.githubusercontent.com/danielwanyan/AIGC_Dnd_onlymarketpitch/main/rules/rules_text.txt` |
| `rules/rules_text_compressed.txt` | 压缩版规则（精简核心逻辑，英文） | `https://raw.githubusercontent.com/danielwanyan/AIGC_Dnd_onlymarketpitch/main/rules/rules_text_compressed.txt` |

## 规则列表

| 编号 | 规则名称 | 说明 |
|------|---------|------|
| LQ01 | 同质化音频 | 30日内同语义音频 > 30 |
| LQ02 | 纯营销叫卖 | 只有营销话术，无商品信息 |
| LQ03 | 货不对板(IPP) | 视频展示商品 ≠ 挂车商品主图 |
| LQ04 | 信息不详细 | 电子/护肤/保健品必须展示+说明 |

## 决策流程

顺序检查，先命中优先：

```
audio_duplicate_count > 30? → LQ01
    ↓
纯营销叫卖? → LQ02
    ↓
货不对板? → LQ03
    ↓
信息不详细? → LQ04
    ↓
无问题
```

## 豁免

- E1: 化妆视频（GRWM）→ OK
- E2: 卡牌开箱视频 → OK
- E3: 派对桌游介绍视频 → OK
- LQ03 豁免: 盲盒/首饰/玉石/卡牌同三级类目; 服饰同SPU不同SKU

## 版本

- 2025-05-19-v3: 当前版本，支持 AIGC + 非AIGC
- 压缩版 (2026-07-03): 英文精简，8598B → 2967B (65% reduction)

## 相关仓库

- [AIGC_DND](https://github.com/danielwanyan/AIGC_DND) - Description is not detailed 评估
- [misleading-rules](https://github.com/danielwanyan/misleading-rules) - Misleading 问题判定规则