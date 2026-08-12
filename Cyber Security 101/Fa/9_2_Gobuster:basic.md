# Gobuster — راهنمای کاربردی

Gobuster یک ابزار متن‌باز امنیتی نوشته‌شده با Go است که برای **Enumeration** و شناسایی منابع در تست نفوذ استفاده می‌شود.

مهم‌ترین کاربردهای Gobuster:

- پیدا کردن Directory و Fileهای وب‌سایت
- پیدا کردن Subdomainها
- پیدا کردن Virtual Hostها (VHost)
- بررسی AWS S3 Bucket
- بررسی Google Cloud Storage

---

## فهرست مطالب

- [مفاهیم پایه](#مفاهیم-پایه)
- [تنظیم DNS در TryHackMe](#تنظیم-dns-در-tryhackme)
- [ساختار کلی Gobuster](#ساختار-کلی-gobuster)
- [Directory Enumeration — dir](#directory-enumeration--dir)
- [Subdomain Enumeration — dns](#subdomain-enumeration--dns)
- [Virtual Host Enumeration — vhost](#virtual-host-enumeration--vhost)
- [تفاوت dns و vhost](#تفاوت-dns-و-vhost)
- [Cheat Sheet](#cheat-sheet)

---

## مفاهیم پایه

### Enumeration

Enumeration یعنی **شناسایی و فهرست کردن منابع موجود** در یک هدف.

مثلاً:

```text
Website
├── /admin
├── /login
├── /images
└── /backup
