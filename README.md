# VoServiceFrame

LSPosed module for Android SystemUI that provides selectable VoWiFi and VoLTE status-bar badge styles.

## Styles

- V1 — Square frame
- V2 — Rounded square
- V3 — Open corners
- V4 — Wi-Fi waves for VoWiFi / cellular bars for VoLTE

Selections are independent for VoWiFi and VoLTE.

## Scope

In LSPosed, scope **only System UI (`com.android.systemui`)**.

## Build with GitHub Actions

1. Create a new GitHub repository.
2. Extract this ZIP into the repository root.
3. Commit and push all files.
4. Open **Actions → Build APK → Run workflow**.
5. Download the `VoServiceFrame-release` artifact.
6. Install the APK, enable it in LSPosed, scope it to System UI, choose styles in the app, then restart SystemUI or reboot.

## Hook strategy

Rather than relying on one ROM-specific drawable name, the module hooks `ImageView.setImageResource(int)` inside SystemUI and examines the runtime resource entry name. It replaces resources whose names contain common VoWiFi / Wi-Fi calling or VoLTE / IMS LTE identifiers.

Matched VoWiFi hints:
`vowifi`, `vo_wifi`, `wifi_calling`, `wificalling`, `wfc`, `ims_wifi`

Matched VoLTE hints:
`volte`, `vo_lte`, `ims_lte`, `hd_voice`, `hdvoice`

Every successful replacement is logged with the `VoServiceFrame` tag in LSPosed logs. If Infinity-X / Vector uses a different resource name, the log output can be used to add it to the candidate list.


## v1.0.1 workflow fix
GitHub Actions now uses `android-actions/setup-android@v4` with `packages: ""` so the obsolete SDK package `tools` is not requested. Required SDK components are installed explicitly.
