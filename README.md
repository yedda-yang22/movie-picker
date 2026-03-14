# 你更 喜欢哪部电影？🎬

豆瓣 Top 250 电影淘汰赛游戏

## 部署步骤

### 1. 创建 Supabase 表

在你的 Supabase 项目 → SQL Editor 中运行以下 SQL：

```sql
create table results (
  id bigint generated always as identity primary key,
  movie_title text not null,
  movie_region text not null,
  created_at timestamptz default now()
);

-- 允许匿名读写（游戏用）
alter table results enable row level security;

create policy "allow_insert" on results
  for insert to anon with check (true);

create policy "allow_select" on results
  for select to anon using (true);
```

### 2. 部署到 Vercel

1. 把整个文件夹上传到 GitHub 新仓库
2. 去 [vercel.com](https://vercel.com) 导入该仓库
3. 一键部署，完成！

### 3. 更新 GA 网址（可选）

部署完后，把 Vercel 给的域名填回 Google Analytics 的 Property 设置里。

## 文件说明

- `index.html` — 主页面，包含所有游戏逻辑
- `movies.js` — 电影数据（豆瓣 Top 250，按地区分类）
- `vercel.json` — Vercel 部署配置

## 技术栈

- 纯 HTML + CSS + JS（无框架依赖）
- Supabase（存储游戏结果 + 统计同选人数）
- Google Analytics（页面 PV + 每题退出埋点）
- html2canvas（截图分享）
- QRCode.js（生成二维码）
