# Docker Desktop: GitLab-এ Group/Project বানিয়ে Next.js Project Push করা

Local Docker Desktop-এ চলা GitLab instance-এ নতুন Group এবং Project বানানো, তারপর একটা Next.js project SSH দিয়ে push করা — পুরো process ধাপে ধাপে এখানে দেওয়া আছে।

---

## Step 1: GitLab-এ Group এবং Project তৈরি করা

Local GitLab dashboard-এ গিয়ে নতুন Group ও Project বানাও:

**http://localhost:8000/dashboard/home** → Click: **Groups** → Click: **New group** → Click: **Create group**

- **Group name:** গ্রুপের নাম দাও
- **Visibility level:** Public দাও
- Click: **Create group**

তারপর project বানাও:

Click: **Create Project** → Click: **Create blank project**

- **Project name:** প্রজেক্টের নাম দাও
- **Visibility Level:** Public দাও
- **Project Configuration**-এ **"Initialize repository with a README"**-এর পাশের tick sign uঠিয়ে ফেলো
- Click: **Create project**

---

## Step 2: PowerShell-এ Next.js Project Create করা

PowerShell open করে এই command গুলো run করো — একটা `gitlab` folder create হবে, সেই folder-এ ঢুকে Next.js app বানানো হবে, তারপর VS Code-এ open হবে:

```bash
mkdir gitlab
cd gitlab
npx create-next-app@latest
code .
```

---

## Step 3: Project Push করা

VS Code-এর terminal অথবা PowerShell-এ project folder-এ থেকে এই command গুলো run করো:

```bash
git init
git add .
git commit -m 'initial'
git remote add origin git@gitlab.com:wasuit-group1/wasimu.it/code-push.git
git branch -M main
git push -u origin main
```

> ⚠️ **মনে রাখবে:** এই remote URL-এ `gitlab.com` লেখা আছে, কিন্তু তুমি যদি **local Docker Desktop GitLab** (`localhost:8000`)-এ push করতে চাও, তাহলে group/project path ঠিক রেখে host অংশটা তোমার local GitLab-এর SSH config alias (যেমন আগের config file-এ সেট করা `my-gitlab-server`) দিয়ে replace করতে হবে, নাহলে push আসল gitlab.com-এ চলে যাবে। প্রজেক্টের actual clone URL local GitLab-এর project page থেকে **Code → Clone with SSH** click করে copy করে নেওয়াই safest।

---

## Step 4: Push Confirm করা

Browser reload দাও — project push হয়ে যাবে, এবং GitLab-এর project page-এ file গুলো দেখা যাবে।

---

## Quick Summary

| Step | কাজ |
|------|-----|
| 1 | Local GitLab-এ Group এবং blank Project তৈরি করা (README ছাড়া) |
| 2 | PowerShell-এ `create-next-app` দিয়ে Next.js project বানানো |
| 3 | Git init করে project-টা remote-এ push করা |
| 4 | Browser reload দিয়ে push confirm করা |
