# Colab Training (Token Flow)

This folder contains the Google Colab notebook for VisoLabel cloud training handoff.

## Flow

1. VisoLabel packages `training_bundle.json` and `dataset/`.
2. The app encrypts the zip with AES-256-GCM and uploads only the encrypted bundle.
3. The notebook resolves the token through `/api/v1/colab/resolve-token/`, downloads the bundle, decrypts it locally in Colab, validates the dataset, trains, and uploads artifacts with `/api/v1/colab/request-checkpoint-upload/`.

New encrypted tokens use `VL1.<base64url-json-array>` with `[server_token, password, metadata]` or `[server_token, password, api_url, metadata]`.

## Notebook

Run `VisoLabel_Train_From_Token.ipynb` in a GPU Colab runtime. The form cell provides:

- Token input and optional API URL override.
- Bundle preview and dataset validation logs.
- RF-DETR training with current Lightning behavior, visible progress, compatible resolution adjustment, and a high-level fallback.
- Classification training for image-folder bundles.
- Checkpoint/log upload back to VisoLabel.

Treat the token as a secret because it can resolve and decrypt the bundle until expiry.
