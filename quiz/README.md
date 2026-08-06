# Practice Quiz Engine — Known Caveats and Operating Notes
July 8, 2026. READ BEFORE SEMESTER START. These are accepted limitations (Gilley ruling, July 8: "keep it as is"), recorded so they are not rediscovered the hard way in week 2.

## Caveats (accepted by design)

1. **The identity gate is a deterrent, not a wall.** This is a static GitHub Pages site: a student who reads the page source can bypass the roster check or forge a completion page. The real integrity layer is unchanged by design: the completion PDF goes through the good-faith auto-flag, and the Skill Check firewall catches anyone who faked their practice. Do not escalate this into surveillance; that tradeoff was already ruled on (June 12 design notes).

2. **Progress is saved per browser, per identity.** A student who practices on their phone and then opens the quiz on a laptop starts their streaks fresh (their phone progress is still on the phone). Expect a few emails about "lost progress" in week 2 — the answer is "finish on the device you started on, or just re-master; it is practice." A cross-device fix would require a server, which contradicts the static-site design.

3. **Roster timing matters.** The roster locks out anyone not on it. Build and upload `roster.json` only AFTER the add/drop deadline (August 30). Any late add must trigger a roster rebuild the same day, or that student cannot practice. Until a roster is uploaded, the quiz runs in open-access mode — that is the correct state for weeks 1–3.

4. **Rebuilding the roster regenerates the salt.** Every rebuild produces a completely new `roster.json` — always upload the freshest file, never merge old and new. The tool shuffles hash order so the file does not mirror your roster order.

5. **Privacy boundary.** `roster-tool.html` must NEVER be committed with student data in it, and no plaintext class list ever goes in the repository. Only the hashed `roster.json` is public. Verify once after first push: open the repository in a browser and confirm no file contains a readable student name or ID.

6. **Verification codes are honesty markers, not cryptographic proof.** The code on the completion page deters casual copying between students (identity is baked in), but a determined student could compute one. Same answer as caveat 1: the Skill Check is the firewall.

## Pre-semester checklist for this folder
- [ ] Push `GitHub Pages Upload` to the repository
- [ ] Click through the quiz once in a real browser (dummy bank loads by default)
- [ ] Scan one newly generated QR code from a printed page (for example section 9-3)
- [ ] After August 30: build `roster.json` locally with `roster-tool.html`, upload to `quiz/banks/`, then test one real student identity and one wrong section number (should be rejected)
- [ ] Confirm the repository contains no plaintext student data
- [ ] When the Objective 1 item bank is ruled and built: drop it at `quiz/banks/objective1.json` and link students to `quiz/?bank=objective1`
