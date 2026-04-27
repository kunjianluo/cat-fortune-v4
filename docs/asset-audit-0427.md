# 《Meowracle Hat》PRD 0427 图片素材审计报告

## A. Asset folder overview

- 检查根目录：`/Users/jankun/Coding/Game/cat_fortune_asset_submission_pack_minimal/images`
- 扫描到图片/GIF文件总数：33
- 子目录：
  - `background`
  - `card`
  - `cat images`
  - `information column`
  - `others`
  - `unit`
- 扩展名统计：
  - `.png`：30
  - `.jpg`：1
  - `.gif`：2

## B. Direct matches

| PRD expected name | found path | match type |
| --- | --- | --- |
| `street_MeowracleHat.jpg` | `images/background/street_MeowracleHat.jpg` | exact |
| `bar-rest cat.png` | `images/background/bar-rest cat.png` | exact |
| `bar-wizard cat.png` | `images/background/bar-wizard cat.png` | exact |
| `street_3shop back.png` | `images/background/street_3shop back.png` | exact |
| `dessert_inside.png` | `images/background/dessert_inside.png` | exact |
| `ice cafe_inside.png` | `images/background/ice cafe_inside.png` | exact |
| `food stall_inside.png` | `images/background/food stall_inside.png` | exact |
| `transformation_1.gif` | `images/others/transformation_1.gif` | exact |
| `image transformation.gif` | `images/others/image transformation.gif` | exact |
| `PUSH button.png` | `images/others/PUSH button.png` | exact |
| `dialog box.png` | `images/others/dialog box.png` | exact |
| `option frame.png` | `images/card/option frame.png` | exact |
| `ring.png` | `images/others/ring.png` | exact |
| `home.png` | `images/unit/home.png` | exact |
| `return.png` | `images/unit/reture.png` | fuzzy |
| `logo.png` | `images/unit/logo.png` | exact |
| `l.career.png` | `images/card/I.career.png` | fuzzy |
| `l.society.png` | `images/card/I.society.png` | fuzzy |
| `l.emotion.png` | `images/card/I.emotion.png` | fuzzy |
| `l.city.png` | `images/card/I.city.png` | fuzzy |
| `l.desire.png` | `images/card/I.desire.png` | fuzzy |
| `dessert_building.png` | `images/others/dessert_building.png` | exact |
| `ice cafe_building.png` | `images/others/ice cafe_building.png` | exact |
| `food stall_building.png` | `images/others/food stall_building.png` | exact |
| `dessert_cat.png` | `images/cat images/dessert_cat.png` | exact |
| `ice cafe_cat.png` | `images/cat images/ice cafe_cat.png` | exact |
| `food stall_cat.png` | `images/cat images/food stall_cat.png` | exact |
| `half-successful.png` | `images/cat images/half-successful.png` | exact |
| `fail.png` | `images/cat images/fail.png` | exact |
| `successful.png` | `images/cat images/successful.png` | exact |
| `wizard cat.png` | `images/cat images/wizard cat.png` | exact |
| `claw.png` | `images/unit/claw.png` | exact |
| `feather.png` | `images/unit/feather.png` | exact |

匹配统计：exact 27，fuzzy 6，合计 33。

## C. Missing assets

按文件名模糊匹配后，未发现完全缺席的 PRD 0427 预期图片素材。

- backgrounds：无
- transitions/others：无
- unit icons：无；但 `return.png` 仅找到疑似拼写版本 `reture.png`
- level-1 cards：无；但卡牌文件使用 `I.` 前缀，不是请求清单中的 `l.` 前缀
- shop buildings：无
- cat characters：无
- punishments：无

缺失统计：0。

## D. Extra assets

未发现超出 PRD 0427 图片清单的额外图片/GIF文件。

额外素材统计：0。

## E. Naming/path mismatches

- PRD/request expects `images/unit/return.png`，实际为 `images/unit/reture.png`。这是最高风险命名问题，若代码按 PRD 直连会 404。
- PRD/request expects `images/card/l.career.png`、`l.society.png`、`l.emotion.png`、`l.city.png`、`l.desire.png`，实际为 `images/card/I.career.png`、`I.society.png`、`I.emotion.png`、`I.city.png`、`I.desire.png`。需要确认前缀是小写 L 还是大写 i。
- PRD 把 `option frame.png` 写在 `images/card/option frame.png`，本次请求将其归入 transitions/others；实际文件在 `images/card/option frame.png`，文件名可用但分组与请求清单不一致。
- PRD 惩罚图路径写作 `images/unt/claw.png`、`images/unt/feather.png`，实际为 `images/unit/claw.png`、`images/unit/feather.png`。疑似 PRD 路径笔误。
- 店铺建筑文件实际放在 `images/others/`，与 PRD 0427 中画面3的 `others/..._building.png` 描述一致；如果实现侧按“shop building”独立目录查找，需要映射。
- 猫角色目录名实际为 `images/cat images/`，包含空格；实现时建议通过映射表引用，避免路径手写出错。

## F. Implementation readiness

判断：需要先建立命名/路径映射表，再接入。

- Ready to wire immediately：背景、转场、商店建筑、猫角色、铃铛、对话框、PUSH按钮、惩罚图基本可接。
- Needs renaming/mapping table：一级卡牌 `l.*` vs `I.*`、`return.png` vs `reture.png`、`cat images` 空格目录、`unit`/`unt` 路径差异。
- Missing critical assets：无。
- Missing optional assets：无。

## G. Suggested next step

推荐：1. Create an asset mapping JSON without renaming files。

理由：素材本体基本齐全，但存在少量命名/路径不一致。先用映射 JSON 固化 PRD 名称到实际文件路径，可以不改动队友提交的资产，也能避免运行时路径散落在代码中。

## Self-check report

- total files scanned：33
- asset-audit-0427.md created：yes
- direct/fuzzy matches：33（exact 27，fuzzy 6）
- missing PRD assets：0
- extra assets：0
- files modified other than `cat-fortune-v3/docs/asset-audit-0427.md`：no
