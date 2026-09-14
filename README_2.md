cd E:\TienIch\Quet_Ma_Doc\Cyrenix

# Bump 0.1.0 -> 0.2.0 Ở 3 FILE
(Get-Content src-tauri\tauri.conf.json -Raw) -replace '"version":\s*"0\.1\.0"','"version": "0.2.0"' | Set-Content src-tauri\tauri.conf.json -NoNewline
(Get-Content package.json -Raw) -replace '"version":\s*"0\.1\.0"','"version": "0.2.0"' | Set-Content package.json -NoNewline
(Get-Content src-tauri\Cargo.toml -Raw) -replace '(?m)^version = "0\.1\.0"','version = "0.2.0"' | Set-Content src-tauri\Cargo.toml -NoNewline

# Kiem tra
Select-String -Path src-tauri\tauri.conf.json,package.json -Pattern '"version"'
Select-String -Path src-tauri\Cargo.toml -Pattern '^version'

git add src-tauri/tauri.conf.json package.json src-tauri/Cargo.toml
git commit -m "release: v0.2.0"

# Push code TRUOC (gồm release.yml mới)
git push origin master

# Tag kích hoạt workflow
git tag v0.2.0
git push origin v0.2.0
