# F2E Spec Vue Skill

`f2e-spec-vue` 是一份用于 Vue 前端开发、代码审查和重构的编码规范 Skill。它以阿里巴巴 F2E Spec 为基础，保留原规范的通用、JavaScript/TypeScript、命名、注释、安全、无障碍和可维护性要求，并将 React 专属部分转换为 Vue 3 规范。

## 适用场景

在以下工作中启用或引用该 Skill：

- 编写 Vue 3 单文件组件、页面、Composable 或 TypeScript 工具代码
- 审查 Vue Template、Props、事件、响应式状态和生命周期代码
- 将现有 Vue 代码重构为更一致、可维护的写法
- 检查组件的性能、安全、可访问性和编码风格

## 使用方式

直接在任务中说明要遵循该规范即可：

```text
用 f2e-spec-vue 规范实现一个 Vue 3 + TypeScript 的表单组件。
```

```text
按 f2e-spec-vue 审查这个 Vue 组件，列出违反规范的问题并给出最小修改方案。
```

```text
将这段 Options API 代码重构为符合 f2e-spec-vue 的写法；不要改变已有功能。
```

## Vue 规则重点

- 新组件优先使用 Vue 3 SFC、`<script setup>` 和 Composition API；已有 Options API 组件遵循项目现有约定。
- 使用 `defineProps` 或 `props` 声明 Props 类型；不要直接修改 Props，通过 `emit` 通知父组件更新。
- 用 `ref`、`reactive` 管理本地状态；解构 Props 时保持响应式。
- 将生命周期钩子和依赖组件实例的 Composition API 在 `setup` 阶段同步注册。
- Composable 使用 `useXxx` 命名；`watch` 明确监听源并清理不再需要的副作用。
- Template 使用 2 空格缩进、双引号属性和稳定唯一的 `v-for` key；避免在模板内放置复杂表达式。
- 不使用 Vue 3 中已废弃的 Vue 2 API，例如 `beforeDestroy`、`destroyed` 和 filters。
- 使用 template ref 获取受控 DOM 引用；避免直接查询和操作 DOM。

## 通用规则

Skill 同时保留原 F2E Spec 的以下要求：

- 2 空格缩进、UTF-8、适当的空行和不超过 100 字符的推荐行宽
- 优先 `const`，仅在需要重新赋值时使用 `let`，禁止 `var`
- 使用严格相等、ES Modules、模板字符串、解构和扩展运算符
- 明确的命名、注释与模块边界
- 禁止 `eval` 和生产环境 `debugger`；谨慎处理控制台输出和不受信任的 HTML
- 为图片、链接和交互控件提供基本无障碍支持

## 审查清单

使用该 Skill 审查 Vue 代码时，重点检查：

1. 格式、导入、命名和 TypeScript 类型是否一致。
2. Props、事件、`ref`/`reactive` 和 Composition API 的职责是否明确。
3. Template 是否具有稳定 key、合理条件渲染和简洁表达式。
4. 是否存在已废弃 API、危险操作、无障碍缺失或不必要的响应式更新。
5. 改动是否在不改变功能的前提下保持最小且可维护。

## 配套工具

可按项目需要使用阿里巴巴 ESLint 配置：

```text
eslint-config-ali
eslint-config-ali/vue
eslint-config-ali/typescript/vue
```

最终以项目已有的 ESLint、Prettier、TypeScript、Vue 版本和组件库约定为准；本 Skill 用于补充和统一这些约定，而不是取代它们。

## 来源

- 阿里巴巴前端代码规范（F2E Spec）
- 阿里巴巴 `f2e-spec-skill` 的 Vue 转换版本
- Vue 官方文档