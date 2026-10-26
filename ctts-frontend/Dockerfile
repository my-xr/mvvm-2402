# ============================================
# CTTS 前端多阶段构建 Dockerfile
# 阶段1：Node 构建阶段（产出 dist 静态文件）
# 阶段2：Nginx 部署阶段（托管 dist）
# ============================================

# ---------- 阶段1：构建阶段 ----------
FROM node:20-alpine AS builder

WORKDIR /build

# 先 COPY package.json 和 lock 文件，再 npm ci（利用层缓存）
COPY package.json package-lock.json* ./
RUN npm ci

# COPY 源码
COPY . .

# 构建产出 dist 目录
RUN npm run build

# ---------- 阶段2：运行阶段 ----------
FROM nginx:alpine

# 从构建阶段复制 dist 到 Nginx 默认静态目录
COPY --from=builder /build/dist /usr/share/nginx/html

# 复制自定义 Nginx 配置（可选，用于 history 路由 + API 代理）
COPY nginx.conf /etc/nginx/conf.d/default.conf

# 声明端口
EXPOSE 80

# Nginx 镜像默认 CMD 即 nginx -g 'daemon off;'，无需重复指定