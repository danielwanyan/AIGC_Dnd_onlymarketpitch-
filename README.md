# AIGC_Dnd_onlymarketpitch

视频低质问题判定规则仓库

## 规则文件

- `rules/rules_text.txt` - 低质问题判定规则

## 规则列表

| 编号 | 规则名称 | 说明 |
|------|---------|------|
| LQ01 | AIGC纯商品展示 | AIGC + 纯商品/无人/纯肢体/捂嘴流 |
| LQ02 | AIGC仅营销叫卖 | AIGC + 无商品信息 + 只有营销话术 |
| LQ03 | 使用重复音频 | 30日内同语义音频 > 30 |
| LQ04 | 内容介绍不详细 | 电子/护肤/保健品必须展示+说明 |
| LQ05 | 非AIGC仅营销叫卖 | 非AIGC + 只有营销话术 |

## 规则文件 URL

```
https://raw.githubusercontent.com/danielwanyan/AIGC_Dnd_onlymarketpitch/main/rules/rules_text.txt
```

## 相关仓库

- [misleading-rules](https://github.com/danielwanyan/misleading-rules) - Misleading 问题判定规则
