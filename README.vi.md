# Skill vẽ sequence diagram AURA cho Codex

Tiếng Việt | [English](README.md)

Repo này chứa skill giúp Codex tạo và rà soát sequence diagram use case theo quy ước của dự án AURA Shore Store. Bộ quy tắc đi kèm có phiên bản 3.1.0. Đây là quy ước của dự án, không phải yêu cầu chung của UML.

## Trước khi cài

1. Nhờ chủ repo cấp quyền truy cập. Repo này **riêng tư**; GitHub có thể báo 404 nếu tài khoản của bạn chưa được cấp quyền.
2. Cài Git và đăng nhập GitHub khi Git yêu cầu. Các lệnh bên dưới tải repo rồi chỉ sao chép thư mục skill vào vùng skill cá nhân của Codex. Nếu đã cài skill, lệnh sẽ dừng để không ghi đè bản đang dùng.

## Cài trên Windows (PowerShell)

Mở PowerShell, copy **toàn bộ** khối lệnh sau và nhấn Enter:

```powershell
$repoDir = Join-Path $env:TEMP ('aura-sequence-diagrams-codex-' + [guid]::NewGuid().ToString('N'))
$skillDir = Join-Path $HOME '.agents\skills\aura-sequence-diagrams'
if (Test-Path -LiteralPath $skillDir) { throw "Skill already exists at $skillDir" }
git clone --depth 1 https://github.com/NoNameVI/aura-sequence-diagrams-codex.git $repoDir
if ($LASTEXITCODE -ne 0) { throw 'Git clone failed. Check repository access and GitHub sign-in.' }
New-Item -ItemType Directory -Force -Path (Split-Path -Parent $skillDir) | Out-Null
Copy-Item -LiteralPath (Join-Path $repoDir 'skills\aura-sequence-diagrams') -Destination $skillDir -Recurse
if (-not (Test-Path -LiteralPath (Join-Path $skillDir 'SKILL.md'))) { throw 'Installation check failed.' }
Write-Host "Installed: $skillDir"
```

## Cài trên macOS hoặc Linux (Terminal)

Mở Terminal, copy **toàn bộ** khối lệnh sau và nhấn Enter:

```bash
(
  set -eu
  repo_dir=$(mktemp -d)
  skill_dir="$HOME/.agents/skills/aura-sequence-diagrams"
  if [ -e "$skill_dir" ]; then echo "Skill already exists at $skill_dir" >&2; exit 1; fi
  git clone --depth 1 https://github.com/NoNameVI/aura-sequence-diagrams-codex.git "$repo_dir/repo"
  mkdir -p "$HOME/.agents/skills"
  cp -R "$repo_dir/repo/skills/aura-sequence-diagrams" "$skill_dir"
  test -f "$skill_dir/SKILL.md"
  printf 'Installed: %s\n' "$skill_dir"
)
```

Trong lúc tải repo, Git có thể mở cửa sổ đăng nhập GitHub. Nếu báo 404 hoặc không có quyền, hãy kiểm tra tài khoản GitHub mà Git đang dùng đã được chủ repo cấp quyền chưa.

## Kiểm tra và sử dụng

Mở **chat Codex mới** rồi gửi yêu cầu mẫu:

```text
Hãy dùng $aura-sequence-diagrams để rà soát sequence diagram use case này theo quy tắc AURA.
```

Để làm việc với ứng dụng AURA thật, bạn còn cần workspace AURA, `AGENTS.md`, code hiện tại, `AURA_Backlog.xlsx` để xác định actor, tài liệu UC và các script build theo release. Với dự án khác, hãy cung cấp code hoặc mô tả UC và yêu cầu rõ kiểu trình bày AURA. Skill chỉ dùng đường dẫn và định dạng riêng của AURA khi chúng có sẵn.

Chủ repo chỉ đăng thay đổi khi có yêu cầu cập nhật rõ ràng. Cài skill không bật đồng bộ GitHub tự động.
