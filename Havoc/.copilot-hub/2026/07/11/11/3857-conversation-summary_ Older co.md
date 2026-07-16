## Goal
删除 Havoc 项目中服务端、客户端、木马端的远程文件管理(FS)功能,清理残留代码。

## Steps
- [x] 已完成 6 个文件的编辑(客户端 UI、handler 等)
- [x] 删除 teamserver demons.go 中 COMMAND_FS 的 TaskBuild case(原 line 204-477)
- [x] 删除 teamserver demons.go 中 COMMAND_FS 的 CommandOutput case(原 line 2549-2992)
- [x] 删除 teamserver commands.go 中 DEMON_COMMAND_FS_* 常量
- [x] 删除 payloads/Demon/src/core/Command.c 中残留的 ~380 行 FS 函数体
- [x] 验证编译无误

## Verification
- `grep COMMAND_FS demons.go` → 0 matches (both TaskBuild + CommandOutput cases removed)
- `grep DEMON_COMMAND_FS commands.go` → 0 matches (constants removed)
- `grep COMMAND_FS Command.c` → only Download.c reference (expected, not FS handler)
- `go build ./...` passes (only pre-existing system sframe linker warning)
- Language server reports 0 errors for demons.go, commands.go, Command.c

## Status
✅ Complete
