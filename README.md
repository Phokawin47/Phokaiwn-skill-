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

MIT — ดู [LICENSE](LICENSE)
