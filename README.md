# 小心愿 ⭐ 把成长装进星星罐

面向家庭的儿童成长激励工具。家长通过「心愿币（星愿币）」记录孩子的良好行为、家庭劳动及奖励消费，帮助孩子在日常生活中建立付出、积累和收获之间的联系。产品强调正向鼓励，不是惩罚工具。

> 在线体验：https://atwu5.github.io/star/

## 功能特性

- **首次引导**：使用说明 → 创建孩子 → 设置快捷项目 → 进入首页
- **星星储蓄罐**：首页视觉中心，随余额增减展示星星，获得时星星飞入罐中、数字滚动增长
- **获得 / 使用心愿币**：默认输入框 + 快捷项目标签（点击自动填充，可继续修改）；余额不足拦截；防重复提交
- **成长日历**：月度获得/使用统计、记录日圆点标识（绿=获得、橙=使用）、按日查看明细、支持跨月切换
- **明细记录**：独立页面（`#/records`），获得/使用两个 Tab，按时间倒序，支持「加载更多」
- **多孩子管理**：切换/添加孩子、数据完全隔离、编辑孩子姓名与心愿币名称、管理快捷项目
- **本地持久化**：localStorage 存储（含 schemaVersion 与损坏容错），刷新/重开浏览器不丢失
- **响应式**：PC 居中布局 + 手机底部弹层，支持 `prefers-reduced-motion`

## 技术实现

- 单文件 `index.html`：HTML5 + CSS3 + 原生 JavaScript，无任何第三方在线依赖
- 数据保存在浏览器 `localStorage`（key：`xiaoxinyuan_mvp_v1`），数据结构与后端账号体系友好：

```js
{
  schemaVersion: 1,
  currentChildId: "…",
  onboarded: true,
  children: [{
    id, name, currencyName, balance, createdAt, updatedAt,
    quickItems:  [{ id, childId, type: "earn"|"spend", name, amount, sortOrder, createdAt }],
    transactions:[{ id, childId, type: "earn"|"spend", amount, reason, operator, createdAt }]
  }]
}
```

- 流水 `amount` 恒为正整数，加减方向由 `type` 决定；余额始终与流水净额保持一致

## 本地运行

直接双击打开 `index.html` 即可；或起一个本地静态服务：

```bash
cd xiaoxinyuan
python3 -m http.server 8080
# 打开 http://localhost:8080
```

## 部署（GitHub Pages）

仓库 `atwu5/star`，Pages 从 `main` 分支根目录发布，访问地址：<https://atwu5.github.io/star/>

## MVP 范围说明

按需求 V1.0 明确不做：商城、兑换订单、转账、孩子独立登录、多人协作、重复任务、勋章、排行榜、AI 评价、成长报告、社交、通知、有效期、历史流水撤销/修改/删除、账号注册与跨设备同步。误操作可通过新增反向记录修正（如误加 10 个，可使用 10 个并注明「修正误加记录」）。
