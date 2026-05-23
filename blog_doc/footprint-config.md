# Footprint 页面数据配置指南

Footprint 页面用于展示个人生活足迹，包括看过的电影、玩过的游戏、去过的地方和吃过的餐厅。

## 数据文件位置

所有数据均配置在 [`src/data/life.json`](../src/data/life.json) 中。

---

## 数据结构总览

`life.json` 包含四个数组字段：

| 字段 | 含义 | 对应页面区块 |
|------|------|-------------|
| `movies` | 电影记录 | Movies |
| `games` | 游戏记录 | Games |
| `travels` | 旅行/居住足迹 | Travels |
| `restaurants` | 餐厅记录 | Restaurants |

---

## 1. Movies（电影）

每条电影记录包含以下字段：

| 字段 | 类型 | 必填 | 说明 |
|------|------|------|------|
| `name` | string | 是 | 电影名称 |
| `poster` | string | 是 | 海报图片路径，建议放在 `/images/movies/` 目录下 |
| `review` | string | 是 | 个人影评或简短描述 |
| `date` | string | 否 | 观看日期，格式自由，如 `"2025-8"` 或 `"2024-12-25"` |

### 示例

```json
{
  "name": "守护解放西 6",
  "poster": "/images/movies/shouhujiefangxi.jpg",
  "review": "看到不同的人生，用他人的事件警示自己！",
  "date": "2025-8"
}
```

---

## 2. Games（游戏）

每条游戏记录包含以下字段：

| 字段 | 类型 | 必填 | 说明 |
|------|------|------|------|
| `name` | string | 是 | 游戏名称 |
| `description` | string | 是 | 游戏简介 |
| `href` | string | 是 | 游戏官网或 Steam 链接，点击卡片会跳转 |
| `icon` | string | 是 | 游戏图标/封面路径，建议放在 `/images/games/` 目录下 |

### 示例

```json
{
  "name": "Counter-Strike 2",
  "description": "世界上最好的FPS游戏",
  "href": "https://www.counter-strike.net/cs2",
  "icon": "/images/games/cs2.svg"
}
```

---

## 3. Travels（足迹）

足迹使用 `Timeline` 组件渲染，每条记录包含以下字段：

| 字段 | 类型 | 必填 | 说明 |
|------|------|------|------|
| `date` | string | 是 | 时间描述，支持自由格式，如 `"2023-07"` 或 `"2001-03 ~ Now"` |
| `content` | string | 是 | 地点描述，格式建议：`地点 — 备注` |

### 示例

```json
{
  "date": "2001-03 ~ Now",
  "content": "中国·上海 — Living Location"
}
```

---

## 4. Restaurants（餐厅）

每条餐厅记录包含以下字段：

| 字段 | 类型 | 必填 | 说明 |
|------|------|------|------|
| `name` | string | 是 | 餐厅名称 |
| `photo` | string | 是 | 餐厅照片路径，建议放在 `/images/restaurants/` 目录下 |
| `review` | string | 是 | 用餐评价或推荐语 |
| `date` | string | 否 | 就餐日期，留空字符串 `""` 表示不显示 |

### 示例

```json
{
  "name": "海底捞",
  "photo": "/images/restaurants/haidilao.jpg",
  "review": "番茄锅+虾滑永远的神，服务天花板",
  "date": ""
}
```

---

## 图片存放目录建议

| 类别 | 建议目录 |
|------|---------|
| 电影海报 | `public/images/movies/` |
| 游戏封面 | `public/images/games/` |
| 餐厅照片 | `public/images/restaurants/` |

> 注意：图片放在 `public/` 目录下，构建后会直接复制到站点根目录，引用路径以 `/images/` 开头。

---

## 完整示例

```json
{
  "movies": [
    {
      "name": "电影名称",
      "poster": "/images/movies/example.jpg",
      "review": "简短影评",
      "date": "2025-1"
    }
  ],
  "games": [
    {
      "name": "游戏名称",
      "description": "游戏简介",
      "href": "https://example.com",
      "icon": "/images/games/example.svg"
    }
  ],
  "travels": [
    {
      "date": "2024-10",
      "content": "中国·北京 — 出差"
    }
  ],
  "restaurants": [
    {
      "name": "餐厅名称",
      "photo": "/images/restaurants/example.jpg",
      "review": "味道不错",
      "date": "2025-2"
    }
  ]
}
```

---

## 注意事项

1. `life.json` 必须是合法的 JSON 格式，注意字段间用逗号分隔，最后一个元素后不要加逗号。
2. 图片路径使用 `/images/xxx` 开头的绝对路径，相对路径可能导致构建后无法正确加载。
3. 修改数据后保存文件，开发服务器会自动热更新页面。
