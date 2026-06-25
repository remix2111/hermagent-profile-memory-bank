# 安装方式

## 方式一：手动复制（最快）

```bash
mkdir -p ~/.hermes/skills/profile-memory-bank/
cp skills/profile-memory-bank/SKILL.md ~/.hermes/skills/profile-memory-bank/
```

然后在 Hermes 会话中加载：
```
/skill profile-memory-bank
```

## 方式二：git clone

```bash
git clone https://github.com/remix2111/hermagent-profile-memory-bank.git /tmp/hermagent-profile-memory-bank
cp -r /tmp/hermagent-profile-memory-bank/skills/profile-memory-bank ~/.hermes/skills/
rm -rf /tmp/hermagent-profile-memory-bank
```

## 方式三：Hermes Skills Hub（推荐）

```bash
hermes skills install profile-memory-bank
```

## 验证

安装后在任意 profile 加载技能，Agent 会检查 memory-bank 目录：

```
/skill profile-memory-bank
```

如果缺失文件会自动创建模板。
