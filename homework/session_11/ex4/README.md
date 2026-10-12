# Bài 4 — GitHub Secrets và đăng nhập Container Registry (GHCR)

## 1. Tạo Personal Access Token (classic)

1. GitHub → avatar → **Settings** → **Developer settings** → **Personal access tokens** → **Tokens (classic)**.
2. **Generate new token (classic)**.
3. Bật quyền **`write:packages`** (và `read:packages` nếu có).
4. Generate → **copy token** (chỉ hiện 1 lần).

## 2. Tạo Repository Secret

1. Vào repo này → **Settings** → **Secrets and variables** → **Actions**.
2. **New repository secret**.
3. Name: **`REGISTRY_TOKEN`**
4. Value: dán token vừa tạo → **Add secret**.
5. Chụp màn hình danh sách Secrets (thấy tên `REGISTRY_TOKEN`, không lộ value).

## 3. Bước trong `ci.yml`

```yaml
- name: Đăng nhập vào GitHub Container Registry
  uses: docker/login-action@v3
  with:
    registry: ghcr.io
    username: ${{ github.actor }}
    password: ${{ secrets.REGISTRY_TOKEN }}
```

## 4. Kiểm tra

1. Push / re-run workflow trên tab **Actions**.
2. Mở log bước **Đăng nhập vào GitHub Container Registry**.
3. Phải thấy **Login Succeeded**.

## Nộp bài

- File `.github/workflows/ci.yml` (có `docker/login-action@v3`)
- Ảnh Settings → Secrets: có `REGISTRY_TOKEN`
- (Tuỳ chọn) Ảnh log Actions: Login Succeeded
