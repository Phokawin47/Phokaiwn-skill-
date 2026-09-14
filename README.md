# Phokawin Skills

คลัง **Agent Skills** สำหรับ AI coding agents (Claude Code, Cursor, Codex, Antigravity) ตามมาตรฐาน [skills.sh](https://skills.sh)

แนวคิดของคลังนี้: สกิลที่ดีไม่ใช่สกิลที่สอนสิ่งที่โมเดลรู้อยู่แล้ว แต่คือสกิลที่ **บังคับวินัย** — มีจุดหยุดให้คนตัดสินใจ มีเกณฑ์ผ่าน/ไม่ผ่านที่เขียนไว้ล่วงหน้า และห้ามอ้างผลลัพธ์ที่ยังไม่ได้วัด

---

## Quick Start

ติดตั้งลงโปรเจกต์ปัจจุบัน:

```bash
npx skills add Phokawin47/Phokawin-skills --all
```

ติดตั้งแบบ global (ใช้ได้ทุกโปรเจกต์):

```bash
npx skills add Phokawin47/Phokawin-skills -g
```

ดูรายชื่อสกิลก่อนติดตั้ง:

```bash
npx skills add Phokawin47/Phokawin-skills --list
```

ติดตั้งเฉพาะบางตัว:

```bash
npx skills add Phokawin47/Phokawin-skills refactor
```

### ติดตั้งแบบ manual (ไม่ใช้ npx)

```bash
git clone https://github.com/Phokawin47/Phokawin-skills.git
mkdir -p ~/.claude/skills
cp -r Phokawin-skills/skills/*/* ~/.claude/skills/
```

หรือใช้เฉพาะในโปรเจกต์เดียว เปลี่ยนปลายทางเป็น `<project>/.claude/skills/`

ตรวจว่า Claude Code เห็นสกิลแล้ว: เปิด Claude Code แล้วพิมพ์ `/skills`

---

## Catalog

### `skills/engineering/`

- **[`refactor`](skills/engineering/refactor/SKILL.md)** — ปรับโครงสร้างโค้ดโดยไม่เปลี่ยนพฤติกรรม จุดเด่นคือ **Gate 0**: ต้องหา test/type/lint command ของโปรเจกต์จริง เช็กว่าโค้ดเป้าหมายมีเทสต์คุมจริงไหม และรัน baseline เก็บผลก่อนแตะโค้ด ถ้าไม่มีเทสต์หรือ baseline แดง → หยุดและเสนอทางเลือก มีเพดานขอบเขต 5 ไฟล์ / 400 บรรทัดต่อรอบ, commit ทีละ refactoring, ห้าม `git add -A`, และเทสต์แดงหลังแก้ = revert ไม่ใช่แก้จนเขียว
- **[`git-commit`](skills/engineering/git-commit/SKILL.md)** — วิเคราะห์ diff จริง จัดกลุ่มไฟล์ที่ stage และเขียนข้อความ Conventional Commit
- **[`spec-to-tasks`](skills/engineering/spec-to-tasks/SKILL.md)** — สรุปบทสนทนาเป็น Technical Spec แล้วแตกเป็น checklist งานแบบ tracer-bullet พร้อมลำดับก่อนหลัง (user เรียกเอง)
- **[`post-mortem`](skills/engineering/post-mortem/SKILL.md)** — บันทึก root cause, กลไกของบั๊ก, การยืนยัน และการป้องกัน ลง `docs/post-mortems/<date>-<slug>.md`
- **[`karpathy-guidelines`](skills/engineering/karpathy-guidelines/SKILL.md)** — Think before coding, Simplicity first, Surgical changes, Goal-driven execution
- **[`scrutinize`](skills/engineering/scrutinize/SKILL.md)** — รีวิว plan / PR / diff จากมุมมองคนนอก ตั้งคำถามว่ามีวิธีง่ายกว่านี้ไหม และไล่ code path จริงไม่ใช่ดูแค่ diff
- **[`debug-mantra`](skills/engineering/debug-mantra/SKILL.md)** — วินัยดีบัก 4 ขั้น: reproduce, หา fail path, หักล้างสมมติฐาน, บันทึกทุกการทดลอง

### `skills/productivity/`

- **[`caveman`](skills/productivity/caveman/SKILL.md)** — โหมดตอบสั้นขั้นสุด ตัดคำฟุ่มเฟือยแต่คงความถูกต้องทางเทคนิค ประหยัด token
- **[`find-skills`](skills/productivity/find-skills/SKILL.md)** — ค้นหาและติดตั้งสกิลจาก [skills.sh](https://skills.sh)
- **[`grill-me`](skills/productivity/grill-me/SKILL.md)** — สัมภาษณ์เค้นความคิดแบบ Socratic จบในแชต ไม่สร้างไฟล์ (user เรียกเอง)
- **[`grill-with-docs`](skills/productivity/grill-with-docs/SKILL.md)** — สัมภาษณ์เค้น requirement สำหรับโปรเจกต์จริง บันทึกลง `CONTEXT.md` และ `docs/adr/` (user เรียกเอง)
- **[`handoff`](skills/productivity/handoff/SKILL.md)** — สรุปสถานะงานลง OS temp directory เพื่อส่งต่อให้เซสชันถัดไป ตัด secrets ทิ้ง (user เรียกเอง)

สกิลทั้งหมดยกเว้น `refactor` คัดลอกมาจาก [Rachapol03/Rachapol-skills](https://github.com/Rachapol03/Rachapol-skills) โดยไม่แก้ไข ดูแหล่งต้นทางและ copyright ได้ที่ [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md)

---

## เพิ่มสกิลใหม่

1. สร้างโฟลเดอร์ `skills/<category>/<skill-name>/SKILL.md`
2. ใส่ YAML frontmatter — `description` คือกลไกเดียวที่ทำให้ agent เรียกสกิลถูกจังหวะ เขียนให้ครอบคลุมทั้ง "ทำอะไร" และ "เมื่อไหร่ควรใช้" รวมถึงสำนวนที่ผู้ใช้พูดจริงโดยไม่เอ่ยชื่อสกิล

```yaml
---
name: your-skill-name
description: สรุปว่าทำอะไร + เมื่อไหร่ควร trigger ใส่คีย์เวิร์ดสำคัญไว้ต้นประโยค
disable-model-invocation: true   # ใส่เฉพาะสกิลที่ต้องการให้ user เรียกเองเท่านั้น
---
```

3. ทดสอบว่าถูกตรวจเจอ: `npx skills add ./ --list`
4. ทดสอบ trigger จริง — สั่งงานด้วยประโยคแบบคนใช้จริง (ไม่เอ่ยชื่อสกิล) แล้วดูว่า agent หยิบสกิลขึ้นมาไหม ถ้าไม่หยิบ แปลว่า `description` ยังไม่พอ ไม่ใช่เนื้อหาในสกิลผิด
5. commit ทีละไฟล์ แล้วเปิด PR

---

## License

MIT — ดู [LICENSE](LICENSE) และ [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md) สำหรับสกิลจากแหล่งอื่น
