<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>منصة مذاكرة - Mozakra Platform</title>
    <link href="https://fonts.googleapis.com/css2?family=Tajawal:wght@400;500;700;900&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary: #2563eb;
            --primary-dark: #1e40af;
            --bg-color: #f8fafc;
            --card-bg: #ffffff;
            --text-main: #1e293b;
            --text-secondary: #64748b;
            --border: #e2e8f0;
            --danger: #ef4444;
            --success: #22c55e;
        }
        body {
            font-family: 'Tajawal', sans-serif;
            background-color: var(--bg-color);
            color: var(--text-main);
            margin: 0;
            padding: 0;
        }
        .container {
            max-width: 900px;
            margin: 20px auto;
            background: var(--card-bg);
            padding: 25px;
            border-radius: 16px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.05);
        }
        h1, h2, h3 { color: var(--primary-dark); }
        button, .btn {
            background: var(--primary);
            color: white;
            border: none;
            padding: 10px 18px;
            border-radius: 8px;
            cursor: pointer;
            font-family: 'Tajawal';
            font-weight: 700;
            transition: 0.2s;
        }
        button:hover { background: var(--primary-dark); }
        input, select, textarea {
            width: 100%;
            padding: 10px;
            margin: 8px 0;
            border: 1px solid var(--border);
            border-radius: 8px;
            font-family: 'Tajawal';
            box-sizing: border-box;
        }
        .nav-tabs {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
            border-bottom: 2px solid var(--border);
            padding-bottom: 10px;
            flex-wrap: wrap;
        }
        .tab-btn {
            background: #e2e8f0;
            color: var(--text-main);
            padding: 8px 14px;
            border-radius: 6px;
            cursor: pointer;
            border: none;
            font-weight: 600;
        }
        .tab-btn.active {
            background: var(--primary);
            color: white;
        }
        .card {
            background: #f1f5f9;
            padding: 15px;
            border-radius: 10px;
            margin-bottom: 12px;
            border-right: 4px solid var(--primary);
        }
        .flex-row { display: flex; gap: 10px; align-items: center; }
        .badge { background: #dbeafe; color: var(--primary-dark); padding: 3px 8px; border-radius: 4px; font-size: 12px; }
        .danger-btn { background: var(--danger); }
        .success-btn { background: var(--success); }
    </style>
</head>
<body>

    <div class="container">
        <h1>🎓 منصة مذاكرة التعليمية</h1>
        <p>نظام إداري متكامل لإدارة الطلاب، المجتمعات الخاصة بكل معلم، الدعم الفني، والإعلانات المتقدمة.</p>

        <!-- شريط التنقل والأقسام -->
        <div class="nav-tabs">
            <button class="tab-btn active" onclick="switchTab('home')">الرئيسية</button>
            <button class="tab-btn" onclick="switchTab('communities')">مجتمعات المعلمين</button>
            <button class="tab-btn" onclick="switchTab('announcements')">الإعلانات والمرفقات</button>
            <button class="tab-btn" onclick="switchTab('support')">الدعم الفني والتذاكر</button>
            <button class="tab-btn" onclick="switchTab('admin')">لوحة تحكم المعلم (Admin)</button>
        </div>

        <!-- قسم الرئيسية -->
        <div id="home" class="tab-content">
            <h2>مرحباً بك في منصة مذاكرة</h2>
            <p>اختر القسم المناسب من الأعلى لتصفح مجتمع معلمك، متابعة الإعلانات، أو فتح تذكرة دعم فني جديدة مع اختيار المدرس المختص.</p>
        </div>

        <!-- قسم مجتمعات المعلمين -->
        <div id="communities" class="tab-content" style="display:none;">
            <h2>مجتمعات المعلمين (لكل معلم وطلابه)</h2>
            <label>اختر المعلم لعرض مجتمعه:</label>
            <select id="selectedTeacherCommunity" onchange="loadTeacherCommunity()">
                <option value="مستر أحمد">مستر أحمد (مادة الرياضيات)</option>
                <option value="مستر إبراهيم">مستر إبراهيم (مادة الفيزياء)</option>
                <option value="مستر محمد">مستر محمد (مادة البرمجة)</option>
            </select>
            <div id="communityChatContainer" style="margin-top: 15px;">
                <div id="communityMessages" style="max-height: 250px; overflow-y: auto; background: #f8fafc; padding: 10px; border-radius: 8px; border: 1px solid var(--border);"></div>
                <input type="text" id="communityMsgInput" placeholder="اكتب رسالتك لطلاب ومستر هذا المجتمع...">
                <button onclick="sendCommunityMessage()">إرسال للمجتمع</button>
            </div>
        </div>

        <!-- قسم الإعلانات والمرفقات -->
        <div id="announcements" class="tab-content" style="display:none;">
            <h2>لوحة الإعلانات الرسمية</h2>
            <div id="announcementsList"></div>
        </div>

        <!-- قسم الدعم الفني والتذاكر المتقدمة -->
        <div id="support" class="tab-content" style="display:none;">
            <h2>الدعم الفني ومساعدة الطلاب</h2>
            <div class="card">
                <h3>فتح تذكرة جديدة</h3>
                <input type="text" id="studentNameTicket" placeholder="اسمك الكامل">
                <label>اختر المدرس المطلوب:</label>
                <select id="targetTeacherTicket">
                    <option value="مستر أحمد">مستر أحمد</option>
                    <option value="مستر إبراهيم">مستر إبراهيم</option>
                    <option value="مستر محمد">مستر محمد</option>
                </select>
                <textarea id="ticketProblemDesc" placeholder="اشرح مشكلتك بالتفصيل..."></textarea>
                <button onclick="createTicket()">إرسال التذكرة للمدرس</button>
            </div>
            <h3>التذاكر النشطة والمغلقة</h3>
            <div id="ticketsList"></div>
        </div>

        <!-- قسم لوحة تحكم المعلم (بكلمة مرور وحماية) -->
        <div id="admin" class="tab-content" style="display:none;">
            <div id="adminLoginBox">
                <h2>تسجيل دخول المعلمين (Admin)</h2>
                <p>هذا القسم مخصص للمدرسين فقط. يرجى إدخال كلمة المرور للمتابعة:</p>
                <input type="password" id="adminPasswordInput" placeholder="كلمة المرور السرية">
                <button onclick="verifyAdminLogin()">دخول لوحة التحكم</button>
            </div>

            <div id="adminDashboardContent" style="display:none;">
                <h2>لوحة تحكم المعلم الشاملة ⚙️</h2>
                
                <!-- إضافة إعلان مع مرفق ملف أو صورة -->
                <div class="card">
                    <h3>نشر إعلان جديد (مع مرفق صور أو ملفات)</h3>
                    <input type="text" id="annTitle" placeholder="عنوان الإعلان">
                    <textarea id="annDesc" placeholder="تفاصيل الإعلان..."></textarea>
                    <label>إرفاق صورة أو ملف:</label>
                    <input type="file" id="annFile">
                    <button onclick="postAnnouncement()">نشر الإعلان</button>
                </div>

                <!-- بحث وتحديد عدة حسابات طلاب دفعة واحدة -->
                <div class="card">
                    <h3>بحث وتحديد حسابات الطلاب دفعة واحدة</h3>
                    <input type="text" id="studentSearchQuery" placeholder="ابحث باسم الطالب أو الكود..." oninput="filterStudentsSearch()">
                    <div id="studentsMultiSelectContainer" style="max-height: 150px; overflow-y: auto; background: white; padding: 8px; border-radius: 6px; margin-top: 5px;">
                        <!-- يتم تعبئتها برمجياً -->
                    </div>
                    <p style="font-size: 13px; color: var(--text-secondary); margin-top: 5px;">تم تحديد الطلاب للعمليات الجماعية.</p>
                </div>
            </div>
        </div>

    </div>

    <script>
        // قواعد البيانات الوهمية والتخزين المحلي
        let announcements = JSON.parse(localStorage.getItem('mozakra_anns')) || [
            { id: 1, title: 'موعد امتحان الفيزياء', desc: 'تم تحديد موعد الامتحان القادم يوم الخميس القادم.', file: '', author: 'مستر إبراهيم' }
        ];
        
        let tickets = JSON.parse(localStorage.getItem('mozakra_tickets')) || [];
        let communityMsgs = JSON.parse(localStorage.getItem('mozakra_comm_msgs')) || {};
        
        let studentsDatabase = [
            { id: 101, name: 'محمد عنتر', group: 'مجموعة أ - أولى ثانوي' },
            { id: 102, name: 'أحمد محمود', group: 'مجموعة ب - أولى ثانوي' },
            { id: 103, name: 'محمود خالد', group: 'مجموعة أ - أولى ثانوي' },
            { id: 104, name: 'يوسف إبراهيم', group: 'مجموعة ج - أولى ثانوي' }
        ];

        function switchTab(tabId) {
            document.querySelectorAll('.tab-content').forEach(el => el.style.display = 'none');
            document.querySelectorAll('.tab-btn').forEach(el => el.classList.remove('active'));
            document.getElementById(tabId).style.display = 'block';
            event.target.classList.add('active');
            
            if(tabId === 'announcements') renderAnnouncements();
            if(tabId === 'support') renderTickets();
            if(tabId === 'communities') loadTeacherCommunity();
            if(tabId === 'admin') initStudentsSearchUI();
        }

        // حماية لوحة تحكم المعلم بكلمة مرور
        function verifyAdminLogin() {
            const pass = document.getElementById('adminPasswordInput').value;
            // كلمة المرور الافتراضية للمدرسين (يمكنك تغييرها)
            if(pass === 'teacher123') {
                document.getElementById('adminLoginBox').style.display = 'none';
                document.getElementById('adminDashboardContent').style.display = 'block';
                alert('مرحباً بك يا مستر! تم تسجيل الدخول بنجاح.');
            } else {
                alert('كلمة المرور غير صحيحة! هذا القسم مخصص للمعلمين فقط.');
            }
        }

        // نظام المجتمعات لكل معلم
        function loadTeacherCommunity() {
            const teacher = document.getElementById('selectedTeacherCommunity').value;
            const container = document.getElementById('communityMessages');
            container.innerHTML = '';
            
            let msgs = communityMsgs[teacher] || [];
            if(msgs.length === 0) {
                container.innerHTML = `<p style="color:var(--text-secondary); text-align:center;">لا توجد رسائل في مجتمع ${teacher} بعد.</p>`;
                return;
            }
            msgs.forEach((m, index) => {
                container.innerHTML += `<div style="background:white; padding:8px; margin:5px 0; border-radius:6px; border:1px solid var(--border);">
                    <b>${m.sender}:</b> ${m.text}
                </div>`;
            });
        }

        function sendCommunityMessage() {
            const teacher = document.getElementById('selectedTeacherCommunity').value;
            const text = document.getElementById('communityMsgInput').value;
            if(!text.trim()) return;

            if(!communityMsgs[teacher]) communityMsgs[teacher] = [];
            communityMsgs[teacher].push({ sender: 'طالب/مستر', text: text });
            localStorage.setItem('mozakra_comm_msgs', JSON.stringify(communityMsgs));
            
            document.getElementById('communityMsgInput').value = '';
            loadTeacherCommunity();
        }

        // الإعلانات مع مرفقات (صور/ملفات) وإمكانية التعديل والمسح للمستخدمين/الأدمن
        function postAnnouncement() {
            const title = document.getElementById('annTitle').value;
            const desc = document.getElementById('annDesc').value;
            const fileInput = document.getElementById('annFile');
            let fileName = fileInput.files.length > 0 ? fileInput.files[0].name : '';

            if(!title || !desc) {
                alert('يرجى كتابة العنوان وتفاصيل الإعلان!');
                return;
            }

            announcements.push({ id: Date.now(), title, desc, file: fileName, author: 'المعلم المسؤول' });
            localStorage.setItem('mozakra_anns', JSON.stringify(announcements));
            
            document.getElementById('annTitle').value = '';
            document.getElementById('annDesc').value = '';
            document.getElementById('annFile').value = '';
            alert('تم نشر الإعلان بنجاح!');
            renderAnnouncements();
        }

        function renderAnnouncements() {
            const list = document.getElementById('announcementsList');
            list.innerHTML = '';
            if(announcements.length === 0) {
                list.innerHTML = '<p>لا توجد إعلانات حالياً.</p>';
                return;
            }
            announcements.forEach((ann) => {
                list.innerHTML += `
                    <div class="card">
                        <h3>${ann.title}</h3>
                        <p>${ann.desc}</p>
                        ${ann.file ? `<p style="font-size:12px; color:var(--primary);">📎 مرفق: ${ann.file}</p>` : ''}
                        <div style="margin-top: 10px;">
                            <button onclick="editAnnouncement(${ann.id})" style="background:#eab308; padding:5px 10px; font-size:12px;">تعديل</button>
                            <button onclick="deleteAnnouncement(${ann.id})" class="danger-btn" style="padding:5px 10px; font-size:12px;">مسح</button>
                        </div>
                    </div>
                `;
            });
        }

        function deleteAnnouncement(id) {
            announcements = announcements.filter(a => a.id !== id);
            localStorage.setItem('mozakra_anns', JSON.stringify(announcements));
            renderAnnouncements();
        }

        function editAnnouncement(id) {
            let ann = announcements.find(a => a.id === id);
            if(!ann) return;
            let newTitle = prompt('تعديل عنوان الإعلان:', ann.title);
            let newDesc = prompt('تعديل تفاصيل الإعلان:', ann.desc);
            if(newTitle !== null && newDesc !== null) {
                ann.title = newTitle;
                ann.desc = newDesc;
                localStorage.setItem('mozakra_anns', JSON.stringify(announcements));
                renderAnnouncements();
            }
        }

        // الدعم الفني وتذاكر المساعدة مع تحديد المدرس وزر الإغلاق والوقت والتاريخ
        function createTicket() {
            const name = document.getElementById('studentNameTicket').value;
            const teacher = document.getElementById('targetTeacherTicket').value;
            const desc = document.getElementById('ticketProblemDesc').value;

            if(!name || !desc) {
                alert('يرجى كتابة الاسم ووصف المشكلة!');
                return;
            }

            const now = new Date();
            const dateStr = now.toLocaleDateString('ar-EG');
            const timeStr = now.toLocaleTimeString('ar-EG', { hour: '2-digit', minute: '2-digit' });

            const newTicket = {
                id: Date.now(),
                student: name,
                teacher: teacher,
                desc: desc,
                status: 'open', // open or closed
                closedAt: '',
                dateTime: `${dateStr} - ${timeStr}`
            };

            tickets.push(newTicket);
            localStorage.setItem('mozakra_tickets', JSON.stringify(tickets));
            
            document.getElementById('studentNameTicket').value = '';
            document.getElementById('ticketProblemDesc').value = '';
            alert('تم إرسال تذكرتك للمدرس المختص بنجاح!');
            renderTickets();
        }

        function renderTickets() {
            const list = document.getElementById('ticketsList');
            list.innerHTML = '';
            if(tickets.length === 0) {
                list.innerHTML = '<p>لا توجد تذاكر دعم فني مسجلة.</p>';
                return;
            }
            tickets.forEach(t => {
                let isClosed = t.status === 'closed';
                list.innerHTML += `
                    <div class="card" style="border-right-color: ${isClosed ? 'var(--success)' : 'var(--danger)'};">
                        <p><b>الطالب:</b> ${t.student} | <b>موجبة إلى:</b> <span class="badge">${t.teacher}</span></p>
                        <p><b>المشكلة:</b> ${t.desc}</p>
                        <p style="font-size:12px; color:var(--text-secondary);">⏰ تاريخ التذكرة: ${t.dateTime}</p>
                        ${isClosed ? `<p style="color:var(--success); font-size:13px;"><b>حالة التذكرة:</b> تم إغلاقها في (${t.closedAt}) ✅</p>` : 
                        `<button onclick="closeTicket(${t.id})" class="success-btn">إغلاق التذكرة (حُلّت المشكلة)</button>`}
                    </div>
                `;
            });
        }

        function closeTicket(id) {
            let t = tickets.find(item => item.id === id);
            if(t) {
                const now = new Date();
                t.status = 'closed';
                t.closedAt = `${now.toLocaleDateString('ar-EG')} الساعة ${now.toLocaleTimeString('ar-EG', { hour: '2-digit', minute: '2-digit' })}`;
                localStorage.setItem('mozakra_tickets', JSON.stringify(tickets));
                renderTickets();
            }
        }

        // بحث وتحديد عدة حسابات طلاب دفعة واحدة في لوحة المعلم
        function initStudentsSearchUI() {
            renderStudentsCheckboxList(studentsDatabase);
        }

        function renderStudentsCheckboxList(arrayToRender) {
            const container = document.getElementById('studentsMultiSelectContainer');
            container.innerHTML = '';
            arrayToRender.forEach(s => {
                container.innerHTML += `
                    <label style="display:flex; align-items:center; gap:8px; margin:4px 0; font-size:14px;">
                        <input type="checkbox" value="${s.id}" class="student-checkbox"> 
                        <b>كود: ${s.id}</b> - ${s.name} (${s.group})
                    </label>
                `;
            });
        }

        function filterStudentsSearch() {
            const query = document.getElementById('studentSearchQuery').value.toLowerCase();
            const filtered = studentsDatabase.filter(s => s.name.toLowerCase().includes(query) || s.id.toString().includes(query));
            renderStudentsCheckboxList(filtered);
        }
    </script>
</body>
</html> 
