---
id: SYS-REPOSITORY-REGISTRY
type: registry
status: active
project: "[[10-project/Project VstState|Project VstState]]"
created: 2026-09-16
updated: 2026-09-16
tags:
  - system
  - repositories
---

# Repository Registry

> [!info] Path convention
> Vault hiện nằm trong **Obsidian/ET4920**. Repository nằm dưới **Research**, nên mọi path được ghi tương đối từ vault root để tránh khóa vào tên user hoặc ổ đĩa.

| Repository | Relative path | Vai trò | Source note |
|---|---|---|---|
| VstHelper | ../../Research/VstHelper | Codebase chính/legacy | [[80-library/open-source-projects/VstHelper|VstHelper]] |
| Open5GS | ../../Research/open5gs | UPF/state reference | [[80-library/open-source-projects/Open5GS|Open5GS]] |
| free5GC | ../../Research/free5gc | 5G core reference | [[80-library/open-source-projects/free5GC|free5GC]] |
| OAI CN5G UPF VPP | ../../Research/oai-cn5g-upf-vpp | UPF/VPP reference | [[80-library/open-source-projects/OAI CN5G UPF VPP|OAI CN5G UPF VPP]] |
| FASTER | ../../Research/FASTER | High-performance KV reference | [[80-library/open-source-projects/FASTER|FASTER]] |

## Code reference block

> [!example] Copy vào code-map/component/ADR
> **Repository:** VstHelper  
> **Path:** src/...  
> **Commit:** pending  
> **Symbol:** pending  
> **Verified on:** pending

## Rules

- Không dùng line number mà không kèm commit.
- Không import toàn bộ vendor documentation vào vault.
- Mỗi upstream project chỉ có một source note chính; concept/architecture note link tới nó.
- Khi code thay đổi làm invalid note, đánh dấu **needs-review** và cập nhật **updated**.