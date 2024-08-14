# 第一阶段：构建阶段
FROM node:18-alpine AS build

# 设置工作目录
WORKDIR /app

# 复制依赖定义文件（仅 package.json 和 package-lock.json）
COPY package*.json ./

# 安装所有依赖（包括开发依赖）
RUN npm install

# 复制应用代码，排除掉 node_modules（受 .dockerignore 控制）
COPY . .

# 使用 Nest CLI 进行项目编译
RUN npm run build

# 第二阶段：生产阶段
FROM node:18-alpine

# 设置工作目录
WORKDIR /app

# 复制编译后的代码
COPY --from=build /app/dist ./dist

# 复制 package.json 和 package-lock.json
COPY --from=build /app/package*.json ./

# 安装仅生产环境需要的依赖
RUN npm install --production

# 暴露应用端口
EXPOSE 3000

# 启动应用
CMD ["node", "dist/main.js"]