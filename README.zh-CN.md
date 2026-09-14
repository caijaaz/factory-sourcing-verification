# factory-sourcing-verification

通用「找真实生产工厂 + 资质核验」方法论 Skill —— 从公开信息中挖掘并核验中国真实生产厂，剔除贸易商/皮包公司，产出可直接询盘的分级工厂池。

> A generic, category-agnostic skill for sourcing real manufacturing factories in China: verify qualifications, filter out traders, and deliver a ranked, inquiry-ready factory pool.
>
> **English README: [README.md](./README.md)**

## 它解决什么问题

外贸/采购找厂时最大的坑不是"找不到厂"，而是：

- 自称 manufacturer 的英文站，实际是参保 1 人的壳公司；
- 手持制备专利的"研发型公司"，根本没有生产许可；
- 有生产许可证，但**许可范围里没有目标产品**；
- 平台数据（企查查/天眼查）显示"存续"，实际信息滞后或张冠李戴。

本 skill 把一次真实出口找厂实战提炼为品类无关的通用流程，通过**多源交叉核验**而不是单信任何一家平台，判断"是不是真厂、能不能合规出货"。

## 五阶段工作流

```
阶段1 锁定需求与门槛  →  产品标识(CAS/型号) + 订单画像 + 硬性资质门槛 + 属地偏好
阶段2 分层渠道撒网    →  撒网层/反查层/实景核验层/出货铁证层 + 可选受限层（12 主线渠道）
阶段3 四维核验        →  存续 / 进出口资质 / 生产资质(看许可范围+有效期) / 目标产品在产
阶段4 分级与剔除      →  ★铁证首选 / Tier-1~3 / 剔除（必须记录死因，防重复捞回）
阶段5 交付            →  Excel 资质汇总表(9列池+剔除表) + PDF 工厂卡片 + 问厂话术
```

核心判断标准见 `references/verification-rules.md`（证据强度四级：铁证 > 强证 > 弱证 > 无效）。

## 安装

需要一个支持 skill 的 agent（如 Claude Code、WorkBuddy，或任何遵循 `SKILL.md` 约定的 agent）。

**用 git（用户级）：**

```bash
git clone https://github.com/caijaaz/factory-sourcing-verification.git <agent-skills-dir>/factory-sourcing-verification
```

将 `<agent-skills-dir>` 替换为你所用 agent 的用户级 skills 目录。之后说"找工厂 / 验厂 / 资质核验 / 剔除贸易商"即自动触发。

**不用 git / 其它 agent：** 在本仓库页面点 **`Code` → `Download ZIP`**，解压后把 `factory-sourcing-verification/` 整个目录放进该 agent 的 skills 目录（目录位置按各 agent 约定）。

## 目录结构

```
factory-sourcing-verification/
├── SKILL.md                        # 主入口：五阶段流水线 + 输入输出 + 决策红线
├── README.md                       # 英文说明（主）
├── README.zh-CN.md                 # 本文件（中文）
├── LICENSE                         # MIT
├── requirements.txt                # 脚本依赖：openpyxl
├── references/
│   ├── channels.md                 # 分层渠道矩阵（12 主线 + 可选受限层）
│   ├── verification-rules.md       # 四维核验细则 + 典型翻车模式
│   └── inquiry-template.md         # 问厂话术（电话四连问 + 询价邮件模板）
└── scripts/
    └── gen_factory_xlsx.py         # Excel 资质汇总表生成模板
```

## 输入与输出

**输入（缺一项就先问）：** 产品名+唯一标识、订单画像（数量/柜型/目标市场）、硬性资质门槛（按优先级）、属地偏好、交付形式偏好。

**输出：**

1. Excel 资质汇总表：表1「真实生产厂池」9 列（厂家/存续/进出口资质/生产资质/目标产品在产/定位/联系方式/地址/生产规模）+ 表2「剔除名单与方法」
2. PDF 工厂卡片清单（每厂一卡 + 风险提示）
3. 对话内分级结论 + 下一步行动建议

## 脚本依赖

```bash
pip install -r requirements.txt   # openpyxl
python scripts/gen_factory_xlsx.py 输出路径.xlsx
```

## 合规与免责

- 全部信息来自**公开渠道多源交叉核验**（政府公示、行业名录、公开报道等），不依赖任何未经授权的批量抓取；数据公开 ≠ 爬取合规，请勿突破任何网站技术措施。
- 工商/资质信息可能滞后或变动，正式合作前请向工厂书面复核并以最新官方文件为准。
- 本仓库为方法论工具，输出仅供参考，不构成法律或商业建议。

## License

[MIT](./LICENSE) © 2026 Factory Sourcing Verification contributors
