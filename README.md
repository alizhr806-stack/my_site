<!doctype html>
<html lang="fa" dir="rtl">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>گرایش شما چیست؟</title>
  <style>
    :root {
      --bg1: #0f172a; --bg2: #0b1220; --card: #0b1226;
      --accent1: #7c3aed; --accent2: #06b6d4; --glass: rgba(255,255,255,0.06);
      --text: #e6eef8;
    }
    * { box-sizing: border-box; font-family: 'Segoe UI', Tahoma, sans-serif }
    html, body { height: 100%; margin: 0 }
    body {
      background: radial-gradient(1200px 600px at 10% 20%, rgba(124,58,237,0.12), transparent),
                  radial-gradient(1000px 500px at 90% 80%, rgba(6,182,212,0.08), transparent),
                  linear-gradient(180deg, var(--bg1), var(--bg2));
      color: var(--text); display: flex; align-items: center; justify-content: center; padding: 32px;
    }
    .card {
      width: 100%; max-width: 760px; background: linear-gradient(180deg, rgba(255,255,255,0.03), rgba(255,255,255,0.01));
      border-radius: 16px; padding: 28px; box-shadow: 0 10px 30px rgba(2,6,23,0.65); backdrop-filter: blur(6px);
      border: 1px solid rgba(255,255,255,0.04);
    }
    h2 { margin: 0 0 18px; font-size: 26px; letter-spacing: 0.2px }
    p.lead { margin: 0 0 22px; color: rgba(230,238,248,0.8) }

    .playground {
      display: flex; gap: 20px; justify-content: center; margin-bottom: 20px;
    }

    .btn {
      appearance: none; border: 0; padding: 12px 18px; border-radius: 12px; font-weight: 600; cursor: pointer;
      box-shadow: 0 6px 18px rgba(2,6,23,0.5); transition: transform .18s, box-shadow .18s;
      background: linear-gradient(90deg, var(--accent1), var(--accent2)); color: white; min-width: 110px; text-align: center;
    }
    .btn:active { transform: scale(0.95) }

    #btnYes { background: linear-gradient(90deg, #10b981, #34d399); }
    #btnNo { background: linear-gradient(90deg, #ef4444, #f97316); }

    .modal {
      position: fixed; inset: 0; display: flex; align-items: center; justify-content: center; visibility: hidden; opacity: 0;
      transition: opacity .18s, visibility .18s;
    }
    .modal.open { visibility: visible; opacity: 1 }
    .modal-backdrop {
      position: absolute; inset: 0; background: rgba(0,0,0,0.5); backdrop-filter: blur(6px);
    }
    .modal-card {
      position: relative; z-index: 2; background: var(--card); padding: 22px; border-radius: 12px;
      min-width: 320px; max-width: 420px; border: 1px solid rgba(255,255,255,0.03);
    }
    label { display: block; margin-bottom: 6px; font-size: 13px; color: rgba(230,238,248,0.9) }
    input[type=text], input[type=email] {
      width: 100%; padding: 10px 12px; border-radius: 8px; border: 1px solid rgba(255,255,255,0.06);
      background: var(--glass); color: var(--text); outline: none;
    }

    .success {
      margin-top: 18px; padding: 14px; border-radius: 10px;
      background: linear-gradient(90deg, rgba(16,185,129,0.12), rgba(124,58,237,0.06));
      color: var(--text); font-weight: 700; border: 1px solid rgba(255,255,255,0.03);
    }

    @media (max-width: 480px) {
      .btn { min-width: 100px; padding: 10px 14px; font-size: 15px; }
    }
  </style>
</head>
<body>
  <div class="card">
    <h2>گرایش جنسی شما چیست؟</h2>
    <p class="lead">لطفاً یکی از گزینه‌ها را انتخاب کنید</p>

    <div class="playground">
      <button id="btnYes" class="btn">همجنسگرا</button>
      <button id="btnNo" class="btn">دگرجنسگرا</button>
    </div>

    <div id="messageArea"></div>
  </div>

  <!-- modal -->
  <div class="modal" id="modal">
    <div class="modal-backdrop"></div>
    <div class="modal-card">
      <h3>اختیاری: اطلاعات تماس</h3>
      <form id="infoForm">
        <label for="name">نام شما</label>
        <input id="name" name="name" type="text" placeholder="مثلاً: محسن" />
        <label for="email">ایمیل</label>
        <input id="email" name="email" type="email" placeholder="مثلاً: you@example.com" />
        <div style="display:flex;gap:10px;justify-content:flex-end;margin-top:14px">
          <button type="button" id="closeModal" class="btn" style="background:linear-gradient(90deg,#6b7280,#9ca3af)">انصراف</button>
          <button type="submit" class="btn">ارسال</button>
        </div>
      </form>
    </div>
  </div>

  <script>
    const btnYes = document.getElementById('btnYes');
    const btnNo = document.getElementById('btnNo');
    const modal = document.getElementById('modal');
    const infoForm = document.getElementById('infoForm');
    const messageArea = document.getElementById('messageArea');

    btnYes.addEventListener('click', () => {
      modal.classList.add('open');
      document.getElementById('name').focus();
    });

    btnNo.addEventListener('click', () => {
      messageArea.innerHTML = '<div class="success">✅ شما گزینه "دگرجنسگرا" را انتخاب کردید.</div>';
    });

    document.getElementById('closeModal').addEventListener('click', () => modal.classList.remove('open'));
    modal.addEventListener('click', e => { if (e.target === modal) modal.classList.remove('open'); });

    infoForm.addEventListener('submit', e => {
      e.preventDefault();
      const name = document.getElementById('name').value.trim();
      const email = document.getElementById('email').value.trim();
      modal.classList.remove('open');
      messageArea.innerHTML = `<div class="success">🎉 ممنون ${name || 'دوست عزیز'}! اطلاعات شما ثبت شد.<br><span style="opacity:.8">ایمیل: ${email || 'ثبت نشده'}</span></div>`;
    });
  </script>
</body>
</html>
