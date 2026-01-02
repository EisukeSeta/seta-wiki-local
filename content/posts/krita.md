---
title: "Krita に Qwen-Edit-Plus-2509 をインストールする暫定方法（2026/01）"
date: 2026-01-02T01:13:22Z
draft: false
---

## Krita に Qwen-Edit-Plus-2509 をインストールする暫定方法（2026/01）

### 前提条件
- **Krita**: 5.2.14 以上  
- **Krita-ai-diffusion**: 1.44.1 以上（最新版）  
- **GPU**: NVIDIA 5060TI 相当（8GB+ VRAM）  
- ローカル ComfyUI / nunchaku サーバー: Krita 同梱の「ローカル標準サーバー」を推奨  

### 1. モデルファイルの準備と配置
```markdown
必須ファイル（nunchaku 版、safetensors）:
├── diffusion_models/
│   ├── svdq-fp4_r32-qwen-image.safetensors          (通常生成用)
│   └── svdq-fp4_r32-qwen-image-edit-2509.safetensors (編集用)
├── text_encoders/qwen-image/
│   └── qwen_2.5_vl_7b_fp8_scaled.safetensors
└── vae/qwen-image/
    └── qwen_image_vae.safetensors
```

- **ダウンロード元**: 
```markdown
Hugging Face `nunchaku-tech/` / `Comfy-Org/Qwen-Image_ComfyUI`  
```
- **配置パス例** (Windows):  
```markdown
  `C:\Users\[ユーザー名]\AppData\Roaming\krita-ai-diffusion\comfyui-nunchaku\models\...`
```
### 2. Krita-ai-diffusion 設定（安定動作構成）
```markdown
推奨プリセット構成:
ディフュージョン構成: Qwen (svdq-fp4_r32-qwen-image.safetensors)
リンクされた編集スタイル: Qwen Edit (svdq-fp4_r32-qwen-image-edit-2509.safetensors)
```

- **なぜこの構成?**  
  - 「ディフュージョン構成: Qwen Edit」単体は `list object has no attribute 'dtype'` エラー発生  
  - **Qwen + リンク:Qwen Edit** が安定動作確認済み（4step Lightning版もOK）  

### 3. インストール・確認手順
1. Krita-ai-diffusion → ローカル標準サーバー → **再インストール**  
2. モデルファイルを上記パスに配置  
3. スタイル設定で「Qwen（通常）+ Qwen Edit（編集）」をペア登録  
4. プリセット保存（例: "Qwen Edit 2509 安定版"）  
5. **低解像度/低ステップでテスト**（512x512 / 4-10 steps）  

### 4. トラブルシューティング
| 症状 | 原因・対処 |
|------|------------|
| `'list' object has no attribute 'dtype'` | ディフュージョン構成を「Qwen Edit」単体にせず、「Qwen + リンク:Qwen Edit」に変更 |
| 「Qwen Editがインストールされていません」 | 通常生成用（qwen-image.safetensors）もペアで配置・登録 |
| VRAM 不足 | fp4/int4 版使用、解像度/バッチサイズを下げる |
| 認識しない | サーバー再インストール → Krita 再起動 |

### 5. 使用時の Tips
- **Lightning 版推奨**: 4step で高速編集可能  
- **外部 ComfyUI 併用**: Plus/Multi-Image 編集が必要なら、Krita 生成 → 外部編集 → Krita 仕上げ  
- **将来性**: バージョンアップで単体「Qwen Edit」も安定化予定（現時点回避必須）  

**最終確認**: 生成（Qwen）→ 編集（Qwen Edit）で一連動作確認後運用開始。