# R36S "V20" board — Sitronix ST7703 panel

This folder adds a working device tree for the newer **R36S V20** board, whose display is a
**Sitronix ST7703** MIPI-DSI panel. None of the existing MultiPanel presets (Panel 0–5, all
`elida,kd35t133`) drive this screen — they produce a **black screen with a blinking red LED**.

This is the same panel reported in
[ArkOS-R3XS issue #293](https://github.com/AeolusUX/ArkOS-R3XS/issues/293), which was closed
unresolved, and it is not recognised by the DTB Identify tool.

## Panel identification (from the stock dtb)

- `compatible = "sitronix,st7703"`
- MIPI-DSI panel (`route-dsi`, `rockchip,px30-mipi-dsi`, `dsi@ff450000/panel@0`)
- Stock firmware: ArkOS-based, boots via `extlinux`, dtb filename `rf3536k3ka.dtb`

## File

**`rf3536k3ka.dtb`** — the known-good device tree extracted from the stock BOOT partition of a
V20 unit. It correctly drives the ST7703 panel.

> **Note:** this is a full board dtb built against the **stock (older) kernel**. Dropping it onto
> a current ArkOS-R3XS card (renamed to `rk3326-r35s-linux.dtb`) makes the OS fail to boot,
> because the board/kernel ABI differs — so it is **not** a drop-in fix for the current image.
> It is contributed here to document the correct **ST7703 panel bindings and init sequence** so
> that proper support can be rebuilt against the current kernel.

## Symptoms on affected units

- Boots the stock card fine; screen works.
- Any `elida` panel preset (Panel 0–5, or the stock full-board dtb on a new kernel) → black
  screen + blinking red LED.
